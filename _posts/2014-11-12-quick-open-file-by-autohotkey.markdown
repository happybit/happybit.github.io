---
layout: post
title: "Quick Open File by AutoHotKey"
date: 2014-11-12 12:31
comments: true
categories: Productivity
---

以前我们的测试工作大部分是基于脚本的，所用语言是公司自创的一套简单语法逻辑。

<!--more-->

通常每个case都会有一个主脚本，所有测试步骤就在这个脚本里实现。这个主脚本会引用许多公共库里的子脚本，让测试人员快速方便地实现一些子模块功能。在引用这些子脚本时，使用的既不算绝对路径，也不能完全算相对路径。而是如下所示这种参数引用式的路径，文件路径的部分或全部可以用str代替。

    run [CommonLibraryPath]\subdir\common_script.txt

而CommonLibraryPath这个str参数的定义，存在与case主脚本同目录下一个名为`paramus.txt`的文件里。

    PARAM str,$CommonLibraryPath,"C:\Common_Library\"

这样做的好处是公共库的location可以随意变换，而不用动case本身。这在一个case应用于多个branch的release下是非常有用的，比如现在trunk的库是`C:\Common_Library\\`,还有另一个branch的库是`C:\Common_Library_branch\\`。case会同时在这两个库里运行，只需对`params.txt`进行集中替换即可，毋需改动主脚本，减少因此可能出错的机率。

但这样随之带来的一个坏处，就是在我们平时编辑脚本的编辑器UltraEdit中，无法快速的打开相应的公共脚本。UltraEdit有一个方便的功能，如果是绝对路径，它可以方便的识别出来，然后在相应行右键即可直接打开该文件。可如果是我们这种引用式的路径，UltraEdit就无能为力了。因为它无法识别参数对应的绝对路径。

几年前我用AutoHotKey实现了可以快速打开这种路径文件的方法。去年重构了一下，简单做了个界面[^1]，只用填`params.txt`和编辑器的路径，就可以方便的操作。

![Quick Open](https://dl.dropboxusercontent.com/u/6459697/blogimage/20141112_quick_open.png)

具体操作方法是：

1. 在QuickOpen中设置好params.txt和编辑器的路径[^2]；
2. 将鼠标置于想打开的文件那一行；
3. 同时按下"Alt"+"O"键，相应的文件就会在编辑器中自动打开；

AHK脚本已上传[GitHub](https://github.com/happybit/playground/blob/master/20141112_QuickOpen.ahk)。

----
[^1]: 借助了[SmartGUI Creator](http://www.autohotkey.com/board/topic/738-smartgui-creator/)，实话实说，AHK不是一个好的语言，生成界面更不友好。执行点简单的操作还行，稍大点的任务所需的effort，和其他如Python等脚本语言相比，就相当不划算了。这只能算是前几年刚接触AHK时自己感兴趣做的小实验而已；
[^2]: 具体params.txt可以是任何文件名，但参数定义的格式需如上例所示相同。Uedit32.exe也可是任意编辑器。
