---
layout: post
title: "Two Tips For This Week"
date: 2014-11-02 20:27
comments: true
categories: Productivity
---

I was annoyed by two issues for a long time when using Total Commander. This week I spent half an hour to tweak my settings and solved them quickly.

<!--more-->

## Open text file in existing Emacs process

GNU Emacs is always openning on my computer. So I am trying to open and edit text files in the existed Emacs window instead of a new Emacs window.

Firstly, you need to add below line in your `.emacs` file.

    (and window-system (server-start))

Then add below AutoHotKey snippet to your AHK configuration file.

    ^!e::
        ClipTemp := ClipboardAll
        Clipboard :=
        Send, ^c
        ClipWait, 200
        S := Clipboard
        SplitPath, S, SName
        Clipboard := ClipTemp
        If (S != "")
            Run, D:\Backup\Software\Develop\emacs-24.3\bin\emacsclientw.exe -n %S%
        return
		
Please replace `D:\Backup\Software\Develop\emacs-24.3\bin\emacsclientw.exe` to the correct Emacs client path on your PC.

At last, select a text file and press `Ctrl` + `Alt` + `e` simultaneously. This file would be opened in Emacs client immediately.

## Unpack archive file to the same folder

There is a built-in shortcut key in Total Commander to unpack archive file: `Alt` + `F9`. However, the unpacked files would be allocated to the folder in the other column of Total Commander. Is it possible to unpack them in the same folder as the original archive?

Of course. We still need a little help from AutoHotKey. Below codes are coming from [internet](http://www.ghisler.ch/wiki/index.php/AutoHotkey:_Unpack_each_archive_to_a_separate_subdir). 

    ^!u::
    IfWinActive ahk_class TTOTAL_CMD
    {
    	PostMessage, 1075, 509
    	WinWaitActive, ahk_class TDLGUNZIPALL
    	Send, {Del}
    	Control, Check, , TCheckBox1
    	Send, {Enter}
    }
    else
    	Send ^!+{F9}
    return
	
Select the zip file in Total Commander and press `Ctrl` + `Alt` + `u`. It would work like a charm. It's time to replace `Alt` + `F9` to this shotcut key.
