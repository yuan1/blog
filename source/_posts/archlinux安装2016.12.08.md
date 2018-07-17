title: archlinux安装2016.12.08
date: 2017-5-12 5:14:32
tags: Linux
---
  自己整理的ArchLinux安装用到的命令
---------------------

 * 网络配置

 
	 + 手动指定：
	
	 ip link set enp1s0 up  
	ip addr add 192.168.1.2/24 dev enp1s0  
	ip route add default via 192.168.1.1  
	 
	 + 设置DNS  
	nano /etc/resolv.conf
	
	 
	  
 * 更新系统时间  
timedatectl set-ntp true

 
 * 分区  
cfdisk
 * 格式化分区

 对于普通分区:mkfs.ext4 /dev/sdXY  
对于swap分区:mkswap /dev/sdXS  
对于EFI分区:mkfs.vfat -F32 /dev/sdXE  
 
 * 挂载分区

 挂载/分区:mount /dev/sdXR /mnt  
挂载EFI分区:mkdir -p /mnt/boot;mount /dev/sdXE /mnt/boot  
挂载home分区:mkdir -p /mnt/home;mount /dev/sdXH /mnt/home  
激活swap分区:swapon /dev/sdXS  
 
 * 选择镜像  
编辑 /etc/pacman.d/mirrorlist，选择您的首选 mirror. 这个 mirror 列表也将通过 pacstrap 被复制并保存在到系统中，所以请确保设置正确。

 
 * 安装基本系统  
pacstrap -i /mnt base base-devel
 * 生成分区信息  
genfstab -U -p /mnt > /mnt/etc/fstab
 * chroot进新系统  
arch-chroot /mnt /bin/bash
 * Locale  
本地化的程序与库若要本地化文本，都依赖 Locale, 后者明确规定地域、货币、时区日期的格式、字符排列方式和其他本地化标准等等。/etc/locale.gen是一个仅包含注释文档的文本文件，要指定您需要的本地化类型，只需移除对应行前面的注释符号（＃）即可：nano /etc/locale.gen  
en\_US.UTF-8 UTF-8  
zh\_CN.UTF-8 UTF-8  
zh\_TW.UTF-8 UTF-8  
 
  接着执行locale-gen以生成locale讯息：  
locale-gen  
创建 locale.conf 并提交您的本地化选项：  
echo LANG=en\_US.UTF-8 > /etc/locale.conf

  * 设置时间

 ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime  
hwclock --systohc --utc  
 
 * 主机名  
要设置 hostname，将其添加 到 /etc/hostname, myhostname 是需要的主机名:  
echo myhostname > /etc/hostname  
建议添加对应的信息到hosts:

 /etc/hosts  
127.0.0.1 localhost.localdomain localhost  
::1 localhost.localdomain localhost  
127.0.1.1 myhostname.localdomain myhostname  
 
 * Initramfs  
如果修改了 mkinitcpio.conf，用以下命令创建一个初始 RAM disk：  
mkinitcpio -p linux

 
 * Root 密码  
passwd
 * 安装引导程序  
bootctl --path=/boot update

 nano /boot/loader/entries/arch.conf  
title Arch Linux  
linux /vmlinuz-linux  
initrd /initramfs-linux.img  
options root=/dev/sda2 rw  
 
 * 退出chroot  
exit

 
    * 添加用户  
首先添加一个用户，并把它加到wheel组：useradd -m -G wheel -s /bin/bash [用户名]  
然后为这个用户设置密码：passwd [用户名]  
最后设置wheel组的用户能用sudo获取root权限，使用visudo来修改sudo的配置：visudo  
找到这样的一行,把前面的#去掉，然后按ESC键，输入:x!回车就可以保存并退出：#%wheel ALL=(ALL) ALL

 
 * bash-completion  
这个软件能够增强bash的Tab自动补全功能，方便我们输入命令：sudo pacman -S bash-completion

 
 * 添加archlinuxcn源  
archlinuxcn是一个由arch中文社区维护的镜像源，其中包含了许多官方镜像中没有但又经常使用的软件。可以通过编辑pacman.conf文件来添加archlinuxcn源:sudo nano /etc/pacman.conf  
在文档结尾处加入下面的文字：

 [archlinuxcn]  
SigLevel = Optional TrustAll  
Server = http://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch  
 
  完成之后刷新pacman数据库  
sudo pacman -Syy  
安装archlinuxcn-keyring，这个是提供校验软件包的密钥的。  
sudo pacman -S archlinuxcn-keyring  
现在archlinuxcn源就可以使用了。

  * .安装yaourt  
yaourt相当于一个加强版的pacman，在pacman的基础上添加了对AUR的支持，并提供诸如彩色输出、交互式搜索模式等一系列实用功能。  
yaourt包含在archlinuxcn源中，所以我们直接用pacman安装即可:  
sudo pacman -S yaourt  
至于yaourt的好处以后就可以体验到了。
 * 安装图形界面  
首先安装xorg-server，这是图形界面的基础。sudo pacman -S xorg-server  
然后安装对应的驱动程序:sudo pacman -S xf86-video-intel xf86-video-ati  
安装Kde桌面:sudo pacman -S plasma kdebase sddm  
删除媒体中心:sudo pacman -R plasma-mediacenter  
为了让我们开机时能够进入图形界面，还需要把显示管理器ssdm设置为开机启动。  
sudo systemctl enable sddm
 * 安装中文字体  
sudo pacman -S adobe-source-han-sans-cn-fonts adobe-source-han-sans-tw-fonts wqy-zenhei wqy-microhei ttf-freefont
  