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