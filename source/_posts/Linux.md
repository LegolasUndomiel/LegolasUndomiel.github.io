---
title: Linux
date: 2022-01-23 20:40:04
tags:
---

## EFI引导分区卸载

## Ubuntu镜像源

参考教程[ubuntu20.04更改国内镜像源](https://blog.csdn.net/qq_33706673/article/details/106869016)
参考教程[ubuntu20.04 LTS 更换国内163源、阿里源、清华源、中科大源](https://www.cnblogs.com/zqifa/p/12910989.html)

```bash
# 中科大源
deb https://mirrors.ustc.edu.cn/ubuntu/ focal main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ focal-security main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-security main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse

# 清华源
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse

# 阿里源
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse

# 网易源
deb http://mirrors.163.com/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ focal-security main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ focal-proposed main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ focal-backports main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ focal main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ focal-security main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ focal-updates main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ focal-proposed main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ focal-backports main restricted universe multiverse
```

## DNS

### DNS设置

```bash
sudo vim /etc/systemd/resolved.conf
# 在配置文件中添加DNS信息
DNS=8.8.8.8 114.114.114.114
systemctl restart systemd-resolved
systemctl enable systemd-resolved
 
sudo mv /etc/resolv.conf  /etc/resolv.conf.bak
sudo ln -s /run/systemd/resolve/resolv.conf /etc/
```

### 修改host

```bash
sudo vim /etc/hosts
# github
13.114.40.48    github.com
```

### DNS刷新

```bash
sudo systemd-resolve --flush-caches
```

### 测试网络

```bash
# 测试连接github网络n次
ping github.com -c n
```

## fcitx安装与卸载

### 安装``fcitx``输入法框架

```bash
sudo apt-get install fcitx fcitx-*
```

### 配置fcitx

```bash
# 使用vim编辑
sudo vim /etc/environment
# 添加环境配置，配置文件中不能有回车换行符，因此使用vim换行
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
```

### 完全卸载``fcitx``

```bash
sudo apt-get remove fcitx
sudo apt-get remove fcitx-*
sudo apt-get purge fcitx*
```

### 安装``fcitx5``输入法框架

```bash
sudo add-apt--repository ppa:hosxy/fcitx5
sudo apt install fcitx5 fcitx5-*
```

## Zotero安装

### 下载安装包

[Zotero官网](https://www.zotero.org)

### 解压文件

对于网上直接下载的源码包，最常见的是``.tar.gz``包和``.tar.bz2``包，其解压缩命令分别为：

```bash
tar -zxvf xxx.tar.gz
tar -jxvf xxx.tar.bz2
```

### 创建Zotero文件夹

选择在``/opt/``目录下创建，因为这个目录下通常放``Google Chrome``和``Mozilla Firefox``

```bash
sudo mkdir /opt/zotero
```

### 复制解压文件

```bash
sudo mv Zotero_linux-x86_64/* /opt/zotero/
```

### 更新``zotero``的桌面位置

````bash
cd /opt/zotero
sudo ./set_launcher_icon
````

### 创造软链接到应用程序

```bash
ln -s /opt/zotero/zotero.desktop ~/.local/share/application/zotero.desktop
```

### 安装完成

此时在``Krunner``里面搜索``zotero``即可打开应用

## deb安装包软件安装

### 安装包下载

1. 在[亿图官网](https://www.edrawsoft.cn/)下载适用于Ubuntu系统的``mindmaster``安装包
2. 在[网易云音乐官网](https://music.163.com/)下载适用于Ubuntu系统的``netease-cloud-music``安装包
3. 在[坚果云官网](https://www.jianguoyun.com/)下载适用于Ubuntu系统的``nautilus_nutstore``安装包
4. 在[Edge官网](https://www.microsoft.com/zh-cn/edge)下载适用于Ubuntu系统的``Edge浏览器``安装包
5. 在[Deskreen官网](https://deskreen.com/lang-en)下载适用于Ubuntu系统的``Deskreen``安装包

### 软件安装

```bash
sudo dpkg -i xxx.deb
# 安装依赖
sudo apt-get install -f
```

## apt命令行软件安装

参考教程[PDF阅读器——Zathura](https://zhuanlan.zhihu.com/p/80184476)

```bash
# Zathura轻量级pdf阅读器
sudo apt install zathura
# vim文本编辑器
sudo apt install vim
# neovim文本编辑器
sudo apt install neovim
# neofetch
sudo apt install neofetch
# aria2
sudo apt-get install aria2 -y
# uGet下载器
sudo apt-get install uget -y
```

## UxPlay安装

### 安装依赖

参考以下资料：[CSDN教程](https://blog.csdn.net/sologala/article/details/112852708)、[GStreamer官网](https://gstreamer.freedesktop.org/documentation/installing/on-linux.html?gi-language=c)、[UxPlay百科](https://github.com/antimof/UxPlay)

```bash
sudo apt-get install libgstreamer1.0-0 gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-doc gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio
sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-doc gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio
sudo apt-get install libssl-dev libplist-dev libavahi-compat-libdnssd-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev gstreamer1.0-libav gstreamer1.0-plugins-bad
sudo apt-get install gstreamer1.0-vaapi
sudo apt-get install libx11-dev
```

### 克隆仓库

```bash
cd ~/Downloads/
git clone https://github.com.cnpmjs.org/antimof/UxPlay.git
```

### 编译项目

```bash
cd ~/Downloads/UxPlay
sudo cmake .
sudo make
sudo make install
```

### 配置bash命令

```bash
sudo vim ~/.bashrc
alias uxplay="/usr/local/bin/uxplay"
```

### 运行程序

确定PC和iPad在相同的WiFi环境下，在``bash``里面输入``uxplay``命令后，在iPad中进行连接
