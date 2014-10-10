---
layout: post
title: "Model-Based Testing"
date: 2014-07-20 09:58
comments: true
categories: Testing
---

前段时间听同事提到"Model-based Testing"（基于模型的测试），挺有趣的，就找来相关资料研究了一下。下面是一些学习心得。

<!--more-->

## Table Of Contents

0. [Reference](#reference)
1. [Process](#process)
	* [Create State Model](#create-state-model)
	* [Generate Sequence of Actions](#generate-sequence-of-actions)
2. [Practice](#practice)
3. [Advantages](#advantages)
4. [Disadvantages](#disadvantages)
5. [Summary](#summary)

## Reference

参考资料主要是Microsoft的Principal SDET *Harry Robinson*的[个人网站](http://www.harryrobinson.net/)和[Model-based Testing community](http://model-based-testing.info/).

## Process

简短来讲，MBT是一种黑盒(Black Box)测试方法，将软件的行为抽象为模型，然后基于模型，选择合适的方式/算法，设计测试用例覆盖相应的模型，以测试各种模型代表的软件行为。

### Create State Model

首先需要对软件行为进行抽象，转化为模型。抽象模型需基于测试scope，选择合适的抽象粒度，否则可能抽象出无数种大小不一层次各异的模型。

在*Harry Robinson*的文章中，他是用以下三个属性来定义State Model的：

* Starting State
* Action
* Ending State

软件在运行过程中，可能会经过多种不同的状态State，触发切换状态的是不同的动作Action。某种状态，可能其中一个Model中的Ending State，又是另一个Model的Startging State。甚至可能通过相同或不同的Actions触发，在两个State之间相互切换，这也是2种不同的Models。

### Generate Sequence of Actions

在上步中得到一系列models后，首先将所有状态states画成不同的节点nodes，接着用表征方向的箭头线，连接不同model下的Starting State和Ending States，不同的线即表示不同的动作Actions。这样就可以得到一张有数个节点，其间有不同连线连接各个节点的拓扑图（也就是一张软件测试人眼中的状态机State Machine）。

接下来就要考虑如何设计测试场景，能完全覆盖所有models。其实就涉及到寻找一条尽可能短的路径，经过各个节点和连线，同时尽量不重复走过的路径。

*Harry Robinson*选择使用著名的图论Graph Theory中“中国邮递员问题”([Chinese postman problem](http://en.wikipedia.org/wiki/Chinese_postman_problem))的算法来解决。“中国邮递员问题”由中国数学家[管梅谷](http://baike.baidu.com/view/318032.htm)Kwan Mei-Ko于1962年研究并给出算法的。使用该算法，可以从上文提到的状态机快速地寻找出，能覆盖所有models的最短路径。

如果某些model更为关键，也可以加上一定的权重weight，通过算法中可实现多次穿越权重更高的节点和路径。

基于最短路径，即可设计出相应的测试用例并进行测试。

## Practice

在前不久的一次[new feature测试规划](http://blog.pzheng.me/blog/2014/07/04/a-practice-for-new-feature-grooming/)中，我们使用了该方法设计了其中部分测试用例。

在该新特性中，我们的产品需支持setup/addition/reconfiguration/deletion这四种Actions，状态是在最多4条links之间相互切换。下图即为整个状态图，不需要在该feature中测试的部分，在图中未予显示。

![MBT practice](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140720_MBT_practice.png)

最终我们从这么多条路径中，选择了一些我们认为更重要的路径，组成了一系列的test cases。基于上图，我们对路径的覆盖率，也有了相对清晰的把握。

## Advantages

* 快速方便的找出整体待测点；
* 用尽可能少的步骤覆盖尽可能多的路径；
* 清晰的把握整体覆盖率；

## Disadvantages

* 一旦需求更新，有新的节点加入，整体测试plan都要重新全盘更新；
* 复杂的通信设备上，各种feature之间的interworking也非常多，因此要精确的定义出各种可能的states，可能用时较长，并且数量庞大。有时甚至连状态都很难清晰界定。可能做出来也不具备可测性；
* 在MBT中假定的是每个state保持一定的独立性，所以测试中可能经过1次也就可以达到测试目的。但实际产品中，状态之间的影响是隐性的，因此有些问题是需要经过多次操作积累到一定量后才会暴露。对这种问题，MBT貌似还没有很好的办法解决；

## Summary

Model-based Testing非常有创意的将图论的算法，融合进测试当中，使测试人员可以快速又方便地制定测试计划，并对整体的路径覆盖率有一定的把控。因此，在测试一些有明确的动作以及状态界定的feature时，能很好的指导测试规划。但一旦系统庞大复杂起来，这种方法的可行性会大大降低。而对于一些需要随机测试，或者stability验证的场景，MBT能做也相对有限。

There is no silver bullet for testing. 一种测试方法不可能打遍天下。不过我们可以在了解学习之后，归入武器库。一旦有适用的场景，就可以立马派上用场。