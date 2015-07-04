---
layout: post
title: "Testing Less"
date: 2015-07-04 10:01
comments: true
categories: Testing
---

前两天看到一篇[文章](http://blog.acolyer.org/2015/06/25/the-art-of-testing-less-without-sacrificing-quality/) _The Art of Testing Less Without Sacrificing Quality_，挺有意思的，和大家分享一下。

<!--more-->

做软件测试的工程师，常常陷入一种矛盾中。为了保证质量和所谓的“测试覆盖率”，我们需要尽可能**多**的测试，各种可能在客户现场发生的场景。但同时，由于资源限制和项目压力，我们又只能测试**有限**的测试集合。现阶段所面临的主要矛盾，是精力日益增长的质量需要同紧迫的项目交割日期还有有限的资源之间的矛盾。于是，各路大神纷纷祭出各种测试方法，各种流程改进（通常还会冠之以牛逼哄哄的名字），希望能缓解这类冲突。

这篇文章就是微软的Kim Herzig等工程师，提出的一种基于历史数据来优化测试效率的方法。作者称之为THEO（ Test Effectiveness Optimization using Historic data）。并且发表了相关[paper](http://research.microsoft.com/pubs/238350/The%20Art%20of%20Testing%20Less%20without%20Sacrificing%20Quality.pdf)。

工作原理说起来并不复杂。首先，测试中发现的bug通常是两类:

* Genuine defect，真实有效需要改正的bug；
* False alarm，由测试环境测试数据等引入的非真实bug；

因此，可以定义两个相应的参数：

* P<sub>defect</sub>(test,context) = #detectedDefects(test,context) / #executions(test,context)
* P<sub>falsePositive</sub>(test,context) = #falseAlarms(test,context) / #executions(test,context)

接着来判断，一个case，跑它所需要的cost Cost<sub>exec</sub> 和不跑它可能导致的cost Cost<sub>skip</sub>。

* Cost<sub>exec</sub> = Cost<sub>machine</sub> + (P<sub>falsePositive</sub> x Cost<sub>inspect</sub>)
* Cost<sub>skip</sub> = P<sub>defect</sub> x Cost<sub>escaped</sub> x Time<sub>delay</sub> x #Engineers

其中，

* Cost<sub>machine</sub>为占用机器的时间，硬件损耗和维护等成本；
* Cost<sub>inspect</sub>为检视testing团队的时间和人力成本；
* Cost<sub>escaped</sub>为bug逃出去之后分析和修正它所需要的成本；
* Time<sub>delay</sub>和#Engineers分别为修正一个历史bug所需要的时间和会被影响到的工程师数量；

最后，通过比较Cost<sub>exec</sub>和Cost<sub>skip</sub>来判断是否需要跑这个case:

* if Cost<sub>exec</sub> < Cost<sub>skip</sub>, case should be executed;
* Else, case won't be executed;

原理说起来很简单，其实我们在反复优化测试集合，以及为未来release制定test plan时，也反复使用，就是基于某个case，衡量跑与不跑所带来的成本，来决定以后是否还需要继续跑这个case。微软的这个做法就是是基于历史数据，提出了具体量化如何计算成本的算法和过程。如果没有海量的历史统计数据，这里的每一项都将是不确定的变量，导致最终结果不够准确，也无法说服人。

文中提到，使用这种方法，微软的Windows/Office/Dynamics等部门，在两年时间内，case执行数减少了50%，测试时间降低了47%。在保证软件质量的前提下，每个产品线每个开发年度平均可以降低两百万美元的开发成本。经理们看到这里眼睛都要发直了吧。