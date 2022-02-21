---
title: LaTeX
date: 2022-01-19 20:06:35
tags:
---
## TeX Live编译环境安装与卸载

参考教程[Installing Texlive Latest Version on Ubuntu](https://fahim-sikder.github.io/post/installing-texlive-latest-ubuntu/)
参考教程[Linux(Ubuntu)配置TeX Live2021-知乎专栏](https://zhuanlan.zhihu.com/p/370950462)
参考教程[在Ubuntu(Linux)下配置Latex环境](https://blog.csdn.net/Zhang_Pro/article/details/106988187)
参考教程[Linux系统下安装texlive](https://blog.csdn.net/qq_46753404/article/details/116240081)

### 完全卸载TeX Live编译环境

```bash
sudo apt-get purge texlive*
sudo rm -rf /usr/local/texlive/*
sudo rm -rf ~/.texlive*
sudo rm -rf /usr/local/share/texmf
sudo rm -rf /var/lib/texmf
sudo rm -rf /etc/texmf
sudo apt-get remove tex-common --purge
sudo rm -rf ~/.texlive
```

### 安装依赖

```bash
sudo apt install perl-tk
```

### 下载镜像安装版

在[LaTeX官网](https://www.latex-project.org/)通过国内镜像网站下载``iso``镜像安装包

### 挂载镜像文件

```bash
sudo mount -o loop texlive.iso /mnt
```

### 安装TeX Live

```bash
cd /mnt
sudo ./install-tl
```

### 卸载镜像文件

```bash
sudo umount /mnt
```

### 添加环境变量

```bash
sudo vim ~/.bashrc
# 添加环境变量至配置文件
export PATH=/usr/local/texlive/2021/bin/x86_64-linux:$PATH
export MANPATH=/usr/local/texlive/2021/texmf-dist/doc/man:$MANPATH
export INFOPATH=/usr/local/texlive/2021/texmf-dist/doc/info:$INFOPATH3
```

### 字体配置

```bash
sudo cp /usr/local/texlive/2021/texmf-var/fonts/conf/texlive-fontconfig.conf /etc/fonts/conf.d/09-texlive.conf
sudo fc-cache -fv
sudo apt-get install texlive-lang-chinese
sudo apt-get install texlive-latex-base texlive-latex-extra texlive-latex-recommended texlive-fonts-recommended
# 重启电脑
sudo shutdown -r
```

### TeX Studio安装

```bash
sudo apt-get install texstudio
```

## TeX Live环境配置

### Windows环境Visiual Studio Code

```json
/*----------------------------------------------------------------*/
/* LaTeX Workshop
/*----------------------------------------------------------------*/
  "latex-workshop.showContextMenu": false,
  "latex-workshop.intellisense.package.enabled": true,
  "latex-workshop.message.error.show": true,
  "latex-workshop.message.warning.show": false,
  "latex-workshop.latex.outDir": "./Auxiliary",
  "latex-workshop.latex.tools": [
    {
      "name": "xelatex",
      "command": "xelatex",
      "args": [
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "-pdf",
        "--output-directory=%OUTDIR%",
        "%DOCFILE%"
      ]
    },
    {
      "name": "pdflatex",
      "command": "pdflatex",
      "args": [
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "--output-directory=%OUTDIR%",
        "%DOCFILE%"
      ]
    },
    {
      "name": "bibtex",
      "command": "bibtex",
      "args": ["%OUTDIR%/%DOCFILE%"],
      "env": {"TEXMFOUTPUT":"%OUTDIR%",}
    },
    {
      "name": "biblatex",
      "command": "biber",
      "args": ["%OUTDIR%/%DOCFILE%"],
      "env": {"TEXMFOUTPUT":"%OUTDIR%",}
    }
  ],
  "latex-workshop.latex.recipes": [
    {
      "name": "xelatex",
      "tools": ["xelatex","xelatex"]
    },
    {
      "name": "pdflatex",
      "tools": ["pdflatex","pdflatex"]
    },
    {
      "name": "xelatex -> bibtex -> xelatex*2",
      "tools": ["xelatex","bibtex","xelatex","xelatex"]
    },
    {
      "name": "xelatex -> biblatex -> xelatex*2",
      "tools": ["xelatex","biblatex","xelatex","xelatex"]
    },
    {
      "name": "pdflatex -> bibtex -> pdflatex*2",
      "tools": ["pdflatex","bibtex","pdflatex","pdflatex"]
    },
    {
      "name": "pdflatex -> biblatex -> pdflatex*2",
      "tools": ["pdflatex","biblatex","pdflatex","pdflatex"]
    }
  ],
  "latex-workshop.view.pdf.viewer": "external",
  "latex-workshop.view.pdf.internal.synctex.keybinding": "ctrl-click",
  "latex-workshop.view.pdf.ref.viewer": "external",
  "latex-workshop.view.pdf.external.viewer.command": "C:/SumatraPDF/SumatraPDF.exe",
  "latex-workshop.view.pdf.external.viewer.args": ["%PDF%"],
  "latex-workshop.view.pdf.external.synctex.command": "C:/SumatraPDF/SumatraPDF.exe",
  "latex-workshop.view.pdf.external.synctex.args": [
    "-forward-search",
    "%TEX%",
    "%LINE%",
    "-reuse-instance",
    "-inverse-search",
    "\"C:/Microsoft VS Code/Code.exe\" \"C:/Microsoft VS Code/resources/app/out/cli.js\" -r -g \"%f:%l\"",
    "%PDF%"
  ],
  "latex-workshop.latex.autoClean.run": "onBuilt",
  "latex-workshop.latex.clean.fileTypes": [
    "*.aux",
    "*.bbl",
    "*.blg",
    "*.idx",
    "*.ind",
    "*.lof",
    "*.lot",
    "*.out",
    "*.toc",
    "*.acn",
    "*.acr",
    "*.alg",
    "*.glg",
    "*.glo",
    "*.gls",
    "*.ist",
    "*.fls",
    "*.log",
    "*.fdb_latexmk",
    "*.nav",
    "*.snm",
    "*.vrb",
    "*.bcf",
    "*.xml"
  ],
  "latex-workshop.latex.recipe.default": "lastUsed",
  "latex-workshop.latex.autoBuild.cleanAndRetry.enabled": true,
  "latex-workshop.latex.autoBuild.run": "never",
```

## 统计字数

使用宏包texcount可以统计文档字数，其官方网站上有详细的documentation，介绍所有的可选项及其含义，详情见[texcount官网](https://app.uio.no/ifi/texcount/)
**常用命令：**

```bash
# 详细字数统计信息
texcount -inc -ch file
# 简略字数统计信息
texcount -inc -ch -1 file
```
