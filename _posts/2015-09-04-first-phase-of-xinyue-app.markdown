---
layout: post
title: "First Phase of Xinyue App"
date: 2015-09-03 22:44
comments: true
categories: Android
---

新月App第一期的工作差不多完成了。有几个TODO还没完成，不过暂时不影响基本使用。

<!--more-->

比如：

* Product detail页面是用TextView混排文字和图片，导致灵活性不够，图片暂时无法点击放大；
* Search功能未加入，WP API插件是已经提供了搜索的接口，想想应该不难，在现有的代码上增加点功能就可实现；
* Design部分稀烂，比如配色，DrawerLayout各元素不完全符合Material Design规范，产品列表和详情页的版式等，是大有可提升的空间；
* ListView要替换成现在更流行的RecyclerView；
* 分享功能太简陋，比如微信朋友圈的分享功能没实现，不想用腾讯或第三方的SDK去做；
* 某些用户体验部分还有待提升，比如产品列表底部的loadMore最好做成自动载入等；
* 对Android不同版本和不同size屏幕的适配工作；

现在的app界面暂时如下所示：

![home](https://dl.dropboxusercontent.com/u/6459697/blogimage/20150903_xinyue_home.png)

![drawer](https://dl.dropboxusercontent.com/u/6459697/blogimage/20150903_xinyue_drawer.png)

![detail](https://dl.dropboxusercontent.com/u/6459697/blogimage/20150903_xinyue_detail.png)

![settings](https://dl.dropboxusercontent.com/u/6459697/blogimage/20150903_xinyue_settings.png)

![about](https://dl.dropboxusercontent.com/u/6459697/blogimage/20150903_xinyue_about.png)

接下来的工作，主要是想写Unit Testing cases，然后做refactoring. 前面提到的TODOS最好也能一并做了。如果时间不允许，就暂缓。重点还是想学学Android的UT，以及实践一下重构。



