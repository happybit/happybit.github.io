---
layout: post
title: "RACH Part 4: AICH transmission timing"
date: 2014-06-21 11:15:08 +0800
comments: true
categories: Radioaccess
---

*AICH transmission timing*, either *0* or *1*, is informed to UE by RNC in SIB5/5bis via BCH. 

<!--more-->

* If *AICH transmission timing* is 0, the next PRACH preamble will be initiated at earliest 3 access slots later after previous failed(no acknowledggement or acknowledggement is NACK) PRACH preamble. And AICH is expected to arrive at UE after 1.5 access slots;
* If *AICH transmission timing* is 1, the next PRACH preamble will be initiated at earliest 4 access slots later after previous failed(no acknowledggement or acknowledggement is NACK) PRACH preamble. And AICH is expected to arrive at UE after 2.5 access slots;

Below figures show the timing of the whole PRACH process when *AICH transmission timing* is 0. *t<sub>AIF</sub>* stands for the transmission time on the air interface. Whereas *t<sub>proc</sub>* is the processing time within Node B, including receiving/transmission time in RF and baseband processing time, etc.

![Mapping](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140621_rach_part4_aich_transmission_timing.png)

As you can see, since the duration between PRACH preamble and AICH is fixed as 1.5 access slots, *t<sub>AIF</sub>* impacts *t<sub>proc</sub>* a lot:

2 * *t<sub>AIF</sub>* + *t<sub>proc</sub>* + 4096 chips <= 1.5 access slots

For simplicity, let's assume:

*t<sub>AIF</sub>* = *d<sub>UE</sub>* / *C<sub>light</sub>*

in above formula, *d<sub>UE</sub>* is the distance between Node B and UE while *C<sub>light</sub>* is the light speed, i.e. 3e8 meters per second.

In case the cell radius is 20 kilometers, *t<sub>AIF</sub>* is 0.0667 millisecond. Therefore we can calculate the maximum allowed *t<sub>proc</sub>* is 0.8 millisecond. And the more cell radius, the less *t<sub>proc</sub>* is allowed. So generally, the vendors will limit the maximum cell radius(for instance 60 km) when *AICH transmission timing* 0 is used by the operators. 



