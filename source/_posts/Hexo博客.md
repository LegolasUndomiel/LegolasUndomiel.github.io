---
title: Hexo博客
date: 2022-01-29 19:00:44
tags:
---

## Hexo环境安装

### Kubuntu(Linux)下环境安装

参考教程[在Linux系统中搭建hexo博客](https://blog.csdn.net/weixin_43916597/article/details/88090351)
参考教程[Hexo升级与问题排除](https://blog.h1msk.cc/)

```bash
# 安装nodejs
sudo apt-get install nodejs
# 检查是否安装成功
nodejs -v
# 安装npm
sudo apt-get install npm
# 安装hexo
sudo npm install -g hexo
# 问题排除 更新系统
sudo apt update
sudo apt -y upgrade
# 添加仓库
sudo apt update
sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
# 更新nodejs
sudo apt -y install nodejs
# 在博客文件夹内
sudo npm install
```

## 推送博客脚本

```bash
# deploy.sh
for i in {1..10}
do
    hexo clean
    hexo g
    hexo d
done
```

执行脚本命令行

```bash
chmod +777 ./deploy.sh
./deploy.sh
```
