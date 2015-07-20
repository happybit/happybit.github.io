---
layout: post
title: "Protocol Buffers at a Glance II"
date: 2015-07-19 21:57
comments: true
categories: Radioaccess
---

[上篇](http://blog.pzheng.me/2015/07/11/protocol-buffers-at-a-glance-i/)简单介绍了JSON和ASN.1作为Protocol Buffers的背景知识。今天我们来具体讲解一下Protocol Buffers的encoding。

<!--more-->

官方网站上有专门的[Encoding](https://developers.google.com/protocol-buffers/docs/encoding)一章详述如何编码。这里就以一个简单的例子来讲解。

假如我们需要传输一条消息，这条消息里包含一个structure，或者用官方说法是embedded message（嵌入式消息）。里面息只有一个元素叫userId，值为4621.

~~~
removeUser {
    userId = 4621;
}
~~~

为了更清晰的展示编码过程，我们先来看一下编码完成后的结果，通过解码来看其中的原理。这条消息经过编码后，serialized data为(0x表示十六进制):

    (0x) 1A 03 08 8D 24

## Step 1 Wire type

首先来看0x1A，转化为二进制(0b)为：

    (0b) 00011 010

请注意，上面估计写成右边LSB的低三位和MSB的高五位分开。原因是，LSB的这三位表示的是这个field的wire type，如下：

| Type | Meaning          | Used For                                                 |
|------|------------------|----------------------------------------------------------|
| 0    | Varint           | int32, int64, uint32, uint64, sint32, sint64, bool, enum |
| 1    | 64-bit           | fixed64, sfixed64, double                                |
| 2    | Length-delimited | string, bytes, embedded messages, packed repeated fields |
| 3    | Start group      | groups (deprecated)                                      |
| 4    | End group        | groups (deprecated)                                      |
| 5    | 32-bit           | fixed32, sfixed32, float                                 |

(0b) 010是十进制的2，对应地，表示这个field里的值类型是“string, bytes, embedded messages, packed repeated fields”的其中一种。如前所述，这个例子里表示embedded message.

## Step 2 Field number

再将剩下MSB的高五位，向右移三位，得到(0b) 11，为十进制的3. 表示这个field number。这里就要介绍一下Protocol Buffers的模板机制。

我们需要提前预设消息模板，一般以.proto为文件扩展名。如下是userconfig.proto:

~~~
message Userconfig {
    ...
    message ActionUserconfig {
        required int32 userId = 1;
    }
    ...
    optional ActionUserconfig addUser = 2;
    optional ActionUserconfig removeUser = 3;
    ...
}
~~~

这里的field number就是指在这条消息里tag为3的这个optional的structure，也就是说，是removeUser message.

## Step 3 Payload length

接下来看(0x) 03，十进制也是3。表明后面接着有3个bytes的payload。数一数，(0x) 08 8D 24，确实是三个bytes.

## Step 4 Values

接着用step 1/2/3里的方法再来解析(0x) 08 8D 24。简单的讲：

* `(0x) 08`转换为二进制是`(0b) 00001 000`, 得到wire type是`0`，表示是Varint；
* 同时得到field number为`1`，从消息模板中，找到对应的tag为`1`的就是userId；
* `(0x) 8d 24`转换为二进制是`(0b) 10001101 00100100`；
  * 按照每8 bits分成两份，分别为`(0b) 10001101`和`(0b) 00100100`；
  * 分别去掉MSB的最高一位，得到`(0b) 0001101`和`(0b) 0100100`. （最高位是用来表示是否到了number的结尾，如果number多于一个byte，就会将第一个byte的最高位设为`1`）;
  * 再将右边的数放在左边（高位），左边的数放在右边（低位），拼在一起，得到`(0b) 00100100 10001101`.相当于做了一次大小端的转换。最终可知`(0b) 00100100 10001101` = `(0x) 12 0D`，也就是十进制的`4621`.

可以看到`.proto`文件在编解码过程中，起了非常关键的作用。这点和ASN.1类似，但和JSON等自解释的截然不同。
