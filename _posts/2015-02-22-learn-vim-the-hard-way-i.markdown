---
layout: post
title: "Learn Vim The Hard Way I"
date: 2015-02-22 21:08
comments: true
categories: Productivity
---

使用“神之编辑器”Emacs有几年了，当初学它主要看中了org-mode，用来实现GTD。带着目的去学，倒也没遇到大的问题。有问题就[Google](https://www.google.com.hk/search?q=emacs)，99.9%都有现成的解决方案。虽然不怎么懂elisp，照猫画虎也学着写了一些configuration file，来满足自己的定制需求。因此，一直也使用Emacs作为唯一的编辑器，未考虑过移情别恋“编辑器之神”Vim。

<!--more-->

**NOTE:** 本文不涉及Emacs和Vim之间的[flame war](http://en.wikipedia.org/wiki/Editor_war)。我相信理智之人能包容地看待事物，并能按需选择适合自己的，而不是“非此即彼”地全盘否定另一方。尤其是面对两个历史如此悠久的工具时，更应谨慎。

知道Vi/Vim是很早之前的事情了，读书的时候偶然看到有同学在命令行里运指如飞。那时还处于“命令行恐惧症”时期，打字可能都比较生硬且强烈依赖鼠标，接触过的编辑器估计还停留在Notepad和MS Word阶段。了解一番后觉得操作太反人类，放弃了。后来学习期间经常需要在Linux/Unix机器上设计电路图，免不了需要编辑一些文件，仍未学会，就是需要用的时候查一下基本操作。主要还是不习惯normal mode和insert mode之间的切换，已经不能使用方向键。工作后心血来潮也多次想捡起来再学学，又数次放弃。至后来因长期使用Emacs，更是一去不复返，断了学Vim的念头。

前两个月下定决心要学一学Vim，原因主要有两点：

* 最近工作中，测试的嵌入式系统主要跑在Linux上。虽是我厂定制版本，也遵守[POSIX](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/vi.html)规范，自带了vi编辑器(Emacs想都别想)。通常遇到一些需要直接编辑的文件，不熟悉vi很让人着急。这时Emacs用得再熟也白搭；
* 很多工具如Android Studio等都自定义快捷键的preference，通常会提供成套的Vim快捷键设置，很少有工具会再提供Emacs快捷键适配。更不要提Firefox上的[Vimperator](http://www.vimperator.org/vimperator)和Chrome上的[Vimium](https://chrome.google.com/webstore/detail/vimium/dbepggeogbaibhgnhhndojpepiihcmeb?hl=en)，这些在非编辑器工具上实现类Vim操作的神插件了。

Vi/Vim给我的感觉就像Linux上的Notepad之于Windows一样，built-in且轻量(no offense，Vim当然比Notepad强大太多！)。随用随开，用完即关，非常轻便。Emacs由于各种定制的插件载入，在启动速度和体量上都比Vim要慢和重。因此我更倾向于开了Emacs后就一直打开并常驻内存直至关机，而且会想尽办法把所有事情都在Emacs中处理掉，比如org-mode和eshell等。而Vim基本上只用于编辑。从这个意义上说，Vim可能更遵循[Unix philosophy](http://en.wikipedia.org/wiki/Unix_philosophy):

> Do one thing and do it well.