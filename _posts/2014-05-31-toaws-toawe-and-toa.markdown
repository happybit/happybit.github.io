---
layout: post
title: "TOAWS, TOAWE and TOA"
date: 2014-05-31 22:12:08 +0800
comments: true
categories: Radioaccess
---

Last time one of my colleague asked me what was *TOAWS*, *TOAWE* and *TOA*. I knew it related to Frame Protocol and *TOA* was time of arrival. But I cannot remember any more. So I did some investigation and here are some notes.

<!--more-->

These definitions were initiated by Nokia in [Tdoc R3-99663](http://www.3gpp.org/ftp/tsg_ran/WG3_Iu/TSGR3_05/docs/Zips/R3-99663.zip) and refined by Ericsson in [Tdoc R3-99875](http://www.3gpp.org/ftp/tsg_ran/WG3_Iu/TSGR3_06/docs/Pdfs/r3-99875.pdf) in 1999. Please note, in R3-99875, it mentioned 3GPP [TS25.401](http://www.3gpp.org/DynaReport/25401.htm)(V1.2.1) would be updated accordingly. But later "the synchronisation in UTRAN" was seperated as an individual 3GPP [TS25.402](http://www.3gpp.org/DynaReport/25402.htm). So the official definitions are presented in sub-clause 5 of TS25.402(V11.0.0) while the mechanism is introduced in sub-clause 7. of the same 3GPP technical specification.

These three timers are used for transport channel synchronisation, more specification, timing adjustment on Iub/Iur. Figure 10 in TS25.402 explains how it works.

![toaws toawe toa](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140531_toaws_toawe_toa.png)

*TOAWS*(Time of Arrival Window Startpoint) and *TOAWE*(Time of Arrival Window Endpoint) are defined in NBAP messages for Transport bearer Setup/Addition/Reconfiguration.

In above figure, it's assumed that the target CFN on air interface is 152 for certain tranport block. Since Layer 1 in Node B needs processing time(t<sub>proc</sub>) to encode, transmit etc. Therefore, this tranport block should arrive in Node B before CFN 152. Node B will send control frame to RNC for timing adjustment with *TOA* which is the time difference between the *TOAWE* and when a data frame is received.

* If TBS arrives too early before *TOAWS*, it will increase the burden of buffer in Node B. Node B will send Timing Adjustment Control frame with positive *TOA* to RNC;
* If TBS arrives right between *TOAWS* and *TOAWE*, timing is perfect. Thus no Timing Adjustment Control frame needed;
* If TBS arrives between *TOAWE* and *LTOA*, Node B is still able to process such TBS. But it's a bit late and dangerous that Node B might not be so quick to process it. So Node B will send Timing Adjustment Control frame with negative *TOA* to RNC;
* If TBS arrives too late even after *LTOA*, Node B is unable to process this TBS and it will send Timing Adjustment Control frame with negative *TOA* to RNC;

After RNC receives Timing Adjustment Control frame with *TOA*, it will adjust the DL data sending timing accordingly, to synchronize with Node B in this way.

The situation is more complicated during soft handover. Please check Figure 14 in TS25.402 for more details.
