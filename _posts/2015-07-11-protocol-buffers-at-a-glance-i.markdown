---
layout: post
title: "Protocol Buffers at a Glance I"
date: 2015-07-11 21:13
comments: true
categories: Radioaccess
---

前段时间在研究一个问题时，发现系统中某个组件，发送消息使用的是Google的[Protocol Buffers](https://developers.google.com/protocol-buffers/)。这里简单介绍一下，权作记录。

<!--more-->

当我们需要从一端向对端传输数据，需要规定好传输格式(rules)，否则当对端接收到数据后不知道如何将数据解码出来。通常，这种规范需要兼具human-readable和machine-readable的特性。Wikipedia有一个[专页](https://en.wikipedia.org/wiki/Comparison_of_data_serialization_formats)对比各种data serialization formats.

我们熟知的XML, JSON等，在human-readable方面做得都不错，且灵活度高。由于自带属性说明(key-value pair)，所传数据具备“自解释”性。但带来的副作用，是冗余度会提升。比如下例中的"firstName"/"lastName"等，甚至"{"/"}"/":"这些符号都会占用传输带宽。

{% highlight json %}
{
  "firstName": "John",
  "lastName": "Smith",
  "isAlive": true,
  "age": 25,
  "address": {
    "streetAddress": "21 2nd Street",
    "city": "New York",
    "state": "NY",
    "postalCode": "10021-3100"
  }
}
{% endhighlight %}

而在通信协议中，由于对时延的敏感和减少信令开销，我们通常使用的是[ASN.1](http://www.itu.int/en/ITU-T/asn1/Pages/introduction.aspx) (Abstract Syntax Notation One). 比如我们常用的[RRC信令传输](http://www.3gpp.org/DynaReport/25331.htm)中，会在RNC和Node B里都预设信息的模板和格式。这样只用按照格式传输value值，到了对端按照模板还原信息即可。这样大大减少了冗余信息的传输。但同时也造成了传输时，数据是一长串bit stream，可读性非常差。通常在调试时，需要辅助的解码工具才能有相对较好的human-readability.

手边没有现成的RRC message，下面以一条baseband message的部分信息为例。

| IE/Group Name                              | Value range | IE Type | Value (Decimal) | Value (Hexadecimal) |
|--------------------------------------------|-------------|---------|-----------------|---------------------|
| User ID                                    | 1…4095      | INTEGER | 1               | 0x01                |
| User Type                                  | 0, 1, 2, 3  |         | 0               | 0x00                |
| # of Radio Link Information                | 1…4         | INTEGER | 1               | 0x01                |
| Radio Link Information (SRadioLinkSetup.h) |             | STRUCT  |                 |                     |
| >RL-ID                                     | 0…31        | INTEGER | 10              | 0x0A                |
| >C-ID                                      | 1…65535     | INTEGER | 3               | 0x03                |
| >Frame Offset                              | 0…255       | INTEGER | 0               | 0x00                |
| >Chip Offset                               | 0…38399     | INTEGER | 0               | 0x00                |

最终传出去的serialized data是`01 00 01 0A 03 00 00`.

Google提出的Protocol Buffers更接近ASN.1。它也需要双方互知消息模板，用来decode数据。不过它使用的方式于ASN.1又有所不同。


