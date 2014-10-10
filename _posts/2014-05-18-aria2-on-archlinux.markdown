---
layout: post
title: "Aria2 on Archlinux"
date: 2014-05-18 21:56:08 +0800
comments: true
categories: Archlinux
---

Days ago, I configured my netbook for [BitTorrent Sync](http://blog.pzheng.me/blog/2014/02/24/build-home-backup-system/). This week, I proceeded further to install [Aria2](http://aria2.sourceforge.net/) on it for the purpose of remote downloading. 

<!--more-->

1. Install Aria2 via Pacman and then create file `~/.aria2/aria2.conf`:

	    $ sudo pacman -S aria2
		$ mkdir ~/.aria2
		$ touch ~/.aria2/aria2.conf

2. Configure `~/.aria2/aria2.conf`:

        #configuration file for aria2c
        continue=true
        daemon=true
        dir=/home/YOURNAME/Pic/Download
        file-allocation=none
        input-file=/home/YOURNAME/.aria2/input.conf
        log-level=warn
        log=/home/YOURNAME/.aria2/aria2.log
        max-connection-per-server=3
        max-concurrent-downloads=3
        max-overall-download-limit=0
        max-upload-limit=128K
        #split=3
        check-integrity=true
        max-tries=5
        retry-wait=3
        min-split-size=5M
        #enable-http-pipelining=true
        enable-rpc=true
        rpc-listen-all=true
        rpc-allow-origin-all=true
        disc-cache=32M
        save-session=/home/YOURNAME/.aria2/input.conf
    
	Please notice to create `input.conf` & `aria2.log` in the same folder as `aria2.conf`. Otherwise Aria2 doesn't work properly and YAAW would report "internal server error".

3. Aria2 autostart on boot:

    Save this file as /etc/systemd/system/aria2c.service, adjust username and config path according to your setup. Ensure your config is set to deamonize (daemon=true).

        [Unit]
        Description=Aria2c download manager
        After=network.target
        
        [Service]
        Type=forking
        User=root
        RemainAfterExit=yes
        ExecStart=/usr/bin/aria2c --conf-path=/home/YOURNAME/.aria2/aria2.conf
        
        [Install]
        WantedBy=multi-user.target

    If fault reported as "code=exited, status=217/USER", please modify "User=***" to proper user, e.g. "root". 

4. Install Apache:

    Apache configuration file: `/etc/httpd/conf/httpd.conf`

	DocumentRoot: `/srv/http`

5. Install [YAAW](https://github.com/binux/yaaw) for Aria2 webfront UI. You can choose any other alternatives as you like.

	    $ cd /srv/http
	    $ git clone https://github.com/binux/yaaw
	    $  sudo systemctl start aria2c
	    $ sudo systemctl start httpd.service

6. Configure for [Thunder offline](lixian.xunlei.com) or [Baidu Yun](yun.baidu.com) download:

    - Install Tampermonkey or Greasemonkey extension for js in Chrome/Firefox;
    - Install JS script from [here](https://github.com/binux/ThunderLixianExporter);
    - On Xunlei offline download/Baidu Yun webpage, configure Aria2 JSON-RPC Path to `http://192.168.2.103:6800/jsonrpc`;
    - Install [MBL&MC extension](https://chrome.google.com/webstore/detail/mblmc%E8%BF%85%E9%9B%B7%E7%A6%BB%E7%BA%BFqq%E6%97%8B%E9%A3%8E%E7%99%BE%E5%BA%A6%E7%BD%91%E7%9B%98360%E4%BA%91%E7%9B%98%E7%AD%89ar/iamaphkapjbdhhpdapkalhanifedeged) in chrome;
	- There will be "YAAW" or "Aria2c for RPC" option on Xunlei offline download/Baidu Yun webpage;

Now you can download files on PC or even [cellphone](https://play.google.com/store/apps/details?id=com.paranoia.remotearia2) remotely in the same LAN. I tried it on both [Xunlei](www.xunlei.com) and [Baidu Yun](yun.baidu.com). It works like a charm! Or you can even configure Dynamic DNS to remotely monitor and download files. Cool.

Tips for "internal server error":

* Aria2 doesn't run as daemon. Check the process firstly;
* JSON-RPC path is incorrect on client(PC/cellphone);
* `rpc-secret` or `rpc-user/password` is in use but it isn't configured in JSON-RPC path;

If Aria2 stops automatically within several seconds after downloading without completion, you might need to tweak your `.aria2.conf` file. Some websites limit the maximum simultaneous connections. So I set "max-connection-per-server=3" and it works.
