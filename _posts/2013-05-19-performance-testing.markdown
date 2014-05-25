---
layout: post
title: "Performance Testing"
date: 2013-05-19 19:57
comments: true
categories: Testing
---

Performance testing is kind of advanced testing when basic functionalities have already been verified in software. And there are several terms regarding performance testing, such as capacity testing, load testing, etc. Once I heard about them from bunch of guys and was confused by different meanings of them from different people's perspective. 

There is a dedicated page on Wikipedia for [performance testing](http://en.wikipedia.org/wiki/Software_performance_testing). But here I'd like to share my view about it.

<!--more-->

### Stability testing

The main objective of stability testing is to verify that SW functions correctly with at least such traffic intensity that it is normally designed to handle (i.e. nominal traffic) and that SW is stable **when loaded for a long time**. The used traffic mix is designed in co-operation with product management. Traffic should correspond real traffic as much as possible. Other objectives of stability testing are to find faults and to verify capacity requirements defined in product documentation.

The keyword of stability testing is lasting for amount of time, one hours, six hours, one day, two days, one week, etc. It depends on the usage of software in customer field. 

Generally, there are three phases for stability testing:

* low load
* moderate load
* high load

### Capacity testing

These tests consist of detailed measurements of the capacity influence of different events. It focuses on different kinds of traffic/services, and how much load SW could afford for each profile. Usually, the real capacity of software is more than what product managers promise to customers for margin purpose.

Major target of capacity testing is to verify different capacities for different profiles which are defined in requirements.

### Overload testing

In the overload tests, traffic are obviously overloaded. There are two situations:

1. Load is more than requirement but less than the real capacity of software.
2. Load is even more than the real capacity of software.

General rule for overload testing is, software could reject those extra traffic. But it should at least obtain the nominal capacity in requirements and shouldn't crash for any reason! Sometimes requirements would define the performance of software with different level of overload traffice.

Overload control is a MUST considered functionality in software design.
