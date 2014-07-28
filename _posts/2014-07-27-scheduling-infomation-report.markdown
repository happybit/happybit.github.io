---
layout: post
title: "Scheduling Information Reporting"
date: 2014-07-27 21:31
comments: true
categories: Radioaccess
---

About half an year ago, we met a problem which resulted in data rate with dramastically ups and downs during load testing. Finally we found it was caused by Scheduling Information(SI) reporting. Here are some learning notes about SI.

<!--more-->

## Prerequisite

Some definitions you'd better to be familiar with in advance:

* SG = "Zero_Grant": it means AG = 1.
* SG <> "Zero_Grant": it means AG is any value between [0, 31] other than 1.
* All processes are deactivated: it means AG = 0 while AG scope = 0 (which means all HARQs).
* At least one process is activated: it means AG > 2 while AG scope = either 1 (single HARQ) or 0.

## What is SI

Scheduling Information(SI) is carried on E-DPDCH along with data. Well, it could be sent as stand-alone SI(18 bits) without any data.

In 3GPP [TS25.321](http://www.3gpp.org/DynaReport/25321.htm) sub-clause 9.2.5.3.2, SI consists of below elements:

* Highest priority Logical channel ID (HLID) (4 bits);
* Total E-DCH Buffer Status (TEBS) (5 bits);
* Highest priority Logical channel Buffer Status (HLBS) (4 bits);
* UE Power Headroom (UPH) (5 bits);

E-DCH scheduler in Node B will use SI as one of the inputs for scheduling algorithm.

## Trigger conditions

There are several trigger conditions to send SI in 3GPP TS25.321.

### SI reporting triggered by SG

According to 3GPP TS25.321 sub-clause 11.8.1.6, there are two major conditions to report SI which depends on SG value.

* SG = "Zero_Grant" or all processes are deactivated
* SG <> "Zero_Grant" and at least one process is activated

And the precondition is "TEBS > 0" because it mentions:

> In CELL_DCH state, when MAC-e or MAC-i is configured, the Scheduling Information shall not be transmitted if the TEBS is zero, even if it was triggered by one of the configured triggering mechanisms.

The brief mechanism is showed in below figure:

![SI reporting](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140727_SI_reporting.jpg)

### SI reporting along with scheduled data

Besides above trigger condition, there is another scenario which could trigger SI reporting in 3GPP TS25.321 sub-clause 9.2.4.2.

> When, due to the quantization in the transport block sizes that can be supported or triggering of the Scheduling Information, the size of the data plus header is less than or equal to the TB size of the E-TFC selected by the UE minus 24 bits, the DDI value [111111] shall be appended at the end of the MAC-e header and a Scheduling Information shall be concatenated into this MAC-e PDU, where DDI value [111111] indicates that there is a Scheduling Information concatenated in this MAC-e PDU. Otherwise, if the size of the data plus header is less than or equal to the TB size of the E-TFC selected by the UE minus 18 bits, a Scheduling Information shall be concatenated into this MAC-e PDU. In any other case it is understood that another MAC-es PDU or Scheduling Information does not fit and it is therefore not necessary to reserve room in the transport block for an additional DDI field.

The basic principle is, whenever there is enough space for SI in that transport block excluding (data + header), SI will be added along with data in that TTI.

## Misunderstanding

Regarding "SI reporting triggered by SG", at first we were not clear about 3GPP statement, especially about the meaning of "becomes":

> If SG **becomes** too small to allow transmission of a single PDU from any scheduled MAC-d flow or if the SG is too small to allow transmission of a single PDU from any scheduled MAC-d flow on that frequency and TEBS **becomes** larger than zero, the transmission of Scheduling Information should be triggered on that frequency.

Later I found this change request was raised by Qualcomm as [RP-070636 CR0362 (Rel-7) R2-073822](http://www.3gpp.org/ftp/tsg_ran/tsg_ran/TSGR_37/Docs/RP-070636.zip). So I turned to Qualcomm enginneers and fortunately they kindly replied soon. They confirmed with below interpretation:

* The UE sends SI when SG becomes too small and TEBS > 0; or
* The UE sends SI when TEBS becomes > 0 and SG is too small.
* The UE only sends once when the above condition is met.
* For the restricted HARQ, our UE follow the spec. accurately such that SI can be on any HARQ.
