---
title: Linux下校园网锐捷4.x安装与运行
date: 2018-6-10 4:24:18
tags: [Linux,School]
categories:
  - Linux
---
* 下载源码  
[https://github.com/yuan1/mentohust](https://github.com/yuan1/mentohust)
* 把etc目录下的文件全部复制到/etc目录下
* 把usr/bin目录下的文件复制到/usr/bin目录下
* 执行sudo chmod a+xs /usr/bin/mentohust添加执行权限
* 执行mentohust 根据具体情况配置即可 
* 如校园网是指定ip，需要先设置ip然后在认证过程中不要选择使用dhcp获取ip
* 配置完成，认证成功后可用ctrl+c结束，然后执行sudo mentohust -b3 -w后台运行
  