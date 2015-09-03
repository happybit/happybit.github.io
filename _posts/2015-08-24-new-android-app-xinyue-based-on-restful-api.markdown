---
layout: post
title: "New Android App Xinyue Based on RESTful API"
date: 2015-08-24 09:26
comments: true
categories: Android
---

做完第一个Android小应用[Conn](http://blog.pzheng.me/2015/04/03/my-first-android-app-conn/)后，一直跃跃欲试想再做一款应用练练手。毕竟脑子里的idea还挺多的，而用工程驱动的方式去学习，也不失乐趣。

<!--more-->

### Java Self-learning

不过在上个项目中，遇到很多关于Java基础知识不清晰的地方，比如抽象类，匿名类等。基本都是靠代码拼贴，还有联想及试错的方式整出来的。所以，想在制作第二款App之前，能稍微巩固一下Java相关的基础。基于此，就学习了University of Helsinki的[在线课程](http://mooc.fi/english.html)Object-Oriented programming with Java [part 1](http://mooc.fi/courses/2013/programming-part-1/) & [part II](http://mooc.fi/courses/2013/programming-part-2/)。不得不说，这套课程设置得很棒，是学习Java入门非常好的材料。具体体现在：

1. 配套的IDE是开源的Netbeans，学校还制作了课程插件，可上传课后作业的代码和计分。关键是windows/Linux/Mac全平台适用，太用心了（尤其是Linux，很多软件声称适配Linux，但其实只支持某些发行版。而这套Netbeans+插件，在家里的Arch Linux上跑毫无问题，大赞。）；
2. 每个课后作业都有一套完整的UT代码，通过UT测试来计算是否pass和算分。同时，你只能在pass之后才能看得到参考答案；
3. 内容说起来算是很浅显的，因此仅适用于入门。不过有几题是没有提示，完全靠自己freestyle的构造整个工程，也需要花点时间；
4. 如果有什么不懂的地方，可以上IRC chat去咨询，反馈及时也挺热情的。

### Server side API

把课后习题全都做完一遍，语法方面的障碍基本扫清。就开始着手做App了，最先想到的就是，希望为[之前搭建](http://blog.pzheng.me/2014/06/01/promotion-independent-designer/)的网站“[新月](http://www.xinyue.in)”，制作一枚Android客户端。想要完成客户端对服务器的接入，必定要经过API接口。经过前期调研，决定选广泛采用的RESTful API。WordPress有成熟的[WP REST API插件](http://wp-api.org/)使用。安装并激活插件后，就可以通过下面形式的网址来get JSON格式的response了。

    GET http://www.xinyue.in/wp-json/posts

Chrome里有Advanced REST client和Postman等多款插件，可在浏览器里debug RESTful API，很顺手。

### Client side architecture

服务器端的问题解决了。接下来就是客户端如何实现了。Google早在2010年的开发者大会上，就提出了几种推荐的RESTful client的解决方案。视频在[YouTube](https://www.youtube.com/watch?v=xHXn3Kg2IQE)上有，slides材料在[这里](https://dl.google.com/googleio/2010/android-developing-RESTful-android-apps.pdf)。最终选用的是Option B方案。

![use contentprovider api](https://dl.dropboxusercontent.com/u/6459697/blogimage/20150824_restful_client_use_contentprovider_api.png)

### Reference

期间，主要参考的资料是：

* [Programming Android](http://shop.oreilly.com/product/0636920010364.do)的Part III. A Skeleton Application for Android。这本书于2011年出版，太老了。Demo里使用的YouTube API早换了不知多少轮了，所以请注意代码下下来，是没法直接运行的。据悉，该书第二个版本将于今年年底发行；
* [9GAG REST Client](https://github.com/stormzhang/9GAG). 用了大量第三方库;
* [Android SQLite database and content provider - Tutorial](http://www.vogella.com/tutorials/AndroidSQLite/article.html). 主要是参考学习ContentProvider的；

就像下面这幅[漫画](http://oktop.tumblr.com/post/15352780846)(by Van Oktop)画的一样，看了那么多书和代码，还是不会写啊。

![how to draw a horse](https://dl.dropboxusercontent.com/u/6459697/blogimage/20150824_how_to_draw_a_horse.jpg)

### Source code

最后还是抽空余时间，慢慢磨，写了个大致的框架出来。核心其实就是实现Google提出的Option B里，用ContentProvider API来异步获取网络信息。这个实现了，后面的基本就都是小修补和User Experience上的改善了。

代码放在[GitHub](https://github.com/happybit/Xinyue)上了，现在还是非常初级的版本，远未达到release的标准。后续我会接着提交改动来完善它。初步在Android 4.1.2和5.0.1两个版本上跑通了，偶有force close的crash问题，正在debug中(时间不够用啊）。




