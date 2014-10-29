---
layout: post
title: "SFN and CFN"
date: 2014-10-26 17:00
comments: true
categories: Radioaccess
---

在UMTS中，同步是很重要的一项工作。如果同步出现问题，轻则某些用户无法建立通话连接，重则整个小区网络瘫痪。而同步中，有两个重要的概念，经常会碰到。那就是SFN和CFN，所有的物理信道都将基于SFN对齐或做一定的偏置。

<!--more--> 

要谈SFN和CFN，还有一个BFN不得不提：

* BFN: Node **B** **F**rame **N**umber. 一个Node B内所有小区的参考时钟，是Node B-specific的；
* SFN: **S**ystem **F**rame **N**umber. 每个小区独立的时间，是cell-specific的；
* CFN: **C**onnection **F**rame **N**umber. 表征UE和UTRAN之间的时间关系，是user-specific的；

SFN是在BFN的基础上，加上T<sub>cell</sub>值区分同一个Node B下各个小区的。T<sub>cell</sub>取值0~9，代表的实际偏置值是T<sub>cell</sub>*256 chips。同频小区不可使用相同的T<sub>cell</sub>，否则UE将不能同步上小区。

每个小区的SFN是在BCH上发送的，UE收到并解出BCH后，将基于SFN推算出CFN。[TS25.211](http://www.3gpp.org/DynaReport/25211.htm) subclause 7中提到的转换关系如下：

    CFN = (SFN + (frame_offset*38400 + chip_offset) Mod 38400) Mod 256

几条基于小区时间(而不是RL-specific或UE-specific)的物理信道，其他信道具体时序关系请参看TS25.211 subclause 7.

* 小区的P-CCPCH和SFN是对齐的；
* HS-SCCH和小区的P-CCPCH的SFN是对齐的，HS-PDSCH落后HS-SCCH两个slots;
* E-AGCH是在小区的P-CCPCH基础上，延迟5120个chips对齐的；



