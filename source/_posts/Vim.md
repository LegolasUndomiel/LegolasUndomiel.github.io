---
title: Vim
date: 2022-02-04 18:59:24
tags:
---

## Visual Studio Code中使用Vim插件

### 插件配置

```json
/*----------------------------------------------------------------*/
/* Vim
/*----------------------------------------------------------------*/
  "vim.autoSwitchInputMethod.enable": true,
  "vim.autoSwitchInputMethod.defaultIM": "1",
  "vim.autoSwitchInputMethod.obtainIMCmd": "/usr/bin/fcitx-remote",
  "vim.autoSwitchInputMethod.switchIMCmd": "/usr/bin/fcitx-remote -t {im}",
```
