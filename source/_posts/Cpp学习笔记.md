---
title: Cpp学习笔记
date: 2022-06-19 21:18:51
tags:
---

## Welcome to C++

- **编译型**：将源代码翻译成机器码，CPU直接运行机器码，运行效率高，兼容多平台，榨干机器所有性能
- **解释型**：源代码翻译为中间码，运行在虚拟机上，运行时进行一些优化
- 举例：英文书翻译为德文or给英文书配备一个翻译

## How to Setup C++ on Windows

- **编译器**：将源代码翻译为二进制码
- Visual Studio插件Visual Assist

## How C++ Works

- 编译器生成的二进制文件可以是 **某种库** or **可执行文件**
- **预处理指令**(**preprocessor**)：例如`#include`，在编译之前，编译器首先处理预处理指令
- `#include`找到文件并复制粘贴
- `main`函数作为程序的入口(entry point)
- **返回类型**(**return type**)
- 运算符就是函数
- **配置**：debug模式和release模式，debug模式下没有开编译优化，相对较慢
- **目标平台**
- cpp文件编译成目标文件(object file)，linker把所有目标文件联系起来生成可执行文件
- 有多个源代码文件，声明(decleration)其他文件的函数存在，编译(compiler)不会寻找函数定义，链接(linker)时会寻找函数定义

## How the C++ Compiler Works

- 将文本文件(text file)编译为中间目标文件(object file)，目标文件是机器码
- pre-process -> tokenizing & parsing
- 编译器将源代码处理为数据和指令，可以自定义编译器、自定义编译规则
- `#define`找到对于字符进行替换
- `#if`条件编译
- release模式下编译时会对代码进行优化
- linker通过目标文件中的函数签名找到具体的函数定义

## How the C++ Linker Works

- 编译时检查语法错误，链接时寻找对应函数定义
- 函数或变量重名时，会出现链接错误(重复定义)，`#include`可能会不小心引起重复
- **解决办法**：`inline`内联函数、`static`静态函数(仅在当前文件函数有效)、头文件里只放函数声明，函数定义放在cpp文件中(头文件的作用相当于快速包含多个声明，不重复写函数声明代码)

## Variables in C++

- C++中不同变量的本质区别是字节大小，即分配的内存大小
- `char`字符、`int`整数、`float`5.5f、`double`、`bool`

## Functions in C++

- **函数**：代码块，设计用来执行特定的任务，类中称为方法(methods)，防止代码重复
- 如果不封装为函数，需要大量复制粘贴代码，同时一些细节会出错，例如`cout << result`中没有修改变量名
- 合理封装代码块，方便维护、提高效率，在调用函数时，需要为函数创建一整个栈(stack frame)，为了执行函数指令在内存中来回跳转，这些需要消耗时间
- 多次执行某个任务，封装成函数
- `main`函数可以不用返回一个值，即省略`return 0;`，实际上这是现代c/c++的特性

## C++ Header Files

- 方便函数声明，使用头文件可以不用每次复制一堆函数声明，只需要`#include`头文件即可
- `#pragma once`防止把多个头文件多次include到一个翻译单元里，`#ifndef`可以实现同样的功能
- `#include`使用引号为相对位置

## How to DEBUG C++ in VISUAL STUDIO


