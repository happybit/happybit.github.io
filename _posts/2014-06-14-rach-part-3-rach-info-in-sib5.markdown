---
layout: post
title: "RACH Part 3: RACH info in SIB5"
date: 2014-06-14 07:06:08 +0800
comments: true
categories: Radioaccess
---

All of the RACH related information is broadcasted on SIB5/5bis via BCH. [Last time](http://blog.pzheng.info/blog/2014/06/07/rach-part-2-ac-and-asc/), the *PRACH partitioning*, which contained the available PRACH preamble signatures and sub-channels, was elaborated in details. But as I mentioned, we need more info to check the exact available signatures and sub-channels.

<!--more-->

Once I was confused about SIB5 and SIB5bis and later found they were almost identical. On [Agilent website](http://wireless.agilent.com/rfcomms/refdocs/wcdma/wcdma_gen_bse_freqbandind.html) it says:

>SIB5bis was introduced by 3GPP as a way to allow new frequency bands to be created that overlap existing frequency bands. For example, when Band IV was introduced it overlapped Band I. To prevent older Band I UEs from camping on Band IV cells (and then transmitting their PRACH messages on the wrong uplink frequency due to a different Tx/Rx frequency separation), Band IV networks transmit SIB5bis instead of SIB5. Band IV UEs expect SIB5bis and can camp to the cell, but older Band I mobiles simply see that SIB5 is missing and thus do not camp to the Band IV cell. SIB5bis is identical to SIB5 except for the SIB type.

In *PRACH System Information List* of SIB5/5bis, there is one Information Elements block called *PRACH RACH Info*. Basically, it specifies the available signatures and sub-channels for this PRACH as well as other necessary info like available SF, preamble scrambling code word number and puncturing limit, etc.

With this part of information and *PRACH partitioning*, we can finnally get the exact available signatures and sub-channels rather than just index or bit number.

![SIB 5/5bis](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140614_rach_part3_sib5_sib5bis.png)

The mapping for available sub-channels is kind of tricky between *PRACH Partitioning* and *PRACH System Information List*. Because *AICH Transmission Timing* should be also taken into account. And you can find the specific mechanism in [TSG WG1#5 (99) 650](www.3gpp.org/ftp/tsg_ran/wg1_rl1/TSGR1_05/.../r1-99650.pdf). (I will introduce *AICH Transmission Timing* in next post and how it impacts Node B process.)

So now we can see the whole mapping is presented as below.

![Mapping](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140614_rach_part3_sib5_sib5bis.png)

