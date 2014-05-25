---
layout: post
title: "Soft and Softer Handover I"
date: 2013-04-02 20:38
comments: true
categories: Radioaccess
---

A few days ago, I found myself wasn't so clear about soft and softer handover and misunderstood the whole procedure. So I just read some material and also asked help from some experts who were good at this topic. Here is the summary part I for my learning.

<!--more-->

**NOTE**: SHO stands for soft/softer HO in the following paragraphs.

Firstly, let's take a look at the overall picture of different handovers.

{% img /images/handover.png %}

# UL SHO

**Misunderstanding #1:**
> There are multiple RLs in both uplink and downlink during SHO.

In downlink, there are two/three RLs(radio links) during SHO. Please notice, radio link is just a logic concept which isn't existed but just describes the connection between Node B and UE. But unlike downlink, there is only one RL in uplink. The reason is, in the downlink, scrambling code is used to distinguish the cells, whereas it's used to identify UE in the uplink.

Therefore, Node B should send two/three copies of the same data via two/three different cells with different scrambling codes (2 way/3 way softer handover). At the same time, there is only one copy of data transmitting from UE to Node B. But all cells in active set will recieve it respectively and finally soft-combine it in RAKE.

That is also the reason why "addleg" command could only apply in downlink without uplink in TM500(test equipment from [Aeroflex](http://aeroflex.com/)) command reference.

The same mechanism is also applicable for E-DPDCH/E-DPCCH, as well as associated ul DPCCH and HS-DPCCH. As a result, all uplink channels have got diversity receiving gain.

