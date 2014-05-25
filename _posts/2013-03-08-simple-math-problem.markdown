---
layout: post
title: "Simple math problem"
date: 2013-03-08 21:01
comments: true
categories: Testing
---

Here is a problem I met during designing test case:

>Module **A** is claimed to be able to process *MaxPrcMsg* messages per second. The buffer could store each message for at most 2 seconds. Once the message hasn't been proceeded within 2 seconds, it will be expired. Input messages are rushed into Module **A** every 100ms. In case the testing duration is (*n* * 100ms). How to set the maximum number *MaxInMsg* of input messages to verify the performance of Module **A** with high load?

The author of this requirement has presented the result and brief calculation. I read about it and found it was interesting. We could solve it by primary school skills.

<!--more-->

Firstly, please take a look at this simple math problem (water in and out):

>Water is drained with stable velocity *x* L per second from tub, whose capacity is *y* L. At the same time, *z* L fresh water is poured in the tub every second. Give a duration *t*. How to set *z* as big as possible without breaking the maximum capacity of the tub.

See, so simple. Isn't it?

The final result is

*MaxInMsg* =  [2 + (*n*-1) * 0.1] * *MaxPrcMsg*

Assume the buffer is empty at the beginning, and *MaxPrcMsg* is 40.

1. In case *n* is 1 (the duration is 100ms), *MaxInMsg* equals 80 as shown in above formula. It means at most 80 messages could be sent to module **A** within 100ms. But in the next 1.9 second, **A** cannot afford any more message at all.

2. In case *n* is 3 (the duration is 300ms), *MaxInMsg* equals 88 as shown in above formula. It doesn't mean we could send 88 messages at the first 100ms, or even (80+8) at the first and second messages. Since when *n* equals to 2, *MaxInMsg* should be 84. So the proper setting should be 80+4+4.

Would you please give a reasonable input for *n* = 100, to keep the buffer in always full state and module **A** always busy in the mean time?

