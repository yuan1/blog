---
title: centos7 teamviewer安装（依赖安装）
tags: [CentOS,Teamviewer,Install]
categories:
  - Linux
toc: false
date: 2019-01-07 10:26:42
---

缺少依赖：
![image.png](http://images.javayuan.cn/FjTudoWEnAdP2WganY_HIW-bXiFr)

安装支持库
```bash
sudo yum install -y epel-release
```

安装依赖：
```bash
sudo yum install qt5-qtdeclarative qt5-qtwebkit qt5-qtx11extras qt5-qtgraphicaleffects qt5-qtquickcontrols
```