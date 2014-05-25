---
layout: post
title: "Productivity Tools on PC (5)"
date: 2013-11-18 22:11
comments: true
categories: Productivity
---

Outlook is the only choice in my company to handle with E-mails. Normally, I would receive 40~50 mails everyday and reply around 20 out of them. How to deal with so many mails was a big problem to me until I found [PIFEM(Pay It Forward Email Management)](http://blogs.msdn.com/b/ianpal/archive/2008/06/03/email-task-and-time-management-with-pifem.aspx) created by [Ian Palangio](http://blogs.msdn.com/ianpal). I immediately fell in love with this method and tweaked it according to my situation. After two years using, I am so pleased to introduce it here.

<!--more-->

## Environment

1. Windows 7 Professinal 64-bit
2. Outlook 2007

## Pre-rules

### Rule #1: Cancel Alerts

Before you do anything, please firstly cancel Outlook alerts. Yes alerts will keep you following the updates in time. But most of the time it distracts me quite a bit. I'd check the outlook randomly after cancelling the alerts. Fortunately I haven't missed any urgent e-mails. 

![Cancel alerts](https://dl.dropboxusercontent.com/u/6459697/blogimage/20131118_cancelalerts.jpg)

### Rule #2: Regular PST 

I would archive my PST file regularly, which means to create new PST file per six months. Since there might be unexpected problems when PST file is larger than 2Gb. And the naming rule is listed as below:

![PST half year](https://dl.dropboxusercontent.com/u/6459697/blogimage/20131118_PSThalfyear.jpg)

### Rule #3: Organized Folders

And in each PST, there are several organized folders based on different priorities. I would press `v` to move some useful items to corresponding folder via [AHK]().

![Organized folder](https://dl.dropboxusercontent.com/u/6459697/blogimage/20131118_organizedfolder.jpg)

I will adjust the order and folder structure based on my needs at that time when initiate a new PST data file.

### Rule #4: Apply rules

There would be certain mails sent by Robots. And it's unnecessary to check them one by one. You just need to archive them to specific folders. And you could check it when you need them.

Another most important thing is, don't forget to "mark them as read" when applying such rules. I hate those unread numbers!

## PIFEM

In GTD, the No. 1 rule is to keep inbox clean. However, with PIFEM, this inbox is not the one displayed in each PST. We are gonna set up a new "inbox" from nowhere. 

Actually the essential of PIFEM is to use "Search Folders"/"Follow up"/"Category" flexibly. Here is my list of favorite folders.

![Favorite folder](https://dl.dropboxusercontent.com/u/6459697/blogimage/20131118_favoritefolders.jpg)

### Set up Search Folders

You could follow below steps to set up new Search Folders.

![Search folder](https://dl.dropboxusercontent.com/u/6459697/blogimage/20131118_searchfolders.jpg)

#### Inbox (To Be Vetted)

Here is the virtual "inbox" you have to cope with every now and then.

![Vetted inbox](https://dl.dropboxusercontent.com/u/6459697/blogimage/20131118_vettedinbox.jpg)

#### Follow up (Today)

All the mails you need to read/reply/finish will be found in this very folder. You just need to focus on this folder everyday and try your best to finish all of them by the end of day. That's it.

![followup today](https://dl.dropboxusercontent.com/u/6459697/blogimage/20131118_followuptoday.jpg)

#### Follow up (Later)

All the mails you need to deal with on tomorrow or even later.

![followup later](https://dl.dropboxusercontent.com/u/6459697/blogimage/20131118_followuplater.jpg)

#### Follow up (Maybe)

All the mails you might read but with low priorities.

![followup maybe](https://dl.dropboxusercontent.com/u/6459697/blogimage/20131118_followupmaybe.jpg)

#### Tasks - Delegate

You might want to check those mails you sent out. For example, assign some tasks to somebody else. Or ask help from others. But you would forget if they miss that mail.

![delegate task](https://dl.dropboxusercontent.com/u/6459697/blogimage/20131118_delegatetask.jpg)

#### Inbox (Completed Today)

This is just a folder to display those mails you have finished today. 

![completed today](https://dl.dropboxusercontent.com/u/6459697/blogimage/20131118_completedtoday.jpg)

#### Add Search Folders to Favorite Folders

Finally you just need to add those new search folders to "Favorite Folders".

![addfavorite folders](https://dl.dropboxusercontent.com/u/6459697/blogimage/20131118_addfavoritefolders.jpg)

### Workflow

1. When you get a new mail, you just need to choose next action from below accordingly:
    - delete it;
    - or move it to proper folders for future reference;
    - or flag it as "Today";
    - or flag it as "Tomorrow" or someday in the future;
    - or flag it as "No date";
  
	![newmail](https://dl.dropboxusercontent.com/u/6459697/blogimage/20131118_newmail.jpg)	
  
    Just remember to proceed mails appropriately and keep "Inbox (To Be Vetted)" empty.
  
2. Focus on "Follow up (Today)" everyday and work. When you finish that mail (mostly end by replying it), you just need to click flag again and mark it as "Completed". It will disappear from this folder.

    The mails in "Follow up (Later)" will be showed in this folder on start date.

3. After you reply one mail and you feel like it's better to follow up it. You could assign the task into "Tasks - Delegate" category and proper follow-up date.

4. Actually all the mails are still in the real inbox. And it's kind of messy at first glance. So it's better to sort your real inbox weekly and only keep those unfinished items.

	![real inbox](https://dl.dropboxusercontent.com/u/6459697/blogimage/20131118_realinbox.jpg)

## Summary

That's all. I promise you are gonna love PIFEM once you try it. It definitely makes my life much easier.

Later, I will write a new post to introduce how I integrate Outlook (PIFEM) with Emacs Org-mode.
