---
layout: post
title: "RACH Part 2: Access Class and Access Service Class"
date: 2014-06-08 11:06:08 +0800
comments: true
categories: Radioaccess
---

In [previous post](http://blog.pzheng.info/blog/2014/05/25/rach-part-1-access-slot-sub-channels/), I have illustrated the access slot and sub-channel is the basic time unit for PRACH. As we know, RACH is **R**andom **A**ccess **Ch**annel which means UE shall initiate PRACH preamble *somehow* randomly. However, it doesn't mean UE could access to network at any access slot. The Access Service Class(ASC) defines the available sub-channels as well as PRACH preamble signatures.

<!--more-->

## Define ASC

### UE in Idle mode

Access Class(AC) is ranged from 0 to 15, while normal UE is randomly allocated AC between 0~9(stored in USIM). AC 10 is not used in field. And AC 11-15 are usded for special or emergency services.

When UE in RRC Idle mode tries to access to the network via PRACH preamble, it will firstly read system information(SIB) from BCH(physical channel P-CCPCH), to get the "AC to ASC mapping table". The value range of ASC is [0, 7] which is totally eight values.

Here is a snippet of SIB5.

![snippet of SIB 5](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140608_rach_part2_sib5.png)

There are seven IEs in the block of "ac-To-ASC-MappingTable". And each IE corresponds to certain ACs and their ASC respectively as below table. Please note to not mix these seven IEs with eight possible ASC values.

![snippet of SIB 5](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140608_rach_part2_ac_asc_mapping.png)

Hence we can find that all ACs' ASC is **0**, i.e. there is only one Access Service Class for this PRACH. Thus there is only one PRACH partitioning as shown in the snippet of SIB5. If there are two ASC (0 and 1), there will be two PRACH partitioning. And the first one for ASC 0 whereas the other one for ASC 1.

### UE in connected mode

When UE is in connected mode, i.e. CELL_FACH mode, ASC is decided by:
    ASC = Min(MLP, NumASC)

In which, *MLP* stands for MAC Logical Channel Priority signalled to UE for each logical channel. And *NumASC* is the configured maximum ASC number.

## Next step

In PRACH partitioning block, we can find the available PRACH preamble signatures and sub-channels. But it's still implicit. We need to combine these infomations with PRACH RACH Info in SIB5 to get the exact available signatures and sub-channels. I will explain it later.
