---
layout: post
title: "Inner Loop Power Control I"
date: 2014-08-08 22:37
comments: true
categories: Testing
---

Power Control(PC) is one of the most important features in UMTS technology. Here I'd like to introduce the Inner Loop Power Control(ILPC).

<!--more-->

## Intro of power control

Power control, just as the name implies, is the mechanism to adjust the transmission power of physical channels for certain purpose. Generally, the purpose is to achieve the specific quality for the signals with the adequate transmission power. No more, no less. 

![Power control intro](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140808_intro_power_control.png)

Please note, in this context, "power" means the signal strength rather than the battery power or the power consumed by the devices. Though a better power control would eventually make devices consume less battery power.

### Categories

From "feedback" perspective, there are two kinds of power control:

* Open loop power control

  Open loop power control is operated without any direct adjustment indicator from reciever as in below figure. 

  ![Power control intro](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140808_open_loop_power_control.png)

  Before I was using "feedback" but later I found "direct adjustment indicator" was more accurate. For instance, the power control for PRACH preamble is open loop during random access procedure. If no AICH(acknowledge for PRACH preamble) was received by UE, the preamble power shall increase step by step(power ramp step) till:
	    
  1. Maximum preamble retransmission number is reached; or
  2. Maximum preamble power is reached; or
  3. AICH, either ACK or NACK, is finially received by UE;

  So actually there is feedback, i.e. AICH, from Node B to UE. However there is no way for Node B to directly inform UE to increase or decrease the power of PRACH preamble. In fact, sort of like one way street, UE could only increase the power or even stop but is forbidden to decrease it during random access procedure.

  ![Power control intro](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140808_rach_preamble.png)

* Closed loop power control

  In contrast to open loop power control, there is straightforward direct indicator from the receiver to inform the transmitter how to adjust the channel power. And then the transmitter would increase/decrease/remain the power level accordingly.

  ![Power control intro](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140808_closed_loop_power_control.png)

  Both uplink and downlink DPCH power control are closed loop while the indicator is called Transmit Power Control(TPC) command.

Meanwhile, from Node B point of view, there are:

* Outer loop power control

  Outer loop power control, a.k.a. OLPC, is mainly proceeded in RNC to derive the SIR target for UL physical channels based on the calculated BLER as well as BLER target. And then RNC will send this SIR target via FP Control Frame to Node B for inner loop power control. 

* Inner loop power control

  As mentioned before, both Node B and UE could sent TPC command carried on DPCCH to each other to tell them to calibrate the power of the corresponding physical channels.

I think both OLPC and ILPC are closed loop power control. In my company, we usually use CLPC which actually refers to ILPC in our daily work .

  ![Power control intro](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140808_inner_outer_loop_power_control.png)
