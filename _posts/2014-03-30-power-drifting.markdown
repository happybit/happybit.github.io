---
layout: post
title: "Power Drifting"
date: 2014-03-30 17:08:45 +0800
comments: true
categories: Radioaccess
---

Closed loop power control (CLPC), a.k.a. fast power control, is an important feature in UMTS to adjust both uplink and downlink power level between Node B and UE via Transmit Power Control (TPC) commands. However the other side of CLPC is power drifting during soft handover ([1](http://blog.pzheng.me/blog/2013/04/02/soft-and-softer-handover/) & [2](http://blog.pzheng.me/blog/2013/05/12/soft-and-softer-handover-ii/)). In subclause 9.2.1.3 of *WCDMA for UMTS: HSPA Evolution and LTE (5th Edition)*, the authors have presented the cause and possible solvement for this issue. So I don't bother to repeat it again. Just some personal thoughts to help me deeply understand.

<!--more-->

Please think about below questions before proceeding further. Let's assume there are two cells in active set, which means two Node B are involved during soft handover.

1. How many ul-DPCCH/DPDCH are there during SHO?
2. How many TPC commands on the uplink from UE to Node B?
3. Why does downlink tranmission power need to be consistent from two Node B?
4. What is the impact of power drifting?

## Question #1&#2

Actually Q#1 and Q#2 are the same. UE needs to add anothe radio link (RL) to another cell (Node B) for SHO. Scrambling code is used on UL to distinguish UEs, which means two Node B will receive one copy of UL data from UE during SHO. Therefore, there is only one pair of ul-DPCCH/DPDCH as well as only one UL TPC commands.

If you still cannot understand, please think about how it could be possible to allocate uplink I/Q code tree if one more ul-DPCCH/DPDCH is added for 2ms TTI E-DCH user with 2SF2+2SF4 of E-DPDCH set.

## Question #3

Please note, here I use "consistent" instead of "equal". Because CPICH power might be different in two involved cells (Node B). To be more specific, we need to equalize the **power windows** of these two cells.

Why do we need to keep them consistent? UE will softly combine the downlink signals from two different cells. Thus in order to stabilize power control, the combined signal power is expected to be the same when UE moves from one cell to anther without considering other factors like interference except the distance. While the respective received power could reflect the distance between UE and Node B to some extend.

## Question #4

* If the real TPC command is **UP**, and any one of the Node B mis-decodes it as **DOWN**. It will result in smaller Eb/N0 than expected on UE side, which would lower the gain of soft combining.
* If the real TPC command is **DOWN**, and any one of the Node B mis-decodes it as **UP**. Though it will not impact UE receiving. It is a waste of power and impacts the power level of other UEs, i.e. impacts the capacity of whole cell.

## Summary

To summarize, it's definitely necessary to prevent power drifting. Especially the frequency of CLPC is as quick as 1500 per second while there is only one bit for TPC command. Moreover, SHO usually happens on the edge of cells, which means the channel condition is not good enough. It's very likely that Node B would misinterpret TPC commands during SHO.
