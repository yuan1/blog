---
title: 我的conky配置文件
date: 2017-11-2 10:36:2
tags: Linux
---
* github地址：[https://github.com/yuan1/MyOwnConky](https://github.com/yuan1/MyOwnConky)
* 编辑conky配置文件gedit ~/.conkyrc，讲conkyrc文件中的内容复制到里面，可以修改network下的enp1s0为你的链接，比如我用WiFi就修改为wlan0
* 新建.conky目录mkdir ~/.conky
* 将conky目录下的conky-startup.sh复制到.conky下
* 将autostart目录下的conky.desktop复制到~/.config/autostart目录下
* 重启即自动启动