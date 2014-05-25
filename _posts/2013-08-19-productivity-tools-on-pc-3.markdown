---
layout: post
title: "Productivity Tools on PC (3)"
date: 2013-08-19 06:13
comments: true
categories: Productivity
---

I found [*Total Commander*](http://www.ghisler.com/) was used by almost everyone in our company when I got on board. Because we have to work among several different scripts with different directories in our daily work. I fell in love with *Total Commander* soon after I tried it. And thanks to my firm, I can use an authorized one.

All the configurations are stored in a file names as "wincmd.ini" under directory `Application Data`.

<!--more-->

[++Download++](http://www.ghisler.com/download.htm) 

# F2 to rename

There has already been lots of defaul shortcusts in *Total Commander*. 

* Some work in *Firefox* way, e.g. `Ctrl + T` to open new tab, `Ctrl + W` to close current tab, etc. 
* Some are quite convenient, e.g. `F5` to copy, `F6` to move, `F7` to create new folder, etc.

But I still cannot get used to a few of them.

For example, by default, we cannot press `F2` to rename file or folder. You just need to add below lines in "wincmd.ini".

	[Shortcuts]
	F2=cm_RenameOnly

# Enable right button of mouse

You might be pissed of by some of the default configurations of *Total Commander*. For instance, right button of mouse is disable by default. You cannot use it to select file/check properties like the way in *Windows Explorer*, etc. I don't know the intension of author for disabling right button (maybe he wishes all operations should be executed by keyboard shortcuts :-)). But sometimes I really need it, especially when I want to compare some files via *Beyond Compare*.

So just copy this line in `[Configuration]` part of "wincmd.ini".

	UseRightButton=0

# Drives list

Drives are listed as drop-down list by default which is not convenient when I try to select different hard drives. Instead, I like all of them being displayed in the upper part of *Total Commander*. Then I could choose any drive with only one click.

Add `[Layout]` in "wincmd.ini" as followings:

	[layout]
	DriveBar1=1
	DriveBar2=1

You will see the change as below picture:

{% img /images/totalcmd_driverlist.png %}

# Using Specific Configuration File

As mentioned, all the settings are stored in "wincmd.ini" file. So you could over-write this file in `Application Data` by your own configuration file. 

Just in case you want to keep the default file still, you could open *Total Commander* in *Command*:

	> C:\Program Files\TOTALCMD.EXE i="d:\Dropbox\wincmd.ini"

Then you could store your *Total Commander* configuration file in *Dropbox* and bring it anywhere. 

But you may be tired of open *Command* and type so many letters. You could turn to *AutoHotKey* for quick opening.

	^!q::
	Run, "C:\Program Files\TOTALCMD.EXE" "/i="d:\Dropbox\wincmd.ini""
	return

Press `Ctrl + Alt + q`. And you could launch *Total Commander* with your own "wincmd.ini" like a charm.

See, this is the second time I integrated my tools together: *Total Commander*, *Dropbox* and *AutoHotKey*.

# Others Configurations

You might want to change the colore for selected files from red to others. Or some other configurations.

Please refer to my configuration file as below for details.

    [Configuration]
    StartupScreen=0
    firstmnu=1591
    PanelsVertical=0
    test=33
    SoundDelay=-10
    FirstTimeUnpack=0
    ShowCentury=1
    Aligned extension=0
    SizeStyle=1
    SizeFooter=1
    DirTabOptions=824
    DirTabLimit=32
    onlyonce=1
    TrayIcon=0
    UseRightButton=0
    Savepath=1
    Savepanels=1
    MarkDirectories=1
    AltSearch=2
    SaveCommands=1
    CountSpace=1
    CountMarked=1
    1hourdif=0
    CopyComments=6
    ShowHiddenSystem=0
    UseLongNames=1
    Small83Names=0
    OldStyleTree=0
    autotreechange=0
    ShowParentDirInRoot=0
    IconOverlays=0
    Showicons=2
    ShowEXEandLNKicons=2
    SortDirsByName=0
    Tips=3
    IconsOnNet=1
    FileTipWindows=1
    Win32TipWindows=0
    ThumbsLocation=%$LOCAL_APPDATA%\GHISLER
    ThumbsCopyDel=1
    ThumbsCustomFieldsEnabled=1
    ThumbOptions=15
    ThumbExplTypes=*.* | *.htm *.html
    ThumbPlgTypes=*.*
    ThumbIrfXnTypes=*.*
    ThumbTxtTypes=*.txt *.ini
    FirstTimeZIP=0
    ExplorerForCopy=0
    Win95Delete=0
    UseTrash=1
    InstallDir=D:\Software\Utilities\totalcmd
    AlwaysToRoot=0
    SingleClickStart=0
    RenameSelOnlyName=0
    SaveHistory=1
    SeparateTree=0
    DirBrackets=1
    SortUpper=0
    QuickSearchAutoFilter=1
    [left]
    path=D:\
    ShowAllDetails=1
    SpecialView=0
    show=1
    sortorder=0
    negative Sortorder=0
    [right]
    path=D:\
    ShowAllDetails=1
    SpecialView=0
    show=1
    sortorder=0
    negative Sortorder=1
    [Command line history]
    [1280x800 (8x16)]
    TreeDlgX=434
    TreeDlgY=201
    TreeDlgDX=411
    TreeDlgDY=397
    TreeDlgMax=0
    Tabstops=278,281,339,-1,736,93
    MenuChangeX=160
    MenuChangeY=120
    MenuChangeDX=960
    MenuChangeDY=560
    MenuChangeMax=1
    ConnectX=397
    ConnectY=215
    ConnectDX=485
    ConnectDY=370
    ConnectMax=0
    [Confirmation]
    deleteDirs=1
    OverwriteFiles=1
    OverwriteReadonly=1
    OverwriteHidSys=1
    MouseActions=1
    [Shortcuts]
    F2=cm_RenameOnly
    C+A+e=em_everything
    [Layout]
    ButtonBar=1
    DriveBar1=1
    DriveBar2=1
    DriveBarFlat=1
    InterfaceFlat=1
    DriveCombo=1
    DirectoryTabs=1
    CurDir=1
    TabHeader=1
    StatusBar=1
    CmdLine=1
    KeyButtons=1
    HistoryHotlistButtons=1
    XPthemeBg=1
    BreadCrumbBar=1
    [Lister]
    Startup=17
    textwidth=81
    binwidth=75
    SearchGoBack=3
    BmpStartup=1
    Multimedia=1
    RTF=1
    IView=0
    IViewPath=i_view32.exe
    HTMLasText=1
    LinkBraces=1
    [Colors]
    InverseCursor=0
    InverseSelection=1
    BackColor=-1
    ForeColor=-1
    MarkColor=8388608
    CursorColor=255
    CursorText=-1
    [Packer]
    InternalZip=1
    InternalUnzip=1
    zipnt=0
    ZIP=pkzip.exe
    UnZIP=pkunzip.exe
    InternalZipRate=6
    Zip83Name=0
    ZipSetDateToNewest=0
    nodelete=0
    OpenPartial=0
    ZIPlikeDirectory=1
    InternalUnarj=1
    ARJlongnames=0
    InternalUnlzh=1
    InternalUnrar=1
    InternalUnace=1
    LinuxCompatible=1
    ARJ=arj.exe
    LHA=lha.exe
    RAR=rar.exe
    UC2=uc.exe
    ACE=ace32.exe
    [Tabstops]
    0=278
    1=281
    3=339
    4=-1
    6=736
    5=93
    AdjustWidth=1
    [MkDirHistory]
    [1440x900 (8x16)]
    CmdSelX=394
    CmdSelY=220
    CmdSelDX=637
    CmdSelDY=371
    CmdSelMax=0
    ConnectX=477
    ConnectY=265
    ConnectDX=485
    ConnectDY=370
    ConnectMax=0
    [1440x900 (10x20)]
    ConnectX=472
    ConnectY=263
    ConnectDX=485
    ConnectDY=451
    ConnectMax=0
    MenuChangeX=150
    MenuChangeY=150
    MenuChangeDX=864
    MenuChangeDY=496
    MenuChangeMax=0
    [1280x800 (10x20)]
    MenuChangeX=145
    MenuChangeY=25
    MenuChangeDX=768
    MenuChangeDY=436
    MenuChangeMax=0
    [DirMenu]
    [lefttabs]
    [righttabs]
    [RightHistory]
    [LeftHistory]
    
