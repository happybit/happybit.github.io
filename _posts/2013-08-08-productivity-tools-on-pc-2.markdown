---
layout: post
title: "Productivity Tools on PC (2)"
date: 2013-08-08 05:59
comments: true
categories: Productivity
---

Eight frequently-used tools were listed in [preview post](http://blog.pzheng.info/blog/2013/07/30/productivity-tools-on-pc-1/). Some of them are so handy that you could use them directly  without any customization. I will introduce first two tools in this single post. 

<!--more-->

# Everyting

_Everything_ is the most convenient search tool on PC.  I configured the following two points according to my own habits and started using it. Honestly, you don't need to follow but just try it. I bet you're gonna love it!

[++Download++](http://www.voidtools.com/download.php) 

## Hot Key Setting

I'd like to use `Alt + F1` to call out _Everything_ from system tray. So I change these two values in `Tools --> Options --> General`:

* New window Hotkey Modifier: `Alt` 
* New window Hotkey Modifier: `VK_F1`

{% img /images/everything_hotkey.png %}

What? You need hot key to minimize it back to system tray? I bet you could try `Alt + F4` :-P

## Hide Empty

As a fake minimalist, I'd like empty appearance when there is nothing in search bar, rather than bunch of non-sense files showing up. I just need to pick `Hide results when the search is empty` in `Tools --> Options --> View`.

{% img /images/everything_hide_empty.png %}

# Launchy

_Launchy_, a quick launcher, is another small tool which will improve your quality of experience on PC. I can get rid of the quick launch bar and all nasty shortcuts on my destop.

Actually _Launchy_ could be replaced by _Everything_ to some extent. But I still keep both of them. Why not let them do their own jobs?

[++Download++](http://www.launchy.net/download.php)

The first thing when I use _Launchy_ is changing default skin to _Spotlight Wide_ :-)

## Scan Catalog

Firstly you need to rescan your program files folders, especially if you are more interested in portable programs. Since the default catalog only contains `start menu` directory and `Program Files` directory.

Go to `Options --> Catalog`, add certain directories. Don't forget to add file type, e.g. `.exe` or `.lnk`, as well as option for sub-directories. Then click `Rescan Catalog`.

{% img /images/launchy_settings.png %}

## Plugins

As you may know, _Launchy_ is able to calculate, search web etc, which I don't use frequently. 

But one plugin I use almost every day is `Runner`. Because portable _DokuWiki_ (_DokuWikiStick_), one of my indispensible tools I'd like to introduce later, needs to run mini _Apache_ engine locally (Please note, this is the first time two tools connect. There will be more in later posts.). I have to click `mapache.exe` whenever PC rebooting to start _Apache_.

So I just go to `Options --> Plugins` and add those executable files into `Runner` as the following screenshot. You could run other similar programs as well.

{% img /images/launchy_plugin.png %}


