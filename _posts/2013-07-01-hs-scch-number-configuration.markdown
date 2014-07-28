---
layout: post
title: "HS-SCCH Number Configuration"
date: 2013-07-01 06:49
comments: true
categories: Radioaccess 
---

I have met a nasty bug regarding HS-SCCH number during testing Dual Cell HSDPA (DC-HSDPA), which took weeks to debug on both Node B and testing equipment side.

<!--more-->

With DC-HSDPA enabled, one UE could only monitor up to 6 HS-SCCH channels in both cells (one dual cell pair), e.g. 3+3, 2+4, 4+2, etc. Usually we'd like to use 3+3 configuration. But really it's up to the vendors. No specific limitation in 3GPP specification regarding this point.

However, there are still 8 HS-SCCH codes available from Node B perspective for these two cells. Then if Node B doesn't inform UE which three out of four HS-SCCH codes will be scheduled in one cell, UE might miss some data due to this mismatch.

The whole process is like this:

1. Node B gets available HS-SCCH codes for each cell via NBAP: Physical Shared Channel Reconfiguration (PSCR) message.
2. RNC sends NBAP: radio link set up message to Node B.
3. Node B sends back radio link set up response message to RNC with specific HS-SCCH codes (in certain sequence).
4. RNC sends RRC: radio link set up message to UE with those HS-SCCH codes (the same sequence).

According to [TS25.212](http://www.3gpp.org/ftp/Specs/html-info/25212.htm) section 4.6.2.3, P and O should fulfil the following formula:

    |*O*-1-|\_*P*/8\_| * 15| mod 2 = (HS-SCCH number) mod 2

    *P* stands for the total HS-PDSCH code number, while *O* the start HS-PDSCH code number. |\_*x*\_| means downward round.

Generally, HS-SCCH number is the index of HS-SCCH codes in radio link set up response message (step #3). For example, in one cell, there are 4 HS-SCCH codes, 4, 8, 9 and 10 in a row. UE 0 is assigned as 4/8/9, and UE 1 as 8/9/10, UE 2 as 8/10/4, etc. For UE 0, the HS-SCCH number for code 4 is 1, code 8 is 2, code 9 is 3. The same is applicable for UE 1, 2, and so forth.

But if you misunderstand HS-SCCH number as the index of HS-SCCH number in PSCR message for the whole cell as below. For instance, in PSCR code 4/8/9/10 is allocated to this cell as this sequence. Please don't make mistake that code 4 as HS-SCCH number 1 for all users. That would result in so unexpected problems since it leads to misbehaviour in above formula.

As you may know, HS-SCCH amount is updated with Multi-Carrier HSDPA arising. But the same formula should be followed no matter how the amount changes.
