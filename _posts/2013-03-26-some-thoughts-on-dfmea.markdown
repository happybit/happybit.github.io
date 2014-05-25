---
layout: post
title: "Some Thoughts on DFMEA"
date: 2013-03-26 21:45
comments: true
categories: Testing
---

Yesterday I took part in a whole day training by my colleague *Zack Taylor* on **DFMEA**, which was really interesting. **DFMEA** stands for **D**esign **F**ailure **M**ode and **E**ffects **A**nalysis. It's a method (or process) for design product, either hardware or software, to predict and prevent defects before delivering.

<!--more-->

# Introduction

*Zack* told me **DFMEA** was a part of **FMEA**, which was created by (maybe) *Motorola* and once used in aviation design in 1960s. Well, it's a little bit different from [the history of FMEA](http://en.wikipedia.org/wiki/Failure_mode_and_effects_analysis#History) on Wikipedia. But one thing for sure, it was invented decades ago. And it was used in military/NASA firstly which extremely concerned about safety and security, and was introduced into software industry later. 

# Critical factors in DFMEA

Firstly team members should identify below critical issues along with **functionalities**:

* Failure mode
* Failure effect
* Failure cause

Then calculate the **Risk Priority Number** (**RPN**) based on the following values (also need input/discussion from team members): 

* Probability/occurrence
* Severity
* Detection

At last, take actions according to **RPN** list!

# My thoughts

It's a great idea to abstract a manual procedure to a general concept or methodology. The inventors tried to quantify and visualize the risks before implementation. Human beings are unmeasurable. But more and more modern methodologies are focusing on inspring the employees and measuring the productivity at the same time, e.g. **Agile**, as well as **DFMEA**. 

# My concerns

1. Team members might feel confused about the definition of "failure mode" and "failure cause". *Zack* said "failure mode" should not be sensed by customer. And with different **scope** of DFMEA, the same issue could be either "failure mode" or "failure cause". To be honest, now I am still perplexed about it... No wonder there will be lots of discussion of it on DFMEA meeting.
2. I am also confused about "detection". *Zack* told me it should be derived from customers' perspective instead of testers. But still, if our SW detects one certain fault, there will be only two possibilities, "raise alarm" or not. Thus no 1~10 levels of ratings. And why the weight of "detection" is the same as "occurrence" and "severity"?
3. All of these items and values are provided by humans. In other words, they are subjective to some extend, i.e. inaccuracy and uncertainty. How to avoid it?
4. Managers more like firefightors rather than wizards or witches. Those defects eliminating during DFMEA are non-existed and avoidable in their opinion. At the same time, it's very difficult to measure the quality of DFMEA.
5. It's a mindset about failure. And without doubt, successful DFMEA needs competency and experienced team member. How to implement it in an ordinary team? 
6. It's living document requiring constantly updating. In my view, process is very easy to be implemented as just a "process", instead of a mindset. Any ideas?

# Enlightening

Brainstorming during DFMEA is keeping asking "what if..." questions. So DFMEA is also a very good chance to discuss **exploratory testing** among architects/developers/testers. Also, we could just use the output of DFMEA as the input of our testing. See, all things have connections!

# Reference

If you are not familiar with this topic, please check the brief introduction on Wikipedia. 

* [FMEA](http://en.wikipedia.org/wiki/Failure_mode_and_effects_analysis)
* [DFMEA](http://en.wikipedia.org/wiki/DFMEA)

You could also check other alternatives:

* [Design Review Based on Failure Mode (DRBFM)](http://en.wikipedia.org/wiki/Design_Review_Based_on_Failure_Mode)
* [Fault tree analysis (FTA)](http://en.wikipedia.org/wiki/Fault_Tree_Analysis)
* [Taguchi methods](http://en.wikipedia.org/wiki/Taguchi_methods)
