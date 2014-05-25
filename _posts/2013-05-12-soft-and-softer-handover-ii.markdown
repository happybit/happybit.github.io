---
layout: post
title: "Soft and Softer Handover II"
date: 2013-05-12 20:28
comments: true
categories: Radioaccess
---

### Power control during SHO

**Misunderstanding #2:**
> No SHO for HSDPA. There is always only one active RL for HS-PDSCH. Thus there is also only one F-DPCH in downlink during ul SHO.

<!--more-->

Since HSDPA was introduced in 3GPP Rel 5, HSDPA scheduling is handled by MAC-hs in Node B instead of RNC. The major reason why there is no SHO for HSDPA is, shared channel aka HS-DSCH is involved in HSDPA. 

As we know, downlink TPC command is carried on either DPCCH or F-DPCH. 

1. In case of DPCCH, the service would be like DL: HSDPA + DCH / UL: HSUPA (+ DCH). Downlink DCH could perform softer/soft handover without any doubt. So there will be two/three TPC commands in downlink.
2. In case of F-DPCH, the serice is more like DL: HSDPA / UL: HSUPA.

As for ul SHO with #2, HSDPA is still active in former serving cell. But on the uplink, there are already two RLs from UE to two/three different cell in Node B.

Each cell needs to send dl TPC to UE for power control purpose. Thus F-DPCH is definitely active for all cells.

The only difference for softer and soft handover is TPC: 

1. Softer handover: one Node B will receive all the uplink channels from the same UE and bring in diversity gain. Thus TPC might be the same for all cells.
2. Soft handover: two or more different Node Bs receive the uplink channels and generate downlink TPC respectively. So that might be possible that TPCs are different at the same time. From UE perspective, the general rule is firstly to follow "DOWN" command in any case. Because, closed loop power control is as quick as 1500Hz to balance the power. And subsequent cell overload is not a good idea in such case.


