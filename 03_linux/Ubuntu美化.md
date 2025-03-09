

Ubuntu 入门到精通

# 给用户root权限

sudo usermod -aG sudo <用户名>

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
sudo apt-get install -f
```

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

## 代码字体

```
tar -xJvf Meslo.tar.xz
sudo mkdir /usr/local/share/fonts/Meslo
sudo mv MesloLG* /usr/local/share/fonts/Meslo
sudo fc-cache -fv
```

# typora 破解

#### <2>.下载Yporaject

```
# git clone https://github.com/hazukieq/Yporaject.git

```

#### <3>.配置rust编译环境

```
1.使用官方脚本安装
# curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

2.检查cargo是否安装
# cargo --version
cargo 1.65.0

```

#### <4>.编译Yporaject

```
# cd Yporaject

1.编译
# cargo build

2.查看在target中是否生成：node_inject
# ls target/debug

3.执行以下命令
# cargo run

```

#### <5>.拷贝target/debug的bin文件到/usr/share/typora目录

```
# sudo cp target/debug/node_inject /usr/share/typora
# cd /usr/share/typora
# sudo chmod +x node_inject
# sudo ./node_inject

```

#### <6>.获取激活码

```
# cd Yporaject/license-gen

1.编译生成激活码的代码
# cargo build

2.生成激活码
# cargo run
output:
    Finished dev [unoptimized + debuginfo] target(s) in 0.00s
     Running `target/debug/license-gen`
License for you: xxxxxx-xxxxxx-xxxxxx-xxxxxx

```

# ESP32 

```
1、安装各种必要的工具
sudo apt-get install git wget flex bison gperf python3-pip python3-venv cmake ninja-build ccache libffi-dev libssl-dev dfu-util libusb-1.0-0 net-tools

2、新建esp32目录
mkdir esp32
cd esp32

3、拉取gitee工具
git clone https://gitee.com/EspressifSystems/esp-gitee-tools.git

4、执行gitee工具切换镜像脚本
cd esp-gitee-tools
./jihu-mirror.sh set

5、拉取esp-idf源码
cd ..
git clone --recursive https://github.com/espressif/esp-idf.git

6、切换esp-idf版本分支到v5.2
cd esp-idf
git checkout v5.2
git submodule update --init --recursive
如果提示失败或有错误试下这句：../esp-gitee-tools/submodule-update.sh

7、更换pip源
pip config set global.index-url http://mirrors.aliyun.com/pypi/simple
pip config set global.trusted-host mirrors.aliyun.com

8、安装编译工具
../esp-gitee-tools/install.sh

9、设置环境变量并将环境变量放到.bashrc中
source export.sh
echo "source ~/esp32/esp-idf/export.sh" >> ~/.bashrc

10、下载课程配套源码
cd ~/esp32
git clone --recursive https://gitee.com/vi-iot/esp32-board.git

11、编译
cd esp32-board/helloworld
idf.py build

12、设置USB串口权限
sudo usermod -aG dialout usrname  usrname需要换成你的用户名

13、重启
```

