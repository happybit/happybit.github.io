---
layout: post
title: "UMTS Layers Mapping for 12.2kbps AMR Call"
date: 2013-07-15 03:27
comments: true
categories: Radioaccess
---

Every freshman needs to learn the channel mapping of different layers when comming into UMTS fields. I don't want to repeat those mapping relationships which could be found in almost every wireless book.

<!--more-->

Here is an abstract figure showing the mapping of Logical Channels and Transport Channels, taking 12.2kbps AMR call as an example. Wheneven my mind is messed up about it, I will glance below picture and recall quickly.

![12.2kbps AMR call](https://dl.dropboxusercontent.com/u/6459697/blogimage/20130715_122kbpsamrcall.png)

The biggest pipe stands for a radio link. And there are four Transport Channels for this radio link: DCH1, DCH2, DCH3 and DCH24. 

* DCH24 carries four SRBs, which map to four Logical Channels through RLC.
* DCH1/2/3 map to three Logical Channels respectively. These three DCHs correspond to three classes of voice quality: Class A, Class B and Class C. They share the same AAL2 channels with the same Binding ID.


