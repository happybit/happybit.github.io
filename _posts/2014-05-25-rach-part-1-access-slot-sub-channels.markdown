---
layout: post
title: "RACH Part 1 - Access Slot and Sub-channel"
date: 2014-05-25 18:55:08 +0800
comments: true
categories: Radioaccess
---

I studied and worked on Enhanced CELL_FACH(3GPP Rel8 feature) during past a few months. This feature was evolved based on R99 RACH and Rel6 E-DCH. Here are some learning notes about R99 RACH.

<!--more-->

Let's get clear about some critial definitions firstly.

## Access slot

As we know, slot is one of the important timing unit in UMTS, just like frame, chip, etc. And one slot consists of 2560 chips whereas one frame(10ms) has 15 slots. However, in R99 RACH, one **Access slot** is 5120 chips instead, i.e. two normal slots. Accordingly, two frames(20ms) have 15 access slots. The reason why one access slot occupies 5120 chips is, one PRACH preamble and AICH is as long as 4096 slots, which is more than one slot but less than two slots.

## Sub-channel

Sub-channel defines a sub-set of the total set of uplink access slots. There are a total of 12 RACH sub-channels. Since two frames have 15 Access slots, and the least common multiple for 12 and 15 is 60 access slots, i.e. eight frames(80 ms). Thus the mapping of access slot and sub-channel remains the same every 80ms.

Here is the table for available uplink access slots for different RACH sub-channels in *3GPP TS25.214 Table 7*. As you can see, for sub-channel #3, it could be:

* #3 access slot in frames with SFN modulo 8 = 0;
* #0 access slot in frames with SFN module 8 = 2;
* #12 access slot in frames with SFN module 8 = 3;
* #9 access slot in frames with SFN module 8 = 5;
* #6 access slot in frames with SFN module 8 = 6;

![RACH part 1_1](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140525_rach_part1_1.png)

Some guys might be confused by above table. So I drew another figure by taking SFN 96~103 as example. SFN 104 is the same as SFN 96 due to the cycle period of 80ms.

![RACH part 1_2](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140525_rach_part1_2.png)

## Summary

Access slot is basic timing unit for R99 RACH for aligning PRACH preamble and AICH channel. Sub-channel is the available set of access slots for certain UE. In my view, sub-channel is the possibility for UE to initiate PRACH preamble. The more available sub-channels, the more possibility to establish a call successfully, especially when there are large quantity of UEs with BHCA (busy hour call attempt).

Regarding how to map sub-channels to certain UE, I will illustrate it in next posts.
