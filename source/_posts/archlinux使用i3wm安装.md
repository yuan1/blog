---
title: archlinux使用i3wm安装
date: 2017-11-1 13:31:25
tags: Linux
---
```bash
安装i3窗口管理器  
pacman -S i3  
安装 lightdm 显示管理器，  
pacman -S lightdm-gtk3-greeter  
然后  
systemctl enable lightdm  
systemctl start lightdm  
登陆进i3之后会自动加载配置向导，基本上一路next即可。
安装网络管理器
pacman -S netork-manager-applet  
systemctl enable NetworkManager.service  
systemctl start NetworkManager.service  
```

列个软件包列表，应该都是你需要的
firefox, flashplugin: 浏览器和flash插件  
xfce4-terminal: 我推荐的终端模拟器  
tmux: 你懂的  
nautilus或pcmanfm或nemo: 文件管理器  
rofi: 启动器  
compton: 开透明什么的需要  
pnmixer: 调音量  
gthumb: 看图  
gnome-screenshot, deepin-screenshot: 截图  
lxappearence: 设置主题、外观  
numix-theme, numix-circle-icon-theme-git: 我喜欢的主题和图标，装完用lxappearence设置生效  
nitrogen: 设置壁纸  
conky: 系统状态监视  
xfce4-power-manager: 电源管理  
mate-notification-daemon: 桌面通知  
还有好多日常软件日后慢慢告诉你…

拷贝配置文件
把旧系统中，/home/yooo/里的以下文件拷到现在的$HOME对应的位置里:
.bashrc: Shell配置  
.xprofile: 进入X时的环境文件  
.i3/*: i3的配置文件  
.vimrc, .vim/: vim配置文件  
.tmux.conf: tmux配置文件  
.fonts/: 一些字体  
.config/fontconfig/: 字体配置  
其他的，例如壁纸之类，看着拷回来就是了…

```bash
输入法
安装fcitx
pacman -S fcitx-im fcitx-sunpinyin fcitx-cloudpinyin fcitx-configtool  
然后，确保自己的~/.xprofile里有以下三行:
export GTK\_IM\_MODULE=fcitx  
export QT\_IM\_MODULE=fcitx  
export XMODIFIERS="@im=fcitx"  
你的~/.i3/autostart.sh会再启动i3时自动运行fcitx，右键那个图标，把sunpinyin给enable了。
多媒体
播放器和解码器:  
pacman -S gstreamer ffmpeg smplayer  
音频  
pacman -S alsa-utils pulseaudio-alsa  
把自己加到用户组里
gpasswd -a yooo audio  
gpasswd -a yooo video  
一些字体
你现在的字体应该还比较难看，装上这些包:
pacman -S wqy-microhei ttf-dejavu ttf-droid cantarell-fonts adobe-source-han-sans-cn-fonts  
你应该还需要写带中文的文档
pacman -S texlive-most  
yaourt -S acroread-fonts-systemwide  
```

未完待续

 