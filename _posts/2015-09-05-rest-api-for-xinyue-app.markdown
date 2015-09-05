---
layout: post
title: "REST API for Xinyue App"
date: 2015-09-05 20:32
comments: true
categories: Android
---

下面我将按照当初从一个idea到最终开发出一个app的过程，讲述一下其中遇到和解决的一些问题。首先是网站，即server端的，接口问题。

<!--more-->

最初，仅仅只是起意想为“[新月](http://www.xinyue.in)”网站做一枚配套的Android App。可心里着实没底，虽然有了[Conn](http://conn.pzheng.me)的一点点经验，仍然不知道如何下手。模模糊糊有个概念，是客户端需要去retrieve网站上的信息，然后展现在手机上。

首先遇到的问题，就是需要一个接口，让客户端能获取网站信息。[新月](http://www.xinyue.in)网站是用Wordpress搭建的，是否有合适的插件实现接口的功能呢？如果没有，自己再做一个接口的程序，开发难度无疑将大大增加。本着Just Get It Work的原则，有现成的就不去再造轮子。先做了一些前期调查，了解到现在最流行的是RESTful API和SOAP等。REST相对来说更流行。在此之前，我可是对RESTful一窍不通。没过几个月，在学习Cloud资料的过程中，发现我们的产品中也应用到了REST（这不，你学的任何东西都不会白费，是吧？）。

快速地选定REST类型的API之后，立即搜索Wordpress的插件库。没让我失望，好几款plugins都可以让Wordpress的网站瞬间拥有REST API。搜了一下网上的评论和各插件的文档，没费多少功夫，就选定了[WP REST API V2](http://v2.wp-api.org/).

安装之后当然是试用了。官方文档里说，要获取网站的posts，直接GET网站的`/wp-json/wp/v2/posts`即可。但是，无论我在Chrome浏览器的Advanced Rest Client中，如何尝试去GET这个路径，都提示出错，返回的message是"No route was found matching the URL and request method"。明显路径不对(一定是我打开的方式有问题...)。后来无意中，用这个路径`/wp-json/posts`打开，发现竟然可以。啊哈，这感觉就像在黑暗的山洞里前行，终于看到前方貌似有一丝光亮了。

因此，所有的接口route都基于这个网址来request的：

    http://www.yourwebsite.com/wp-json/posts

App的前期开发（ContentProvider的实现），都是基于上面这个网址去实现的。到中后期，发现问题了：

1. 该网址只返回最近的10篇帖子，10篇以前的posts该如何获取？
2. 在app的tab中，是以首饰的种类做区分的，如何通过REST API获取特定category的posts?
3. 如何实现搜索？有相应的API吗？

查看了[官方文档](http://wp-api.org/#posts_retrieve-posts)后，发现有filter可以使用。而filter的参数，可以通过Wordpress的[开发文档](http://codex.wordpress.org/Class_Reference/WP_Query#Category_Parameters)查看。调试了几遍，摸清了门路，用下面这个网址，即可获取到earrings这个类目下的第一页所有posts。注意，你可以先通过前面的方式，查看每个post的结构，找出你想要过滤的字段对应的是什么参数。比如，新月网站中的类目实际上就是Category中的slug字段，通过Wordpress的[开发文档](http://codex.wordpress.org/Class_Reference/WP_Query#Category_Parameters)找到对应的参数，就是category_name.

    http://www.yourwebsite.com/wp-json/posts/?filter[category_name]=earrings&page=1

而对于搜索，可以使用下面的scheme，来搜索所有包含"rings"字符串的posts。非常方便。（search功能在app中暂未提供）

    http://www.yourwebsite.com/wp-json/posts/?filter[s]=rings

Server端的API接口搞定了，接下来是app中最重要的ContentProvider部分了。事实上，这部分也是我花时间最多的地方。