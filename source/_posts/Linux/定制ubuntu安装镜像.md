---
title: 定制ubuntu系统安装镜像
date: 2018-10-12 17:49:44
tags: Linux
---

## 环境准备
1. 使用ubuntu系统（目前使用1604 桌面版）
2. 定制包含docker的ubuntu server 安装镜像，定制后安装过程跟原先ubuntu server安装过程一样。

## 工具准备
1. Cubic软件（软件需要GUI，所以使用桌面版本的ubuntu）
2. ubuntu server 镜像（ubuntu 官网下载）

## 开始安装
1. cubic软件安装
```
sudo apt-add-repository ppa:cubic-wizard/release
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 6494C6D6997C215E
sudo apt update
sudo apt install cubic
```
2. 打开软件，选择工作目录，最后会在该目录中生成iso镜像文件
![](http://images.javayuan.cn/15393381317711.jpg)

3. 在Original ISO 中选择需要自定义的镜像文件，这里为ubuntu server。Custom ISO中的属性是根据镜像文件自动生成的属性，可以自己修改一下，比如version filename Release name 等。
![](http://images.javayuan.cn/15393383943295.jpg)
4. 下一步进入系统环境自定义，在此命令终端中可以使用apt 等命令安装一些软件，并且如果想要往镜像里面放文件，可以直接将文件拖动到这个窗口中，根据提示即可完成文件的复制，在这里更改后，安装完的系统都会存在，比如我在这儿使用apt装了一个docker，在别的电脑上用我自定义的镜像装完后会自带docker，跟预安装软件类似。
![](http://images.javayuan.cn/15393386276170.jpg)
5. 最后根据提示点击下一步即可创建成功自定义镜像。生产镜像后系统的安装步骤跟原先一样。可以使用VirtualBox 等虚拟机进行测试。
![](http://images.javayuan.cn/15393386679168.jpg)


