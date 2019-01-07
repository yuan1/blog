---
title: ubuntu 静态ip配置
tags: Blog
originContent: "# \b胶片项目部署\n\n## ubuntu 静态ip配置\n`sudo vi /etc/network/interfaces`\n```\nauto eth0\niface eth0 inet static\naddress 192.168.8.100\_\_ \_\nnetmask 255.255.255.0\ngateway 192.168.8.2\ndns-nameserver 114.114.114.114\n```\n重启网络：`sudo /etc/init.d/networking restart`\n## docker load image\n系统image 存放路径 /videon/install;\n使用`sudo docker load -i ./image.tar`，导入\b\b\bimage;\n## docker 启动系统\nyml文件存放路径 /videon/docker;\n使用`sudo docker-compose -f ./app.yml up`;\n如需后台运行加`-d`即可;\n## 修改res目录权限\n使用`sudo chmod 777 /home/vn/res`"
categories: []
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
