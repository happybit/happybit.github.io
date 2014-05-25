---
layout: post
title: "Fix Archlinux"
date: 2013-06-22 04:20
comments: true
categories: Archlinux
---


If you are an Archlinux user, you might have noticed the latest news - [Binaries move to /usr/bin requiring update intervention](https://www.archlinux.org/news/binaries-move-to-usrbin-requiring-update-intervention/). The same problem was encountered on my laptop during update:
	
	error: failed to commit transaction (conflicting files)
	filesystem: /bin exists in filesystem

Following the instruction, I just uninstalled Grub and some other programs. But accidentally hit POWER OFF button right after. No surprise I cannot login to Archlinux after reboot. Here is the procedure how I fixed it.

<!--more-->

1. Download [latest Linux ISO](https://www.archlinux.org/download/) and creat Live USB via [LinuxLive USB Creator](http://www.linuxliveusb.com/).

2. Get into Live CD mode and set up internet connect according to [Beginners' Guide](https://wiki.archlinux.org/index.php/Beginners%27_Guide).

	Here is an example of wireless connection.

	    # iw dev
	    # ip link set wlp3s0 up
	    # wifi-menu wlp3s0 

3. Check disk partitioning.

	    # lsblk /dev/sda 
	    # fdisk -l  

	On my laptop, sda 7/8/9/10 are Linux partitions.

	* sda 7: 200M boot directory
	* sda 8: 2G SWAP
	* sda 9: 4.7G root directory
	* sda 10: 28.6G home directory

4. Mount the directories respectively.

	    # mkdir /mnt/arch
	    # mount /dev/sda9 /mnt/arch
	    # mount /dev/sda7 /mnt/arch/boot/
	    # mount /dev/sdb10 /mnt/arch/home/

5. Chroot according to wikipage [Change Root](https://wiki.archlinux.org/index.php/Chroot).

	    # arch-chroot /mnt/arch

6. Use the same internet connection.

	    # cp -L /etc/resolv.conf etc/resolv.conf

7. Assign the shell.

	    # chroot . /bin/bash

8. Install syslinux.

	    # pacman -S syslinux
		# syslinux-install_update -i -a -m
		# nano /boot/syslinux/syslinux.cfg

	Change sda9 to the root directory.

	    ...
	    LABEL arch
		    ...
		    APPEND root=/dev/sda9 ro
	    	...

	To prevent below error. You still need the following steps.

	    /sbin/init does not exist 

9. Install systemd-sysvcompat.

	Find below line in '/boot/syslinux/syslinux.cfg'.

	    LINUX ../vmlinuz-linux

	Add init as:

	    LINUX ../vmlinuz-linux init=/usr/lib/systemd/systemd

10. Exit chroot.

	    # exit
		# umount /mnt/arch/

11. Reboot and now you will get into the nice bootload interface.
