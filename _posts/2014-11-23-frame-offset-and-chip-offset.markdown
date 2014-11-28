---
layout: post
title: "Frame Offset and Chip Offset"
date: 2014-11-23 22:17
comments: true
categories: Radioaccess
---

Frame Offset and Chip Offset are timing offset for one radio link in terms of frames and chips. 

<!--more-->

More speficically, it defines the timing offset between downlink DPCH relative to P-CPICH (Look familiar? Yes. It's also the delay for SFN and CFN. Please refer to [SFN and CFN](http://blog.pzheng.me/2014/10/26/sfn-and-cfn/)).

    Toffset = FrameOffset * 38400 + ChipOffset

As you can see from the `Figure 29: Radio frame timing and access slot timing of downlink physical channels`:

![radio frame timing](https://dl.dropboxusercontent.com/u/6459697/blogimage/20141123_radio_frame_timing.png)

t<sub>DPCH,n</sub> is the same as T<sub>offset</sub> in the above equation.

Generally, Frame Offset and Chip Offset are picked by RNC randomly to distribute different radio links' data evenly. Even the chanelisation codes could be used to distinguish different channels, it's still not a good idea to initiate all the radio links at the same time or very closely since it may cause data burst in a short period.

According to 3GPP [TS25.433](http://www.3gpp.org/DynaReport/25433.htm):

> The Frame Offset is the required offset between the dedicated channel downlink transmission frames (CFN, Connection Frame Number) and the broadcast channel frame offset (Cell Frame Number). The Frame Offset is used in the translation between Connection Frame Number (CFN) on Iub/Iur and the least significant 8 bits of SFN (System Frame Number) on Uu. The Frame Offset is UE and cell specific.

Chip Offset definition as well:

> The Chip Offset is defined as the radio timing offset inside a radio frame. The Chip offset is used as offset relative to the Primary CPICH timing for the DL DPCH or for the F-DPCH.

And the technical speficiation also defines the value range of Frame Offset is [0, 255] while that of Chip Offset is [0, 38399].

However, [_Radio Access Networks for UMTS_](http://www.wiley.com/WileyCDA/WileyTitle/productCd-0470724056.html) mentions that, usually, RNC will only select Frame Offset from [0, 7] randomly for a new set-up radio link:

> When a UE makes the transition to CELL_DCH and the first DPCH radio link is established the range is limited to between 0 and 7. In this scenario, a range of eight radio frames is sufficient and corresponds to the maximum Transmission Time Interval (TTI) of 80 ms. This range of 8 radio frames is mirrored by the maximum range defined for the corresponding RRC signalling used to inform the UE of the equivalent information... the full range of frame offset values become applicable when a UE enters soft handover and the NBAP Radio Link Setup Request message is used to specify the timing of a new radio link. 

