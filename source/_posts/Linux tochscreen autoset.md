---
title: Linux toch screen autoset
date: 2018-12-29 13:51:56
tags: [Linux,Screen,Touch]
categories:
  - Linux
---

I wrote a simple script that will fix things using udev. First create /etc/udev/rules.d/99-monitor-hotplug.rules

It is just this line:

`ACTION=="change", SUBSYSTEM=="drm", ENV{HOTPLUG}=="1", RUN+="/usr/share/X11/touchscreen.sh"`

Now the /usr/share/X11/touchscreen.sh file (mark it +x !!) :

```
#!/bin/sh
#
# This is designed to be run by hotplug.  See hotplug docs ...
#

# Make sure PATH is sane
export PATH="/bin:/usr/bin"

# Now the rest of the ENV to hook into X
# This should probably be run by Dbus, but I don't know how.
# Instead I see who's running Dbus, and get that user's .Xauthority
# So, its kind of a hack!

export USER=`ps -ef | grep dbus-daemon | grep session | cut -d ' ' -f 1`
export DISPLAY=":0"
export XAUTHORITY=/home/$USER/.Xauthority
export ICON=/usr/share/icons/Adwaita/scalable/devices/video-display-symbolic.svg

# Find Touchscreen id number -- sets id
export `xinput | grep touch | cut -f 2`

# Find the primary screen! 
export screen=`xrandr | grep primary | cut -d ' ' -f 1`
# sleep
sleep 1s
# Use xinput to map them
xinput --map-to-output $id $screen

su $USER -c "notify-send -i $ICON \"TouchScreen\"\
 \"Mapping Device $id to your $screen screen\""

```