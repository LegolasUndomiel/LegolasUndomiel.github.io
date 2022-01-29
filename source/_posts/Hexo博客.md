---
title: Hexo博客
date: 2022-01-29 19:00:44
tags:
---

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
