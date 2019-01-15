---
title: CENTOS 修改静态IP
tags: Blog
originContent: ''
categories: []
toc: false
date: 2019-01-15 15:27:22
---

进入 /etc/sysconfig/network-scripts/ 文件
ifconfig 查看当前使用的网卡
修改对应网卡的ip
```bash
    BOOTPROTO="static" #dhcp改为static 
    ONBOOT="yes" #开机启用本配置
    IPADDR=192.168.7.106 #静态IP
    GATEWAY=192.168.7.1 #默认网关
    NETMASK=255.255.255.0 #子网掩码
    DNS1=192.168.7.1 #DNS 配置

```
