---
layout: post
title: "ACK/NACK/DTX in HSDPA"
date: 2013-03-07 21:08
comments: true
categories: Radioaccess
---

I own a localhost wiki based on [DokuWiki](https://www.dokuwiki.org/) as my personal knowledge management tool. After more than two years collecting day by day, I am pleased to see more and more tips/experience in different areas appearing on it. I don't think I will publish the whole wiki on the internet in the near future. But I'd like to orgnize and share some of the topics on this site. 

The first post is about HSDPA's acknowledge.

<!--more-->

As we know, ACK/NACK which is carried on uplink HS-DPCCH is sending from UE to inform Node B whether it has received/decoded certain transport block successfully. 

The meanings of ACK/NACK/DTX are as obvious as their names express:

* ACK: Transport block is decoded correctly by UE;
* NACK: Transport block is decoded incorrectly;
* DTX: discontinuous transmission.

Actually, it's not that simple. We could tell more from these different states. 

According to [chapter 6.2.6 ACK/NACK Transmit Power Reduction for HS-DPCCH](http://books.google.com/books?id=pl6U09IkLHwC&pg=PA174&lpg=PA174&dq=hs-scch+fail+nack+ack+dtx&source=bl&ots=r-SporHp0o&sig=zW_--9jdV5J6QmAimxPNjRTHwY8&hl=en&ei=GlSyTvbZBq3V4QT73PHLAw&sa=X&oi=book_result&ct=result&resnum=10&ved=0CFoQ6AEwCQ#v=onepage&q&f=false|Mobile communication systems and security]]) in *Mobile Communication Systems and Security* by *Man Young Rhee*.

> In Release 5, the UE always uses DTX in the ACK/NACK field of the HS-DPCCH except when an ACK or NACK is being transmitted in response to an HS-DSCH rtansmission. This means that if the UE fails to detect typical probability 0.01 of the HS-SCCH, the UE will use DTX in the corresponding ACK/NACK field. The Node B must avoid decoding this DTX as ACK if it is to avoid loss of the HS-DSCH TTI at the physical layer.

In summary:

 1. If HS-SCCH is not decoded successfully(no matter which part is wrong, part 1 or part 2), UE will not send any ACK/NACK info on HS-DPCCH, which is **DTX**.
 2. If HS-SCCH is successful but HS-PDSCH CRC is failed, **NACK** will be sent.
 3. Only if both HS-SCCH and HS-PDSCH are decoded correctly, UE will send **ACK**.
