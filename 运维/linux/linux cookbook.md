## 软件安装
### 安装idea
1. 创建安装目录 mkdir /opt/idea
2. 下载IDEA安装包到这个目录并解压 tar -zxvf  ideaUI-2020.3.2.tar.gz
3. 在桌面创建快捷方式 vi idea.desktop 添加以下内容

``` properties 
[Desktop Entry]
Name=IntelliJ IDEA
Comment=IntelliJ IDEA
Exec=/opt/idea/idea-IC-203.7148.57/bin/idea.sh
Icon=/opt/idea/idea-IC-203.7148.57/bin/idea.png
Terminal=false
Type=Application
```

### 安装中文输入法
1. 安装fcitx5
sudo pacman -S fcitx5 fcitx5-configtool fcitx5-qt fcitx5-gtk fcitx5-chinese-addons
2. 修改环境变量
vim ~/.pam_environment
``` properties
GTK_IM_MODULE DEFAULT=fcitx
QT_IM_MODULE  DEFAULT=fcitx
XMODIFIERS    DEFAULT=@im=fcitx
```
3. 设置登陆后默认启动输入法
vim ~/.xprofile
``` properties
fcitx5 & 
```

## 软件配置
## bash: ll: command not found
问题描述：bash: ll: command not found
问题原因：ll 是 “ls -l”的别名写，是别名，而不是原生自带的，所以在bash里面是找不到这个指令的。
问题解决：bash每次启动时候会添加每个用户下的.bashrc文件，该文件里面时bash的配置
         只需在该配置文件里面加上一句即可alias ll='ls -l',保存后再重新载入source ~/.bashrc
         如果时对于所有用户，则配置文件在/etc/bash.bashrc