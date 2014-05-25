---
layout: post
title: "2SF2+2SF4 E-DPDCH without ul-DPDCH"
date: 2014-03-09 20:38:10 +0800
comments: true
categories: Radioaccess
---

The reason why ul-DPDCH is not supported for E-DPDCH with 2SF2+2SF4, is presented in 3GPP [TS25.213](http://www.3gpp.org/DynaReport/25213.htm).

<!--more-->

According to Table 0: Maximum number of simultaneously-configured uplink dedicated channels in TS25.213 as below, in case of 4 E-DPDCH channels, there should be no ul-DPDCH configured.

![3gpp_ts25213_table0](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140309_3gpp_ts25213_table0.png)

More specifically, you could refer to [3G Evolution: HSPA and LTE for Mobile Broadband](http://www.amazon.com/3G-Evolution-Second-Edition-Broadband/dp/0123745381). As you can see, when there are 2SF2+2SF4 E-DPDCH configured, there is no extra space for ul-DPDCH in terms of code tree.

![edpdch_with_and_without_dch](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140309_edpdch_with_and_without_dch.jpg)
