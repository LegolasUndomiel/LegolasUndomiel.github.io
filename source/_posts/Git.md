---
title: Git
date: 2022-03-13 16:20:26
tags:
---

[Git教程-廖雪峰](https://www.liaoxuefeng.com/wiki/896043488029600)

## 初始化设置

```bash
# 设置用户名
git config --global user.name <UserName>
# 设置用户邮箱
git config --global user.email <UserEmail>
# 生成SSH公钥密钥
ssh-keygen -t rsa -C <UserEmail>
# 初始化本地仓库
git init
```

- ``--global``选项表明这是全局仓库设置，不使用该选项可以给单个仓库单独设置用户名、用户邮箱
- 初始化本地仓库后，会在当前文件夹生成``.git``隐藏文件夹，``.git``是本地仓库，当前文件夹是工作区，需要使用git进行版本管理的代码要放在当前文件夹或子文件夹里。

## 建立仓库

## 分支操作

## 标签操作

```bash
# 添加标签
git tag -a <TagName>
# 推送单个标签
git push origin <TagName>
# 推送全部标签
git push origin --tags
```

- ``-a``选项代表``创建一个带注解的标签``，执行该命令时，``Git``会打开文本编辑器，填写标签的注解，就像给提交写注解一样
- 不使用``-a``选项也可以，但``Git``不会记录这标签是啥时候打的，谁打的，也不会让你添加个标签的注解

## git原理
