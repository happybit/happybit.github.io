---
layout: post
title: "OVSF Codes"
date: 2014-03-12 21:34:32 +0800
comments: true
categories: Radioaccess
---

As we know, the channelization codes for physical channels in UMTS should be orthogonal. Otherwise the reciever would not be able to decode the data correctly.

<!--more-->

## Spreading Factor

3GPP adopts [Hamamard Codes](http://en.wikipedia.org/wiki/Hadamard_code), a.k.a. Walsh Codes, to generate channelisation codes as below figure(from [WCDMA for UMTS HSPA Evolution and LTE 5th Edition](http://www.amazon.com/Harri-Holma-Antti-Toskala-Evolution/dp/B00AOTQMC2)). In UMTS, we usally call them OVSF(**O**rthogonal **V**ariable **S**preading **F**actor) codes.

{% img /images/20140312_channelizationcodes.png %}

## Orthogonal

It's easy to understand why the codes with the same Spreading Factor(SF) are orthogonal. 

For instance, C<sub>4,3</sub> and C<sub>4,4</sub> are orthogonal since the product(bit by bit) is 0.

> C<sub>4,3</sub>(1) * C<sub>4,4</sub>(1) + C<sub>4,3</sub>(2) * C<sub>4,4</sub>(2) + C<sub>4,3</sub>(3) * C<sub>4,4</sub>(3) + C<sub>4,3</sub>(4) * C<sub>4,4</sub>(4) 
> = 1 * 1 + (-1) * (-1) + 1 * (-1) + (-1) * 1 
> = 0

Assume there are two channels to transmit data. Let's say signal on one channel is *x* while signal on the other channel is *y*. And *x* is spread by channelization code C<sub>4,3</sub> and *y* is spread by code C<sub>4,4</sub>. So the final data to receiver is:

> x*C<sub>4,3</sub> +  y*C<sub>4,4</sub>

Receiver should be aware of these two channelization codes in advance, from for example control channels etc. Thus it could respectively decode the original data by multipying received data by each channelization code. That is:

> (xC<sub>4,3</sub> +  yC<sub>4,4</sub>) * C<sub>4,3</sub> = x*C<sub>4,3</sub>*C<sub>4,3</sub> +  y*C<sub>4,4</sub>*C<sub>4,3</sub> = x*C<sub>4,3</sub><sup>2</sup> 

That's why we say ideally there is no inter-channel intereference once they are spread by channelization codes.

## Non-orthogonal

In *WCDMA for UMTS HSPA Evolution and LTE 5th Edition*, it says below words without detailed explanation.

> There are certain restrictions as to which of the channelization codes can be used for a transmission from a single source. Another physical channel may use a certain code in the tree if no other physical channel to be transmitted using the same code tree is using a code that is on an underlying branch, i.e. using a higher spreading factor code generated from the intended spreading code to be used. Neither can a smaller spreading factor code on the path to the root of the tree be used. 

Still, take C<sub>2,2</sub> and C<sub>4,4</sub> as example. But here is the problem, C<sub>4,4</sub> is a four-dimensional vector meanwhile C<sub>2,2</sub> is only two dimensional. How to linealy multiply these two vectors? 

One of my colleagues told me, in Linear Algebra, the missing bits would be filled with "0" in case two different dimensional vectors multiply. Thus the product of C<sub>2,2</sub> and C<sub>4,4</sub> should be "2" instead of "0".

It's more clear to draw an illustrator when the signal is one bit as "1". Because the chip duration T<sub>chip</sub> is fixed as 1/3840000 second. The spreading data with C<sub>4,4</sub> is longer than C<sub>2,2</sub>.

{% img /images/20140312_non_orthogonal_1.png %}

If the input data is (1, -1) and spread by C<sub>2,2</sub>. Then the output will be exactly the same as "1" spread by C<sub>4,4</sub>.

{% img /images/20140312_non_orthogonal_2.png %}

That's why certain code and its children codes are not orthogonal. And it is impossible for receiver to decode the original channel data respectively. 
