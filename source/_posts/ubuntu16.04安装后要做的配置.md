---
title: ubuntu16.04安装后要做的配置
date: 2018-7-20 4:14:55
tags: [Linux,Ubuntu,Install]
categories:
  - Linux
---

* 卸载不常用的软件
```bash
卸载libreofficesudo apt-get remove --purge libreoffice*/
```
  
* 安装必备软件
```bash
ubuntu-tweak-tool  
sudo apt install ubuntu-tweak-tool  
screenfetch  
sudo apt install screenfetch  
gparted分区工具  
sudo apt install gparted  
gimp图像编辑  
sudo apt install gimp  
GDebi程序安装工具  
sudo apt install gdebi  
virtualBox虚拟机  
sudo apt install virtualbox  
vlc视频播放器  
sudo apt install vlc  
系统美化  
flatabulous-theme  
sudo add-apt-repository ppa:noobslab/themes  
sudo apt-get update  
sudo apt-get install flatabulous-theme  
ultra-flat-icons  
sudo add-apt-repository ppa:noobslab/icons  
sudo apt-get update  
sudo apt-get install ultra-flat-icons  
numix-gtk-theme   
sudo add-apt-repository ppa:numix/ppa   
sudo apt-get update && sudo apt-get install numix-gtk-theme  
numix-icon-theme-circle  
sudo add-apt-repository ppa:numix/ppa   
sudo apt-get update && sudo apt-get install numix-icon-theme-circle  
```