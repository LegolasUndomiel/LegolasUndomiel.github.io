---
title: C/C++
date: 2022-01-23 20:42:41
tags:
---

## GCC/G++编译环境配置

### Windows环境Visiual Studio Code环境配置

### Kubuntu(Linux)环境Visual Studio Code环境配置

```json
// tasks.json配置文件
{
    "version": "2.0.0",
    "tasks": [
        {//这个大括号里是‘构建（build）’任务
            "label": "build", //任务名称，可以更改，不过不建议改
            "type": "shell", //任务类型，process是vsc把预定义变量和转义解析后直接全部传给command；shell相当于先打开shell再输入命令，所以args还会经过shell再解析一遍
            "command": "g++", //编译命令，这里是gcc，编译c++的话换成g++
            "args": [    //方括号里是传给gcc命令的一系列参数，用于实现一些功能
                "${file}", //指定要编译的是当前文件
                "-o", //指定输出文件的路径和名称
                "${fileDirname}/bin/${fileBasenameNoExtension}.out", //承接上一步的-o，让可执行文件输出到源码文件所在的文件夹下的bin文件夹内，并且让它的名字和源码文件相同
                "-g", //生成和调试有关的信息
                "-Wall", // 开启额外警告
                "-static-libgcc",  // 静态链接libgcc
                "-std=c++11", // 语言标准，可根据自己的需要进行修改，写c++要换成c++的语言标准，比如c++11
            ],
            "group": {  //group表示‘组’，我们可以有很多的task，然后把他们放在一个‘组’里
                "kind": "build",//表示这一组任务类型是构建
                "isDefault": true//表示这个任务是当前这组任务中的默认任务
            },
            "presentation": { //执行这个任务时的一些其他设定
                "echo": true,//表示在执行任务时在终端要有输出
                "reveal": "always", //执行任务时是否跳转到终端面板，可以为always，silent，never
                "focus": true,
                "panel": "new" //每次执行这个task时都新建一个终端面板，也可以设置为shared，共用一个面板，不过那样会出现‘任务将被终端重用’的提示，比较烦人
            },
            "problemMatcher": "$gcc" //捕捉编译时编译器在终端里显示的报错信息，将其显示在vscode的‘问题’面板里
        },
        {//这个大括号里是‘运行(run)’任务，一些设置与上面的构建任务性质相同
            "label": "run", 
            "type": "shell", 
            "dependsOn": "build", //任务依赖，因为要运行必须先构建，所以执行这个任务前必须先执行build任务，
            "command": "${fileDirname}/bin/${fileBasenameNoExtension}.exe", //执行exe文件，只需要指定这个exe文件在哪里就好
            "group": {
                "kind": "test", //这一组是‘测试’组，将run任务放在test组里方便我们用快捷键执行
                "isDefault": true
            },
            "presentation": {
                "echo": true,
                "reveal": "always",
                "focus": true, //这个就设置为true了，运行任务后将焦点聚集到终端，方便进行输入
                "panel": "new"
            }
        }
    ]
}
```

```json
// launch.json配置文件
{
    "version": "0.2.0",
    "configurations": [
        {//这个大括号里是我们的‘调试(Debug)’配置
            "name": "Debug", // 配置名称
            "type": "cppdbg", // 配置类型，cppdbg对应cpptools提供的调试功能；可以认为此处只能是cppdbg
            "request": "launch", // 请求配置类型，可以为launch（启动）或attach（附加）
            "program": "${fileDirname}/bin/${fileBasenameNoExtension}.out", // 将要进行调试的程序的路径
            "args": [], // 程序调试时传递给程序的命令行参数，这里设为空即可
            "stopAtEntry": false, // 设为true时程序将暂停在程序入口处，相当于在main上打断点
            "cwd": "${fileDirname}", // 调试程序时的工作目录，此处为源码文件所在目录
            "environment": [], // 环境变量，这里设为空即可
            "externalConsole": false, // 为true时使用单独的cmd窗口，跳出小黑框；设为false则是用vscode的内置终端，建议用内置终端
            "internalConsoleOptions": "neverOpen", // 如果不设为neverOpen，调试时会跳到“调试控制台”选项卡，新手调试用不到
            "MIMode": "gdb", // 指定连接的调试器，gdb是minGW中的调试程序
            "preLaunchTask": "build" // 调试开始前执行的任务，我们在调试前要编译构建。与tasks.json的label相对应，名字要一样
    }]
}
```
