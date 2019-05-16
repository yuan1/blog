---
title: CentOS7.6升级openssh-7.9p1
tags: Blog
originContent: ''
categories: []
toc: false
date: 2019-05-16 13:37:22
---

CentOS7.6源码安装openssh-7.9p1

操作系统版本

```
[root@localhost src]# cat /etc/redhat-release 
CentOS Linux release 7.6.1810 (Core) 
```

当前openssh-server版本

```
[root@localhost ~]# rpm -qa | grep openssh
openssh-server-7.4p1-16.el7.x86_64
openssh-7.4p1-16.el7.x86_64
openssh-clients-7.4p1-16.el7.x86_64
```

下载源码包

```
[root@localhost src]# curl -O http://ftp2.fr.openbsd.org/pub/OpenBSD/OpenSSH/portable/openssh-7.9p1.tar.gz
```

解压源码包

```
[root@localhost src]# tar zxvf openssh-7.9p1.tar.gz
```

进入源码目录

```
[root@localhost src]# cd openssh-7.9p1/

```

安装编译工具及依赖包

```
[root@localhost openssh-7.9p1]# yum -y install gcc make openssl-devel pam-devel zlib-devel rpm-build
```

配置

```
[root@localhost openssh-7.9p1]# ./configure --prefix=/usr --sysconfdir=/etc/ssh --with-md5-passwords --with-pam --without-hardening
```

编译源码

```
[root@localhost openssh-7.9p1]# make
```

安装源码

```
[root@localhost openssh-7.9p1]# make install
```
可能会出现报警：

```
ssh-keygen: generating new host keys: DSA 
/usr/sbin/sshd -t -f /etc/ssh/sshd_config
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0640 for '/etc/ssh/ssh_host_rsa_key' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
key_load_private: bad permissions
Could not load host key: /etc/ssh/ssh_host_rsa_key
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0640 for '/etc/ssh/ssh_host_ecdsa_key' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
key_load_private: bad permissions
Could not load host key: /etc/ssh/ssh_host_ecdsa_key
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0640 for '/etc/ssh/ssh_host_ed25519_key' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
key_load_private: bad permissions
Could not load host key: /etc/ssh/ssh_host_ed25519_key
```

要重新生成key，然后make install

cd /etc/ssh然后删除ssh_host前缀的KEY文件
```

ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key

ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key

ssh-keygen -t dsa -f /etc/ssh/ssh_host_ed25519_key

```

拷贝启动脚

```
[root@localhost openssh-7.9p1]# \cp -rf contrib/redhat/sshd.init /etc/init.d/sshd
```

添加到服务管理

```
[root@localhost openssh-7.9p1]# chkconfig --add sshd
```

添加到开机服务

```
[root@localhost openssh-7.9p1]# chkconfig sshd on
```

修改配置文件
```
[root@localhost openssh-7.9p1]# sed -i "32a PermitRootLogin yes" /etc/ssh/sshd_config # 允许root用户远程登录
[root@localhost openssh-7.9p1]# sed -i "83a UsePAM yes" /etc/ssh/sshd_config
```

重启sshd服务

```
[root@localhost openssh-7.9p1]# service sshd restart
```

删除下载的源码包
```
[root@localhost openssh-7.9p1]# cd ../
[root@localhost src]# rm -rf openssh-7.9p1*
```

查看ssh客户端版本，版本已经升级。

```
[root@localhost src]# ssh -V
OpenSSH_7.9p1, OpenSSL 1.0.2k-fips  26 Jan 2017
```

查看sshd位置

```
[root@localhost src]# which sshd
/usr/sbin/sshd
```

查看sshd服务端版本，版本已经升级。

```
[root@localhost src]# strings /usr/sbin/sshd | grep OpenSSH
OpenSSH_7.9
OpenSSH_7.9p1
OpenSSH_2.*,OpenSSH_3.0*,OpenSSH_3.1*
OpenSSH_2*,OpenSSH_3*,OpenSSH_4*
OpenSSH_7.0*,OpenSSH_7.1*,OpenSSH_7.2*,OpenSSH_7.3*,OpenSSH_7.4*,OpenSSH_7.5*,OpenSSH_7.6*,OpenSSH_7.7*
OpenSSH_3.*
OpenSSH_5*
OpenSSH_6.6.1*
OpenSSH_6.5*,OpenSSH_6.6*
OpenSSH*
```

centos7.6升级openssh-7.9p1完成。