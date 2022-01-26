---
title: Linux
date: 2022-01-23 20:40:04
tags:
---

## EFI引导分区卸载

## Zotero安装

- 下载安装包
  [Zoterou官网](https://www.zotero.org)
- 解压文件
  对于网上直接下载的源码包，最常见的是``.tar.gz``包和``.tar.bz2``包，其解压缩命令分别为：

  ```bash
  tar -zxvf xxx.tar.gz
  tar -jxvf xxx.tar.bz2
  ``` 

- 创建Zotero文件夹
  选择在``/opt/``目录下创建，因为这个目录下通常放``Google Chrome``和``Mozilla Firefox``

  ```bash
  sudo mkdir /opt/zotero
  ```

- 复制解压n文件到``/opt/zotero``目录下

  ```bash
  sudo mv Zotero_linux-x86_64/* /opt/zotero/
  ```

- 更新``zotero``的桌面位置

  ````bash
  cd /opt/zotero
  sudo ./set_launcher_icon
  ````

- 创造软链接到应用程序

  ```bash
  ln -s /opt/zotero/zotero.desktop ~/.local/share/application/zotero.desktop
  ```

- 安装完成
  此时在``Krunner``里面搜索``zotero``即可打开应用

## UxPlay安装

- 安装依赖

  参考以下资料：[CSDN教程](https://blog.csdn.net/sologala/article/details/112852708)、[GStreamer官网](https://gstreamer.freedesktop.org/documentation/installing/on-linux.html?gi-language=c)、[UxPlay百科](https://github.com/antimof/UxPlay)

  ```bash
  sudo apt-get install libgstreamer1.0-0 gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-doc gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio
  sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-doc gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio
  sudo apt-get install libssl-dev libplist-dev libavahi-compat-libdnssd-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev gstreamer1.0-libav gstreamer1.0-plugins-bad
  sudo apt-get install gstreamer1.0-vaapi
  sudo apt-get install libx11-dev
  ```

- 克隆仓库

  ```bash
  cd ~/Downloads/
  git clone https://github.com.cnpmjs.org/antimof/UxPlay.git
  ```

- 编译项目

  ```bash
  cd ~/Downloads/UxPlay
  sudo mkdir uxplay
  cd ~/Downloads/UxPlay/uxplay
  cmake ..
  make
  sudo make install
  ```

- 移动项目

  ```bash
  sudo mkdir /usr/local/uxplay
  sudo mv ~/Downloads/UxPlay/uxplay/* /usr/local/uxplay/
  ```

- 配置bash命令

  ```bash
  sudo vim ~/.bashrc
  alias uxplay="/usr/local/uxplay/uxplay"
  ```

- 运行程序

  确定PC和iPad在相同的WiFi环境下，在``bash``里面输入``uxplay``命令后，在iPad中进行连接