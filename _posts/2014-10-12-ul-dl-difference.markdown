---
layout: post
title: "Modulation difference between UL and DL"
date: 2014-10-12 20:00
comments: true
categories: Radioaccess
---

Last time, one of my colleagues asked me a interesting question regarding the difference of modulation between uplink and downlink. And I'd like to share with you here today.

<!--more--> 

As you know, IQ(In-phase & Quadrature) modulation is widely used in various wireless technologies. And QPSK is adopted for downlink DCH while BPSK for uplink in UMTS. The difference is, one copy of downlink data from one physical channel will split into two and each one will be mapped to each IQ phase. However uplink data from one physical channel would be only mapped to one phase, either in-phase part or quadrature part. Please refer to below figure for illustration.

![IQ modulation](https://dl.dropboxusercontent.com/u/6459697/blogimage/20141012_iq_modulation.png)

I didn't figure out the reason why they are different from official materials. Here are some personal thoughts on it.

Firstly and most importantly, BPSK is less complicated than QPSK, which means it needs less power to modulate the signals. And as you know, UE battery power is the key and critical factor for all design considerations.

Secondly, if downlink chooses the same modulation as uplink, it would consume more code resource which is limited and quite precious. At the beginning, the data rate for R99 is not that high. According to below table, you can see that for the same data rate, spreading factor for downlink is twice as minimum SF for uplink. And for the downlink, the bottleneck is code resource instead of power consuming.

|  Service/data rate  |  UL min SF  |  DL SF  |
|-----------|---------|---------|
|  4.75AMR  |  SF128  |  SF256  |
|  12.2AMR  |  SF64  |  SF128  |
|  32kbps  |  SF32  |  SF64  |
|  57.6kbps  |  SF16  |  SF32  |
|  64kbps  |  SF16  |  SF32  |
|  128kbps  |  SF8  |  SF16  |

Last, multiple physical channels with big SF will cause larger PAR(peak to average power ratio) than single physical channel with small SF. For instance, one DPDCH channel with SF4 carries the same rate of data as two DPDCH channel with SF8. However, according to TFC selection mechanism in 3GPP(as well as E-TFCI selection for E-DCH), UE inclines to choose single SF4 channel other than two SF8 channels. This is also considered from UE power consumption perspective.

Since I didn't search around for the technical discussion/meeting minutes during the initial design. This is just my own assumption. Please let me know if you have second opinion.
