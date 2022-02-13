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
  "vim.handleKeys": {
    "<C-f>": false,
    "<C-F>": false,
    "<C-b>": false,
    "<C-w>": false,
    "<C-k>": false,
    "<C-z>": false
  },
  "vim.normalModeKeyBindingsNonRecursive": [
    {
      "before": ["Up"],
      "after": ["Nop"]
    },
    {
      "before": ["Down"],
      "after": ["Nop"]
    },
    {
      "before": ["Left"],
      "after": ["Nop"]
    },
    {
      "before": ["Right"],
      "after": ["Nop"]
    },
  ],
  "vim.insertModeKeyBindings": [
    {
      "before": ["Up"],
      "after": ["Nop"]
    },
    {
      "before": ["Down"],
      "after": ["Nop"]
    },
    {
      "before": ["Left"],
      "after": ["Nop"]
    },
    {
      "before": ["Right"],
      "after": ["Nop"]
    },
  ],
  "vim.visualModeKeyBindings": [
    {
      "before": ["Up"],
      "after": ["Nop"]
    },
    {
      "before": ["Down"],
      "after": ["Nop"]
    },
    {
      "before": ["Left"],
      "after": ["Nop"]
    },
    {
      "before": ["Right"],
      "after": ["Nop"]
    },
  ],
```
