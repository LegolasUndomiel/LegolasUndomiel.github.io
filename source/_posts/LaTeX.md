---
title: LaTeX
date: 2022-01-19 20:06:35
tags:
---
## TeX Live编译环境配置

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
texcount -inc -ch -1 file
```
