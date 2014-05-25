---
layout: post
title: "Build home backup system"
date: 2014-02-24 20:28
comments: true
categories: Archlinux
---

I never seriously consider photoes as precious wealth till one day I drowned into my album collections. Those silly and embarrassed moments instantly became vivid. In order to backup and organize all my family's pictures at one place, I decide to build up a system on my out-of-date netbook since I don't want to spare money on an expensive NAS machine.

<!--more-->

## Backup folders from Android/iOS automatically

First of all, I need sync the pictures from all of my family phones and tablet. [BitTorrent Sync](http://www.bittorrent.com/sync) is good choice because it covers almost all platforms, Windows/Linux/Android/iOS, etc. And it's FREE.

* Follow [this wiki entry](https://wiki.archlinux.org/index.php/BitTorrent_Sync), I can easily set up BT Sync on my netbook running Archlinux. And run `systemctl status btsync@user` to check the status;
* Install *BT Sync* on all phones and iPad;
* Choose camera folders and set them as backup folders;
* Add backup folders on PC with secret codes;

Now all the pictures will be uploaded to the specific folders on PC and new photoes will be synchronized later as well. And If *BT Sync* drains the phones' battery, you could try to enable "Auto Sleep".

The only constraint is, I have to keep *BT Sync* opening on iPad during synchronization. But I can bear it since I seldom take pictures on iPad.

## Set sharing folders on Archlinux

NFS ([Network File System](https://wiki.archlinux.org/index.php/Nfs)) is the my first choice to share folders on Archlinux because it's UNIX/Linux oriented and highly efficient. However I dropped it later due to the lack of decent client apps on Android/iOS.

Samba, as an alternative, was set up instead. Always following [the official wiki](https://wiki.archlinux.org/index.php/SMB) will make you waste less time on configuration or debugging.

## View Pictures on Android/iOS/TV box

[ES File Explorer](https://play.google.com/store/apps/details?id=com.estrongs.android.pop&hl=en) on Andorid and [FileExplorer](https://itunes.apple.com/us/app/fileexplorer-free/id510282524?mt=8) on iPad are able to mount SMB folders as well as browse remote pictures freely.

On TV box, [XBMC](http://xbmc.org/) is always the best choice. It could even support NFS! 

## Existed problem

The only problem I meet now is the speed. The wireless ethernet card on netbook is only 150Mbps while my TP Link router at home is also 150Mbps. I can approximately get 6Mbps transmission from another Windows PC in the same LAN. But only 2Mbps data rate could be reached on an android phone. SMB client might be the bottleneck I guess. 

I'd like to put it aside. Because I only use it to browse family photographs. Fine is just enouge. Don't let the pefectionism ruin your life!
