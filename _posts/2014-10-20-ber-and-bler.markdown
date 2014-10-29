---
layout: post
title: "BER and BLER"
date: 2014-10-20 7:00
comments: true
categories: Radioaccess
---

BLER and BER are two of the most important key performance indicators(KPI) in any of those wireless products. Let's get a quick review about what they mean and what performance they indicate exactly.

<!--more--> 

BLER stands for **B**lock **E**rror **R**ate while BER is **B**it **E**rror **R**ate. Here `block` means transport blocks and `bit` is information bits. Both BER and BLER are statistic results over a certain period.

> The Bit Error Ratio is defined as the ratio of the bits wrongly received to all data bits sent. The bits are the information bits **above the convolutional/turbo decoder**. A Block Error Ratio is defined as the ratio of the number of erroneous blocks received to the total number of blocks sent. An erroneous block is defined as a Transport Block, the cyclic redundancy check (CRC) of which is wrong. 

Here comes a simple flow chart of decoding downlink DPDCH on UE side. As you can see, BLER measurement takes place at "CRC detection" phase within BTS physical layer. And BER is measured after CRC detection (most often in RNC) when information bits are received and then compared with an **already-known data pattern**. The pattern could be either fixed data or PN9/PN15. Of course pseudo noise patter is preferred.

![BER and BLER](https://dl.dropboxusercontent.com/u/6459697/blogimage/20141020_ber_bler_blocks.jpg)

In above figure, there is also a "DPDCH BER measurement" which is mainly used in internal R&D. This BER is measured by physical layer. Once the data is decoded, physical layer would encode the data and compare it with the original received data from RAKE receiver to calculate DPDCH BER.

BLER indicates the quality of the whole network which is more critical. Because even there is data loss/error during transmission, the original data could be restored to perfect due to coding gain of turbo/convolutional algorithm. Thus BER just reflects the estimation of coding gain.

Usually, in laboratory, we expect zero BER for each channel during low/medium-load testing. And pass criterion for BLER depends on different services and their QoS(Quality of Service). Outer Loop Power Control could help to maintain the BLER target.

If BER/BLER doesn't meet the criteria, we need firstly to fine-tune the test environment. If the test environment could be excluded from suspicion, for BER issue, we can compare the sending and receiving data to check whether they follow the same pattern. For BLER issue, we can start from debugging CRC functionality and then check from top to bottom to find the root cause step by step. In such way, we have found an undermining bug which caused the CRC data was different during retransmission.
