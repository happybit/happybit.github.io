---
layout: post
title: "Linux Driver for RTL8188CE"
date: 2014-11-28 21:25
comments: true
categories: Archlinux
---

Arch Linux on ThinkPad T420i sucks due to the stock wireless network card -- RealTek RTL8188CE. The wireless connection keeps dropping and most of the ping packages are lost even to the router(Netgear WNDR4300) in home LAN.

<!--more-->

I have tried several ways mentioned on the internet. For instance, disable IPv6 or replace `netctl` by `NetworkManager`, etc. The situation becomes even worse. The wireless would disconnect completely after a short while and cannot bring back to live again.

Till recently, I found [this modified driver](https://github.com/FreedomBen/rtl8188ce-linux-driver) for RTL8188CE. It's not the official driver but fixes some issue on official driver.

If you have the similar problem, please try this driver. Don't forget to explore #Troubleshooting section if the problem still exists. The fixed rate commands finally help to solve my problem.

Really appreciate the author's sharing. :smile:
