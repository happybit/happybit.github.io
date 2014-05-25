---
layout: post
title: "Migrating from Octopress to Jekyll"
date: 2014-05-25 19:17:08 +0800
comments: true
categories: Others
---

Just remind you, this site has been migrated from [Octopress](http://octopress.org) to [Jekyll](http://jekyllrb.com). The theme was cloned from [Lanyon](http://lanyon.getpoole.com/) and I tweaked it a bit.

<!--more-->

Honestly, Octopress is so far so good as a blog framework. It's simple and static. And it supports markdown syntax naturally without needing any dedicated webhost, since it could be hosted on [GitHub](http://github.com). However, the biggest problem to me is, the whole site needs to be deloyed **locally** whenever I am going to post new article, which mean I can hardly publish posts conveniently on the other computer except my home PC. 

After searching around, I found Jekyll, as the basic framework of Octopress, could be easily depoyed on GitHub as well(so it's extremely easy for migration). Thus it's also simple and static. Even better than Octopress in terms of simplicity.

For instance, there is only one `master` branch for Jekyll and the structure of folders is simple as below:


    ├── 404.html
    ├── about.md
    ├── archive.html
    ├── atom.xml
    ├── CNAME
    ├── _config.yml
    ├── _includes
    ├── index.html
    ├── _layouts
    ├── LICENSE.md
    ├── _posts
    ├── public
    └── README.md

Besides, I could write and publish posts almost anywhere via:

* [Prose.io](http://prose.io) on web;
* [GitHub](https://play.google.com/store/apps/details?id=com.github.mobile) or [Jekyll](https://play.google.com/store/apps/details?id=gr.tsagi.jekyllforandroid) apps on Android; 

