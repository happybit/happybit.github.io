---
layout: post
title: "Conky Issue on Archlinux"
date: 2014-03-22 07:09:30 +0800
comments: true
categories: Archlinux
---

[Conky](http://conky.sourceforge.net/index.html) is a light-weight and handy system monitor for X on Linux. However, wheneven I click other area on the destkop, it would disappear immediately. Here is how I sovle it after googling around.

<!--more-->

Openbox, LXDE and PCManFM are used on my Archlinux. Later I found out the disappearing was caused by PCManFM which was also used for desktop management besides file manager. Please enter `# killall pcmanfm` and if there is no Conky disappearing afterwards, you could try my following method to replace PCManFM with Feh to manage wallpaper.

Please notice the autostart file might be different on different Linux distro.

1. Disable pcmanfm from autostarting. Edit `/etc/xdg/lxsession/LXDE/autostart` to remove or comment out below line:

        @pcmanfm --desktop-off --profile LXDE

2. Install Feh from official repository:

        # pacman -S feh

3. Edit `~/.config/lxsession/LXDE/autostart` to add:

        @feh --bg-fill /path/to/wallpaper.jpg

Attach my screenshot and `.conky` file.

![conky](https://dl.dropboxusercontent.com/u/6459697/blogimage/20140322_conky.png)

    alignment top_right
    
    own_window yes
    own_window_transparent yes
    own_window_type destop
    own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager
    
    double_buffer yes
    background yes
    text_buffer_size 512
    #maximum_width 
    
    border_width 1
    cpu_avg_samples 10
    default_color white
    #default_outline_color white${scroll 16 $nodename - $sysname $kernel on $machine | }
    default_shade_color white
    draw_borders no
    draw_graph_borders yes
    draw_outline no
    draw_shades no
    use_xft yes
    xftfont DejaVu Sans Mono:size=8
    gap_x 5
    gap_y 60
    #minimum_size 5 5
    net_avg_samples 2
    no_buffers yes
    out_to_console no
    out_to_stderr no
    extra_newline no
    own_window yes
    own_window_class Conky
    own_window_type desktop
    stippled_borders 0
    update_interval 1.0
    uppercase no
    use_spacer none
    show_graph_scale no
    show_graph_range no
    
    TEXT
    ${color grey}Archlinux $color ${alignr}${exec whoami}@$nodename
    ${color grey}$sysname $kernel on $machine 
    
    Date & Time ${hr 2}
    ${color grey}${execpi 60 DJS=`date +%_d`; cal | sed s/"\(^\|[^0-9]\)$DJS"'\b'/'\1${color}'"$DJS"'${color grey}'/}
    ${color}${font : size=16}${offset 150}${voffset -65}${time %l:%M:%S}${color grey}${offset 1}${voffset -24}${font : size=8}${time %p}
    
    
    
    
    
    
    Info ${hr 2}
    ${color grey}Uptime:$color $uptime
    ${color grey}Frequency (in GHz):$color $freq_g
    ${color grey}RAM Usage:$color $mem/$memmax - $memperc% ${membar 4}
    ${color grey}Swap Usage:$color $swap/$swapmax - $swapperc% ${swapbar 4}
    ${color grey}CPU Usage:$color $cpu% ${cpubar 4}
    ${color grey}CPU Temp: $color ${acpitemp} C
    ${color grey}Processes:$color $processes  ${color grey}Running:$color $running_processes
    ${color grey}Battery: ${color}${battery} ${battery_bar}
    
    HDD ${hr 2}
    ${color grey}root $color${fs_used /}/${fs_size /} ${fs_used_perc /}% ${fs_bar 6 /}
    ${color grey}boot $color${fs_used /boot}/${fs_size /boot} ${fs_used_perc /boot}% ${fs_bar 6 /boot}
    ${color grey}home $color${fs_used /home}/${fs_size /home} ${fs_used_perc /home}% ${fs_bar 6 /home}
    
    Network ${hr 2}
    ${color grey}SSID: $color${wireless_essid wlp3s0}
    ${color grey}Signal: $color${wireless_link_qual_perc wlp3s0}% ${alignr}${wireless_link_bar 8,60 wlp3s0}
    ${color grey}Address: ${color}${addr wlp3s0}
    Up:$color ${upspeed wlp3s0} ${color grey} - Down:$color ${downspeed wlp3s0}
    
    Processes ${hr 2}
    ${color grey}Name              PID   CPU%   MEM%
    ${color lightgrey} ${top name 1} ${top pid 1} ${top cpu 1} ${top mem 1}
    ${color lightgrey} ${top name 2} ${top pid 2} ${top cpu 2} ${top mem 2}
    ${color lightgrey} ${top name 3} ${top pid 3} ${top cpu 3} ${top mem 3}
    ${color lightgrey} ${top name 4} ${top pid 4} ${top cpu 4} ${top mem 4}
