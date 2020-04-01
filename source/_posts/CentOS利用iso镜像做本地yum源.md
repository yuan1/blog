---
title: CentOS利用iso镜像做本地yum源
tags: [CentOS,ISO,YUM,Install]
categories:
  - Linux
toc: false
date: 2019-01-07 11:57:27
---

## 介绍
CentOS是完全免费的，它的yum可以直接使用；而RedHat的yum则需要注册付费才能使用，如果不这样则有两种解决方案，也可以说是三种。
1. 利用iso镜像做本地yum源
2. 利用光盘做本地yum源
3. 利用Centos的在线地址做本地yum源
在这里用iso或者光盘做本地yum源的方法是差不多的，只是用光盘的话Linux系统会自动挂载，用iso镜像的或需要手动挂载，这里就说挂载iso的方法吧。

## 使用
1. 创建iso存放目录和挂载目录
```bash
mkdir /mnt/iso 
mkdir /mnt/cdrom
```

2. 将iso镜像文件上传到/mnt/iso文件夹下

3. 将/mnt/iso/下的iso文件挂载到/mnt/cdrom目录
```bash
mount -o loop /mnt/iso/XXXXX.iso /mnt/cdrom 
```
	<注：挂载完之后对其操作会提示设备繁忙，此时需要umount解开挂载才行>


查看是否挂载成功： 
```bash
df -h
```
	<用来查看系统中所有挂载的，mount也可以>

4.<最关键的一步>如果/etc/yum.repos/下面有其它的*.repo文件，先创建个文件夹，将这些*.repo先转移到文件夹中，自己写一个.repo的文件
```bash
mkdir /etc/yum.repos.d/bak
mv *.repo /etc/yum.repos.d/bak 
```
 然后创建自己的.repo文件
```bash
vi myself.repo
```

 内容如下：
```bash
[base]
name=RedHat
#注：这里的baseurl就是你挂载的目录，在这里是/mnt/cdrom
baseurl=file:///mnt/cdrom    
#注：这里的值enabled一定要为1  
enabled=1                    
#gpgckeck的值无所谓
gpgckeck=0
#注：这个你cd /mnt/cdrom/可以看到这个key，这里仅仅是个例子
gpgkey=file:///mnt/cdrom/RPM-GPG-KEY-CentOS-7
```
                   
5. 测试：
```bash
yum clean all
yum install vim*
```