---
layout: post
title: "Learn Vim The Hard Way II"
date: 2015-02-23 21:50
comments: true
categories: Productivity
---

[前文](http://blog.pzheng.me/2015/02/22/learn-vim-the-hard-way-i/)提到个人学Vim的一些背景和动机。本文将介绍一下自己学习Vim的方法。

<!--more-->

一直以来，我学习的方法都是尽量快速入门，并在练习中熟练基本操作，然后在日积月累的日常使用中去精进和进阶学习。这种学习方法是遵循[Pareto principle](http://en.wikipedia.org/wiki/Pareto_principle)而来。我的理解是，对于某项技能，只用掌握20%就可以应付生活或工作中80%的需求。因此，快速掌握了这20%后，就能以此为基础去探索剩下的80%，成为真正的专家。这样才不会因为开始就举步维艰而中途放弃。之前学习Vim每每放弃的原因，也就在于未能掌握这最开始的20%。

然而如网上流传的各种editors的learning curve图来看，Vim和Emacs都是最为诡异的。其中Vim是以学习曲线陡峭著称，也就是说这前20%是最难学的。

![Editors Learning Curve](https://dl.dropboxusercontent.com/u/6459697/blogimage/20150223_editors_learning_curve.jpg)
[[Source](http://www.quora.com/How-accurate-do-you-think-these-text-editor-learning-curves-are)]

个人在学习Vim时。遇到的最大困难是经常和Emacs的快捷键记混。使用Emacs几年后，一些基本操作的快捷键已形成肌肉记忆，编辑时左手小拇指会不自觉地想去按键盘左下角的Ctrl键。只要抑制住按Ctrl键的冲动，就可以说迈出了成功的第一步。剩下的，就是"背"了。

这里就要祭出利器了--[Anki](http://ankisrs.net/)。这是一个遵循遗忘曲线的卡片式辅助记忆工具（好几年前学习Perl时，也做过一个类似的命令行工具，用来记单词的，当然不能和这个相比啦:blush:）。这个工具强大之处在于全平台支持，支持各种操作系统如Windows，Linux，Mac，[Android](https://play.google.com/store/apps/details?id=com.ichi2.anki)，[iOS](https://itunes.apple.com/us/app/ankimobile-flashcards/id373493387?mt=8&ign-mpt=uo%3D4)等。如不想使用app，还支持[web](https://ankiweb.net/)界面，无比贴心。其中Android版本免费，而iOS版本人民币163元（作者知道Android用户购买力没iOS用户强么？:sunglasses:）。

[AnkiWeb]((https://ankiweb.net/))上有很多共享的decks，可直接下载使用。如有特殊需求，也可自制deck和cards。我选择的shared deck是[Vim Commands](https://ankiweb.net/shared/info/3803780219). 其中共有239张卡片，对应239个Vim命令（有些非常用或暂时用不上的可在学习过程中hide起来）。

我用的是Android版本[AnkiDroid Flashcards]((https://play.google.com/store/apps/details?id=com.ichi2.anki))，非常直观，上手就能使用。而且有各种统计值辅助了解学习进度。我直接使用默认设置，也就是每天学习20张新卡片。别小看这20张卡片。因为之前学过的卡片，会在遗忘期限到达之前，加入到复习列队里，所以学过一段时间后，每天新增的和复习的卡片加起来会有100多张。

通常我都是在每天通勤时，掏出手机翻那些卡片学习，到公司之后，把刚才觉得比较难的命令，在电脑上操作一下，加深记忆就ok了。除掉周末，三周时间就可以将整个deck全部过一遍。再加几周反复巩固，大部分常用命令就都不在话下了。