---
title: ubuntu 静态ip配置
tags: [Ubuntu,IP]
categories:
  - Linux
toc: false
date: 2018-10-12 12:33:21
---

## ubuntu 静态ip配置
`sudo vi /etc/network/interfaces`
```
auto eth0
iface eth0 inet static
address 192.168.8.100    
netmask 255.255.255.0
gateway 192.168.8.2
dns-nameserver 114.114.114.114
```
重启网络：`sudo /etc/init.d/networking restart`
## docker load image
系统image 存放路径 /videon/install;
使用`sudo docker load -i ./image.tar`，导入image;
## docker 启动系统
yml文件存放路径 /videon/docker;
使用`sudo docker-compose -f ./app.yml up`;
如需后台运行加`-d`即可;
## 修改res目录权限
使用`sudo chmod 777 /home/vn/res`
