---
layout: post
title: "Chinese Input on Arch Linux"
date: 2014-10-29 7:00
comments: true
categories: Archlinux
---

Linux下的输入法，有几种主流的frameworks，[IBus](https://code.google.com/p/ibus/)，[fcitx](https://fcitx-im.org/wiki/Fcitx)和[SCIM](http://sourceforge.net/projects/scim/)等。基于这几种框架，又有数种输入法可供选择。看起来种类繁多，但实际试用后能满意的却寥寥。以下是我在Arch Linux上切换各种中文输入法的一点经历。

注，本人习惯使用简体中文全拼输入法，Arch Linux桌面环境为LXDE。在Windows上大部分时间使用搜狗输入法。

<!--more--> 

最初安装Arch Linux时，循着安装手册安装了ibus-pinyin。丑是丑了点，好歹能用。头两年某天常规地`sudo pacman -Syu`，升级了系统和IBus后，ibus-pinyin忽然就不能工作。据Arch Linux wiki的[IBus词条](https://wiki.archlinux.org/index.php/IBus#Input_method_engines)说，是ibus-pinyin不再维护了：

> Package currently not maintained and partly broken with latest ibus base.

转而使用页面上推荐的ibus-libpinyin，倒是能启动并使用。问题是响应速度太慢了，常常一句话打得稍快点就漏字，很不爽。将就使用一段时间，实在忍不了，继续寻找适合的输入法。过程中也试用过ibus-sunpinyin和ibus-cloud-pinyin，都因各种原因放弃。

正好这个时候，[发现](http://blog.felixc.at/2014/04/sogou-pinyin-for-linux-new-release/)Windows上常用的搜狗拼音出[Linux版本](http://pinyin.sogou.com/linux/)了。觊觎搜狗的词库，就顺便从IBus阵营切换到fcitx阵营。词库是丰富了，无奈搜狗继承了大公司Linux产品都是后妈养的这个优良传统（参见[Linux QQ](http://im.qq.com/qq/linux/)的境遇），活脱脱一个半成品。自启动除了fcitx本身的自启，将`/etc/xdg/autostart/fcitx-autostart.desktop`拷贝至`~/.config/autostart/`，还需要启动面板程序*qimpanel*。在自启文件里（我的机器上是`~/.config/lxsession/LXDE/autostart`），加上:

    @sogou-qimpanel

这样还有问题，左下角经常有个小黑框挡着，不影响使用，但影响心情啊。放狗[搜出来](http://askubuntu.com/questions/451095/lubuntu-14-04-and-fcitx-qimpanel-how-to-remove-this-black-square)，可以通过安装`compton`解决：

1. Install compton from AUR;
2. create `~/.compton.conf` according to [this post](http://ubuntuforums.org/showthread.php?t=2144468);
3. modify `shadow = false`;
4. in `~/.config/lxsession/LXDE/autostart`, add ”@compton”

可即使是这样，还是经常出问题，面板经常无法正常自启，动不动就提示“搜狗输入法面板无法启动”，需要手工启动`sougou-qimpanel`。而且词汇记忆能力极弱，我平时输入中使用`在`多于`再`，可无论我重选多少次。每次当我键入`zai`时，出现在首词的永远是`再`。

愤而转向“[中州韵输入法](https://code.google.com/p/rimeime/)”，也就是Mac上有名的“鼠须管输入法”，Windows上称作“小狼毫输入法”。安装非常简单，配置是纯文本形式，非常好。使用了几天，暂时还在慢慢摸索中，未出现各种奇怪的问题。而且基于用户习惯积累词汇功能很强大，基本上输入过一两次的词组，后面就会优先跳出来。慢慢积累，就会越用越顺手。现在Windows上的搜狗输入法也被我卸载，换成“小狼毫”了 :lol:

以上通过中州韵输入法“明月拼音”输入。


