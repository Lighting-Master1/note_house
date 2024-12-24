Ubuntu 入门到精通

# 1更换软件源

```
sudo gedit /etc/apt/sources.list
```

```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-proposed main restricted universe multiverse
```

## updata

```
sudo apt-get update
sudo apt-get upgrade
```

# 2.设置谷歌输入法

## 安装输入法系统

```
sudo apt-get install fcitx
# 将fcitx.desktop文件复制到开机自启动目录中
# 命令格式: sudo cp "fcitx.desktop文件所在的位置"  "开机自启动目录"
sudo cp /usr/share/applications/fcitx.desktop /etc/xdg/autostart/
sudo apt purge ibus
```

## 安装搜狗依赖工具

```
sudo apt install libqt5qml5 libqt5quick5 libqt5quickwidgets5 qml-module-qtquick2 libgsettings-qt1
```

# 3.Ubuntu 美化

## 安装桌面程序

```
sudo apt install -y gnome-tweaks gnome-shell-extensions
```

打开Gnome官网

```
 extensions.gnome.org
```

插件安装

```
User Themes 
Blur my Shell
Compiz alike magic lamp effect
```

### Big Sur 主题 WhiteSur

 [WhiteSur-gtk-theme](https://github.com/vinceliuice/WhiteSur-gtk-theme/)

```
cd WhiteSur-gtk-theme  # 进入主题目录
./install.sh -t all -N glassy # 运行安装脚本
sudo ./tweaks.sh -g  # 添加主题
```

### Big Sur 应用图标 Mkos-Big

 [Mkos-Big-Sur](https://github.com/zayronxio/Mkos-Big-Sur/)

```
mkdir ~/.icons  # 创建 ~/.icons 目录
tar -xJvf Mkos-Big-Sur.tar.xz -C ~/.icons  # 将图标文件解压到 ~/.icons 目录
```

## Big Sur 字体  

 [San-Francisco-Pro-Fonts](https://github.com/sahibjotsaggu/San-Francisco-Pro-Fonts) 

```
sudo mkdir /usr/local/share/fonts/SF-Pro  # 新建字体文件夹
sudo mv SF-Pro* /usr/local/share/fonts/SF-Pro  # 安装字体
sudo fc-cache -fv  # 刷新字体列表缓存
```

## 文档字体