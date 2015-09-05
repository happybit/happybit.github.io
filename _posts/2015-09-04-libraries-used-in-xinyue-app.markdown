---
layout: post
title: "Libraries used in Xinyue App"
date: 2015-09-04 22:04
comments: true
categories: Android
---

在制作第一款App Conn时，使用了不少三方库，比如Floating Action Button和Navigation Drawer等。因为那时Google虽已正式提出[Material Design](http://www.google.com/design/spec/material-design/introduction.html)，介绍了不少新颖的设计方案。但并未适时推出配套库，因此涌现出大量三方库来支持此类需求。

<!--more-->

题外话，作为developer，你完全可以不遵守Material Design。比如以小米的[MIUI](http://www.miui.com)和魅族[Flyme](http://www.flyme.cn/)为首的iOS向，还有锤子Smartisan为代表的前iOS向。基本上都是长了颗Android的心，却又向往iOS的长相，因此大刀阔斧地进行了整容。这里就不提其他大量如华为[EMUI](http://www.emui.com/)、联想[VIBE UI](http://www.vibeui.com/vibeui/index#!/index)、中兴等各家整残的ROM了。

还有以微信为首，tab放在bottom的那些apps，几乎全未遵守Material Design的设计规范。说的就是你们，支付宝和豆瓣，学谁不好...

其实对很多无设计经验的developers来说，Material Design的出现，绝对是好事。它保证了设计的底线和统一的用户体验，按它的来起码不会丑到哭。因此在整个开发设计过程中，我也希望能尽量遵守Material Design规范。

今年Google推出[Android Design Support Library](http://android-developers.blogspot.jp/2015/05/android-design-support-library.html)成功解救了我们。FAB等功能或效果都可使用support lib来实现了。因此在Xinyue App中，能使用官方库的，我都会用官方的support-v4和design support库去实现。如下：

* [DrawerLayout](https://developer.android.com/intl/zh-cn/reference/android/support/v4/widget/DrawerLayout.html);
* [TabLayout](https://developer.android.com/intl/zh-cn/reference/android/support/design/widget/TabLayout.html);
* [Toolbar](https://developer.android.com/intl/zh-cn/reference/android/widget/Toolbar.html);
* [SwipeRefreshLayout](https://developer.android.com/intl/zh-cn/reference/android/widget/Toolbar.html);

官方库也不是没有坑，比如在support-v4:22.2.1中，tab可能会无故消失。这个问题在[论坛](https://code.google.com/p/android/issues/detail?id=180462)里吵翻了，据说在23版本里仍然未解决。我暂时使用的是[17楼](https://code.google.com/p/android/issues/detail?id=180462#c17)提供的work-around，并不完美。

同时，另一些重要的功能，如在右滑退出等，Google仍未提供官方库支持。因此，还是不可避免的需要使用一些三方库。在Xinyue App中，我主要使用了：

* [Volley](https://developer.android.com/intl/zh-cn/training/volley/index.html)：Google出品，用于网络请求；
* [Universal Image Loader](https://github.com/nostra13/Android-Universal-Image-Loader)：用于请求和加载image;
* [Gson](https://github.com/google/gson)：同样来自Google，快捷方便地解析JSON格式;
* [SwipeBackLayout](https://github.com/yrom/SwipeBackLayout)：用于滑动退出；
* [SwipeRefreshLayout](https://github.com/Demievil/SwipeRefreshLayout)：用于上拉加载；
* [PreferenceFragment](https://gist.github.com/cbeyls/7475726)：官方的PreferenceFragment不支持support-v4中的fragment，这个第三方的可以；
