---
layout: post
title: "Inner Loop Power Control II"
date: 2014-08-16 19:25
comments: true
categories: Radioaccess
---

Inner Loop Power Control exists on both uplink and downlink. For the uplink, Node B will send TPC(Transmit Power Control) command to UE which would adjust its own transmission power accordingly. Vice versa for the downlink.

<!--more--> 

### TPC command for UL ILPC

TPC command is carried on downlink DPCCH for R99 users. Figure 2 in 3GPP [TS25.211](http://www.3gpp.org/DynaReport/25211.htm) shows the TPC command in DPCCH fields.

![dl DPCH structure](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140816_dl_dpcch_frame_structure.png)

After HSDPA was announced in 3GPP Release 5, the data and TFCI could be carried on HS-PDSCH and HS-SCCH. If each user is configured with downlink DPCH(including DPDCH/DPCCH), RNC needs to reserve one channelization code for each user. The impact, that the DPCH occupy considerable portion of the downlink channelization codes, may emerge as the user amount increases. Fortunately, F-DPCH was introduced in 3GPP Release 6 to relieve such burden. 

The spreading factor is fixed as 128 which is fairly large. Therefore, it's not a big problem for RNC to allocate several F-DPCH codes on the downlink code tree with limited channelization code resource. As illustrated in Figure 12B in 3GPP TS25.211, each slot of F-DPCH consists of N<sub>OFF1</sub> bits, N<sub>TPC</sub> bits and N<sub>OFF2</sub> bits. 

![F-DPCH structure](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140816_fdpch_structure.png)

The exact bits number of N<sub>OFF1</sub>, N<sub>TPC</sub> and N<sub>OFF2</sub> depends on F-DPCH slot format as Table 16C in 3GPP TS25.211. N<sub>OFF1</sub> and N<sub>OFF2</sub> are actually DTX with nothing transmitted.

![F-DPCH slot format](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140816_f-dpch_slot_format.png)

Basically users sharing the same F-DPCH code would have different F-DPCH slot formats to distribute TPC commands for all users evenly on F-DPCH channel without overlapping. One F-DPCH code could carry TPC commands for at most **TEN** users.

![F-DPCH slot format](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140816_f-dpch_ten_users.png)

However, the above figure is not accurate enough. Since it doesn't take the user specific delay(compared to P-CPICH), i.e. chip offset, into account for the timing alignment. If the chip offset of user 1-10 are 0/256/512/.../2304 respectively which happens to be just 1/10 slot in between. It will lead to the overlapping of TPC commands transmission between User 1 and User 6 (as well as User 2 and User 7, etc.) as below figure.

![F-DPCH overlapping](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140816_f-dpch_ten_users_chipoffset_overlapping.png)

Then you could just adjust either the chip offset or the F-DPCH slot format for each user. But usually RNC will take care of all the stuff for you. Here is one example as all users share the same F-DPCH code and the same F-DPCH slot format at the same time.

![F-DPCH non-overlapping](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140816_f-dpch_ten_users_chipoffset_non_overlapping.png)

You may ask, if there is no downlink DPCH, where are the pilot bits after all data/TFCI/TPC bits could be carried on other channels? I will explain it later.
