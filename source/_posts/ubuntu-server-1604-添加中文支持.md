---
title: ubuntu server 1604 添加中文支持
tags: Blog
originContent: ''
categories:
  - Linux
toc: false
date: 2019-09-25 17:47:00
---

```bash
 sudo apt-get install language-pack-zh-hans

```
安装完后有如下提示：

```bash
Generating locales...
  zh_CN.UTF-8... done
  zh_SG.UTF-8... done
Generation complete.

```

tty的中文方块乱码

默认的tty只能显示一个字节128或256字符，你可以用setfont命令去改tty的字体，但是永远只能局限在1字节。不能支持utf-8多字节，所以我们需要安装fbterm

安装fbterm

```bash
apt-get install fbterm

```

安装中文字体

```bash

文泉驿

apt-get install xfonts-wqy

文泉驿-正黑

apt-get install ttf-wqy-zenhei


```

切换到fbterm控制台

```bash

fbterm

```
