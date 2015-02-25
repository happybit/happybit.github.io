---
layout: post
title: "Learn Vim The Hard Way III"
date: 2015-02-25 08:25
comments: true
categories: Productivity
---

光背命令还不够，最好了解一下背景，以及和其他editor的差异，就能更好的理解Vim。

<!--more-->

常将[Vi](http://en.wikipedia.org/wiki/Vi)和[Vim](http://www.vim.org/index.php)混为一谈，貌似一样。其实有区别，但区别也很简单。Vi是Unix上的一款编辑器，最初是[Bill Joy](http://en.wikipedia.org/wiki/Bill_Joy)(Sun公司的联合创始人之一)于1976年写的。Vim是**V**i **IM**proved的缩写，顾名思义你可以将它看作Vi的增强版(Vim并没有完全兼容Vi)。由荷兰人[Bram Moolenaar](http://www.moolenaar.net/)(现任职Google)于1991年写出来的。你可以在terminal中使用Vim，也可以有单独的GUI application，比如在Windows下常用的[gVim](ftp://ftp.vim.org/pub/vim/pc/gvim74.exe).

和Emacs类似，由于早期的键盘无方向键也没有鼠标，因此操作都需要用快捷键实现。这也让尽可能多的键盘操作，在主键盘范围内，也就是左右手自然放在键盘上，那片区域内。而不需要频繁移动到键盘其他位置，效率自然高了。在Emacs中，为了区分真正的input和快捷键，通常用功能键`Ctrl`来组合各种操作的快捷键，比如前进`Ctrl-F`(orward)和后退`Ctrl-B`(ack)。而在Vim中，前进后退的快捷键分别是`j`和`k`，右手食指和中指落在键盘上的两个键。宗旨也就是越频繁的键要在越方便的位置。但是由于没有功能键的辅助，编辑器无法区分当前是真的想输入"j/k"还是方向操作。因此Vim最重要的一个概念就是normal mode和insert mode，默认进入文件是normal mode，可以使用各种快捷键移动或操作，通常键入`i`进入insert mode，按`Esc`键退出insert mode进入normal mode。据说高手使用Vim时只有normal mode。击键效率上来说，肯定是Vim取胜。不过用惯了Emacs，倒也不觉得常按`Ctrl`键有什么不适。

和Emacs完全定制成自己喜欢的方式不同，Vim我暂时未加其他插件，除了基本设置了一下ignorecase/autoindent/hlsearch等，也没有太多定制（主要也是不熟vimscript)。其中一个原因是，希望能像原教旨派那样享受纯粹的击键快感。更重要的原因是，很多操作未必是在本地，比如SSH到服务器上，太多定制可能反而导致记不住默认的设置。

相较于Emacs，Vim的快捷键看起来更强大。这种强大体现在快捷键的组合上。Emacs的快捷键之间相对独立，如果想要实现一个连起来的操作，就需要重新定义一个key binding。而Vim上移动和操作的快捷键可以组合，比如删除是`d`，移动至行末是`$`。可以在normal mode直接键入`d$`就是删除至行尾。甚至可以加入数字，比如`dw`是删除一个单词，`d3w`就是删除三个单词。如果任性定制自己喜欢的快捷键，反而可能丢失了这些组合功能。因此也没有太多必要去customize和redirect已有的key binding。


