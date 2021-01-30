## 安装idea
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

## 安装中文输入法
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
