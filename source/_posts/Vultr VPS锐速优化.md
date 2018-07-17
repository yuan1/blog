title: Vultr VPS锐速优化
date: 2018-2-16 10:8:34
tags: Linux
---
   * Vultr服务器测试了几个，最后决定用日本的，距离大陆近，好像是最近新开的的，直连。
 * 关于锐速，想说的是，不知道为什么，电脑连网速还可以，但是手机用ss连网速超慢，可能是我联通卡的原因，刚开始用的洛杉矶的机房，换了几个都是美国的，手机上用还是不理想，最后ping了一下各个机房，发现日本的速度最快，然后就换了日本机房的服务器，又google原因，因为vultr 是KVM系统的VPS,所以发现了锐速，装了之后网速一路飙升，不排除是日本机房的原因。
 * 安装
	 + wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/serverspeeder/master/serverspeeder-all.sh && bash serverspeeder-all.sh
	  
 * 卸载锐速
	 + chattr -i /serverspeeder/etc/apx* && /serverspeeder/bin/serverSpeeder.sh uninstall -f
	  
  