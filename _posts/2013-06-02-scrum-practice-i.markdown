---
layout: post
title: "Scrum Practice I"
date: 2013-06-02 06:08
comments: true
categories: Testing
---

Scrum master in our team took annual leaves these days. As her backup, I hosted the sprint retrospective & planning meeting, which was a rare and exciting experience to manage a scrum team and practice scrum.

<!--more-->

In my humble opinion, Agile aims to develop and test software in a more lightweight and quick-response way, which is why it's chosen by many software companies. But for the testing work in our team, more specifically, for testing large scale of telecom software, it's a bit difficult to do it lightly, due to the complexity of testing frame/tool/objectives.

Well it's another topic for the improvement of our testing frame (Honestly it hasn't been improved quite much. So it is still being far away from "idealy"). Today I'd like to summarize some tips we are using in sprint retrospective and planning.

### Sprint Planning
We will get the task list from Product Owner before sprint planning. And during planning, we need to break down those tasks which are expected to be finished in this sprint, estimate the effort for each task and check whether we could finish them on time.

#### Problems & Possible Reasons

Previously, we would simply sum up all the tasks' effort and compare it with the available time(total working hours - possible leave hours) in hour bank. But we found it was so inaccurate that we could hardly finish all the tasks we had promised in beginning.

In my view, there are two reasons for this inaccuracy:

1. Estimation is not precise.
2. Estimation is pure effort, instead of duration on timeline.

Group dicussion and breaking down tasks as small as possible would help for #1, as Agile coach suggests.

#### Effort vs. Duration

As for #2, you might be suprised. Frankly, now it's the biggest challenge in our team. Aforementioned complixity and dependency by other sites/components are definitely the cause. 

For instance, we may estimate a certain task is expected to complete within four hours. And the actual effort is four hours. But it lasts for, let's say, four days in the end. The scenario might be:

1. Tester spends two hours creating test scripts and running case. And he/she finds a problem in software.
2. After two days investigation, software guys would provide correction.
3. Tester verifies the correction and another bug is encountered in one hour. 
4. Feedback to software guys and discussion is still ongoing. Finally root cause is found two days later.
5. Tester verifies it again and report the test results in one hour.

This is a very common scenario in our daily work. The reality is much more complicated and time-consuming. Please don't ask why so much time is needed for software guys investigation. That's the current status which we cannot change in a multinational corporation.

As you can see, it only costs four hours for this task. But the duration is four days totally. So if we just sum the efforts up for all tasks, there might be huge gap between calculation and reality.

#### What Actions We've Taken

We use two simple tools in sprint planning to try to prevent such gap:

1. Mindmap tool (either [Freemind](http://sourceforge.net/projects/freemind/) or [Xmind](http://www.xmind.net/). Both are free.).
2. Calendar

Suppose we have a list of tasks and the effort has already been estimated. Now we need to fill those tasks into the calendar.

Firstly, add four nodes in Mindmap tool.

* Monthly target
* Weekly target
* Risks
* Leave plan

Secondly, add all the tasks with effort into "Monthly target" node. 

Thirdly, list the leave plan for the forthcoming sprint. And line through those days in calendar.

Fourthly, add several nodes under "Weekly target". Node number accords to the week number in one sprint. Generally there are four weeks (one month) in our team. Please highlight the actual working days(without weekends and public holidays) for each node.

Finally, fill those tasks into each week node accordingly. Leave plan should be taken into account during filling. And don't forget to list the risks under "Risks" node during planning.

Of course you may have daily target but it's to aggressive and pushing. We'd rather recommend weekly target.

After practice with several testers, we suprisely found we were too optimistic previously. Many tasks cannot be added into this map aligned with timeline. 

With weekly target, we could control the progress of project more carefully. Please also pay attention to "risks" which might cause delay for your project.

