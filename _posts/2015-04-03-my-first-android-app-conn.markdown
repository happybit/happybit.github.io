---
layout: post
title: "My First Android App Conn"
date: 2015-04-03 20:22
comments: true
categories: Android
---

终于我的第一个[Android app](http://conn.pzheng.me)出炉了，拖得太久了。本来去年底开始自学Android开发时，就已经把雏形做出来了，基本功能完成，并一直在使用。但是“能用”和“好用”之间，还需填补大量完善的功夫。前几个月因其他事务太多，一度停止。最近又捡起来，熬了几个夜总算弄出一个“可用”的[版本](https://dl.dropboxusercontent.com/u/6459697/app/Conn/Conn_v1.0.0.apk)。欢迎尝鲜！

<!--more-->

最初起意学Android开发，也是基于自己的需求。由于鄙司可怜又可笑的自尊，谨遵"eat your own dog ~~shit~~food"原则，不允许友商的基站凌驾于自己头顶。运营商也乐得不用网优和维护，于是我们在一片友商基站的包围下成了孤岛。不仅所辖小区未被加入邻小区的active set，无法进行softer handover，导致进出公司电话必断。而且大楼内数据连接异常不稳定，上网一段时间后自动断线或陷入“僵尸网络”症状--数据显示是连接的，死活就是上不了网。大家给出的tips无外乎频繁关闭/开启“飞行模式”或“数据连接”。

即使现在Android已可通过status bar的快捷按钮，快速地进行“数据连接”的操作，仍嫌繁琐。且不说每次“下拉状态栏--点击关闭数据连接--下拉状态栏--点击开启数据连接”，一轮未连上，再来一轮，狼狈得狠。就是每次手机制造商看似贴心的小提示(如下图所示)，还要再多耗费一次点击，也着实x疼。

![dialog](https://dl.dropboxusercontent.com/u/6459697/blogimage/20150403_conn_dialog.jpg)

这个app的核心功能很简单，就是点击一次，会尝试自动连接网络，如接入失败，会自动重连，直至成功。其实只用制作一个widget button就可以的事，我还是制作了一个MainActivity，有overdevelopment之嫌。主要也是抱着学习的目的玩一玩各种功能。从核心功能实现，到界面完善，到确定名称为**Conn**和logo（好啦知道两个都很逊只花半个下午就定稿了），最后签名发布，并利用[GitHub Pages](https://pages.github.com/)制作[应用专属页面](http://conn.pzheng.me/)。除了没上传Google Play Store，也算硬着头皮走完了一个简单的流程。

整个app制作过程中，大致使用了(四大组件除了ContentProvider其他都用到了)：

* Activity;
* Fragment;
* Intent;
* Service;
* AsyncTask;
* AppWidgetProvider/BroadcastReciever;
* SharedPreference;
* PreferenceFragment;
* NavigationDrawer;
* FloatingActionButton;

其中，[NavigationDrawer](https://github.com/kanytu/android-material-drawer-template)和[FloatingActionButton](https://github.com/makovkastar/FloatingActionButton)使用了开源代码，大大加速了开发进程。后续几篇posts，我会将开发中遇到的问题汇总，陆续贴出来，算是入门的经验。

关于软件的使用，请参看[应用页面](http://conn.pzheng.me/)，代码也放在[GitHub](https://github.com/happybit/Conn)上了。

对了，我没学过Java，所有代码都是看[官方training](http://developer.android.com/training/index.html)和[API文档](http://developer.android.com/guide/index.html)，还有[Google](http://www.google.com)/[GitHub](http://www.github.com)/[StackOverflow](http://www.stackoverflow.com)上搜到，拼凑起来的（all honor belongs to them）。写得不合规范的地方，请多指教，万谢。
