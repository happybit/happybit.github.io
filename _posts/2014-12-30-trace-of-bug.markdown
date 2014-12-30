---
layout: post
title: "Trace Of Bug"
date: 2014-12-30 13:54
comments: true
categories: Radioaccess
---

这是很早以前遇到的一个关于MIMO HSDPA的问题，其实是在研究其他问题的时候，顺带发现的。后来同事和我深究下去，最后发现还真是一个bug。

<!--more-->

## Table Of Contents

0. [Intro](#intro)
1. [Background knowledge](#background-knowledge)
2. [Deduction](#deduction)
3. [Summary](#summary)

## Intro

起初，我们在一个多用户的MIMO HSDPA测试用例里，同一个Node B中identical的两个cells内，分别建立一个QoS完全相同的MIMO HSDPA用户。最终出来的结果与预期一样，两个用户的data rate相同。不过，在研究log时，无意发现两个用户的HS-SCCH power level差别很大。其中一个用户是我们预设的*minimum HS-SCCH power*，而另一个用户比前者高接近9dB（也就是差不多8倍）。**为何会出现配置相同的小区和用户，HS-SCCH power差别如此之大呢？**

## Background Knowledge

我们知道，3GPP协议规范中并未明确指出关于HSDPA相关的两个物理信道---HS-PDSCH和HS-SCCH--的power control的细节，**具体算法完全up to vendors**. 虽然这不是必须的，但大部分公司还是在这两条信道上做了一定的power control以增进基站性能。

一般来说，这两个信道的power变化不会太剧烈，因为用于传data的HS-PDSCH优先级较其他R99的信道较低，通常都是在为R99的下行DCH信道以及HSUPA的下行信道分配完power之后，整个小区的剩余power几乎都可供HS-PDSCH使用。因此，基站完全可以基于需传的数据来合理控制power的大小，如果真的是信道质量非常差，power control算法一直需要抬升功率的话，它至多提升到将剩余power用完的程度，不能再多了。而用于传control信息的HS-SCCH，相较而言，就更需要稳定了。因为一来它的spreading factor很大，为128，也就是说速率相对较低，所需power也较低。二来为了保证control信息的稳定接收（因为如果这部分信息接收不稳定，就无法保证数据部分的正确接收了），对这条信道的power调整通常也不会太剧烈和太频繁。

说到power control，总要有一定的feedback作为算法输入，才能进行相应的调整。对HSDPA来说，上行只有一条信道HS-DPCCH，由用户反馈ACK/NACK信息以及CQI信息。因此通常算法也会围绕这些feedback来做文章。具体算法每个公司不同，此处细节略过。

## Deduction

### Rough Checking

实验室环境比真实无线环境简单，从算法推导，HS-SCCH power理应处于*minimum HS-SCCH power*的状态。因此，倾向于认为是power较高的那个小区出了问题。

我们发现，两个UE的BLER都接近零，接收过程一直是连续的，不存在DTX的情况。因此ACK/NACK这条路我们认为是近乎相同的。检查UE和Node B两端的log也证实了我们的想法。

接着怀疑点自然就放在CQI上了。因为在实验室空口质量非常好，所以CQI照道理应该质量也非常好。在检查了power较高的UE和Node B两侧的log后发现端倪。UE侧显示CQI值是每九个TTI上报CQI 14后，会紧接着的一个TTI上上报CQI 30，以10个TTI为一个周期循环往复。但是Node B侧的log显示CQI值有一定的规律，但值的变化并不是9+1的形式。

OK. 现在初步定位了问题在哪儿，我们需要仔细研究一下关于MIMO的CQI上报。

### MIMO CQI Reporting

MIMO HSDPA的CQI上报和普通HSDPA用户不同。[3GPP TS25.214](http://www.3gpp.org/DynaReport/25214.htm) sub-clause 6A.1.2.2中指出，MIMO HSDPA用户会依次上报Type A和Type B的CQI values。符合下面公式的TTI就会上报Type A CQI，不符合的就会报Type B CQI.

![MIMO CQI](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140705_feature_grooming_xmind.png/20141230_MIMI_CQI.jpg)

简单说，CQI是UE对下行pilot的测量，Node B收到CQI后可以大致得到UE推荐的transport block size。因此：

* Type A就是UE基于当前的信道质量推荐的CQI value：
  * 如果信道质量够好速率够高可以用双流，取值为 15*CQI<sub>1</sub>+CQI<sub>2</sub>+31。这种情况下，CQI取值范围是4bit, [0, 14];
  * 如果信道质量不够好也可以使用单流，取值为CQI<sub>s</sub>。取值范围是5 bit，[0, 30];
* Type B就是假设当前只能传输primary transport block，也就是单流模式的情况下，基于当前的信道质量，UE给出的CQI值。因此这种CQI值和普通的HSDPA CQI取值范围相同，为[0, 30]。Type B的频率通常较Type A更慢。引入Type B CQI的动机是假设信道条件很好，CQI值也很高，但是Node B暂时没有那么多数据需要传输的时候，就可以参考Type B的CQI只用单流来发送数据即可；

#### k'

    k' = k/(2ms)

其中k是CQI feedback cyle. 此处假设为2 ms.

#### CFN

UE和Node B内部主要基于SFN，所以需要进行SFN和CFN的转换，参见[该文](http://blog.pzheng.me/2014/10/26/sfn-and-cfn/)。

#### N/M ratio

N/M ratio是Node B内部定义的一个参数，取值范围有10个，依次是1/2, 2/3, 3/4,..., 9/10, 1/1. 在我们的测试用例中，这个值为9/10，所以*M_cqi*为10，同时*N_cqi_typeA*为9.

#### m

*m*值是基于[3GPP TS25.211](http://www.3gpp.org/DynaReport/25214.htm) sub-clause 7.7算出来的:

m = (T<sub>TX_diff</sub>/256 ) + 101

其中T<sub>TX_diff</sub>是下面两个timing的时间差，单位是chips（T<sub>TX_diff</sub> =0, 256, ....., 38144）：

* 该HS-PDSCH子帧的起始传输时间(参看sub-clauses 7.8 and 7.1)； 
* 下行DPCH或F-DPCH的起始时间(参看sub-clause 7.1)； 

一个frame有5个sub-frames，也就是5个HSDPA TTI。所以对某个特定的radio link来说，随着SFN的变化，*m*会有5个值。

同样，基于TS25.211 sub-clause 7.1，所有下行的时序都是基于P-CCPCH的:

* DPCH/F-DPCH: t<sub>DPCH,n</sub>或t<sub>F-DPCH,n</sub>，即RL frame offset * 38400 + chip offset;
* HS-PDSCH: 第一个HS-SCCH帧的时序是和P-CCPCH对齐的。所以一个DPCH frame里对应的5个HS-SCCH子帧取值就是{0, 2560*3, 2560*6, 2560*9, 2560*12}. HS-PDSCH晚于HS-SCCH两个sub-frames，也就是5120 chips;

所以，*T<sub>TX_diff</sub>*的取值范围就是{5120 - t<sub>DPCH,n</sub>, 12800 - t<sub>DPCH,n</sub>, 20480 - t<sub>DPCH,n</sub>, 28160 - t<sub>DPCH,n</sub>, 35840 - t<sub>DPCH,n</sub>}。由此也可以算出*m*对应5个子帧的取值范围。

#### Instance

假设frame offset和chip offset都为0，则T<sub>TX_diff</sub> ∈ {5120, 12800, 20480, 28160, 35840}. 而 *m* ∈ {121, 151, 181, 211, 241}.

我们以SFN 1972 sub-frame 4(sub-frame是0/1/2/3/4)为例，CFN = 1972 mod 256 = 180, *m*为241。所以公式中:

    Left hand = Rounddown((5*180 + roundup(241 * 256/7680))/1) mod 10 = 9

因为*N_cqi_typeA*也为9，公式左右相等，因此符合传输Type B CQI的上报时刻。

但是我们发现这个时候在UE侧上报的是一个Type A的CQI value。最终确认问题出在UE端的CQI上报时序出错。而此时Node B还是以正确的时序尝试去解HS-DPCCH时，解出来的CQI值就全是乱的，因此导致Node B认为CQI变化过大，一直在尝试升HS-SCCH的power，最终导致我们看到一个cell的HS-SCCH power比另一个高很多的情况。

## Summary

这是一次从下行方向细微处发现的小问题，研究至上行方向反馈，最后追溯到UE处为止，探索bug的踪迹。在此之前，我对MIMO的两种type CQI没有太深入的研究，借这次bug的契机，学习和巩固了MIMO以及时序方面的知识，实在是一次有意义又有趣的explore之旅。
