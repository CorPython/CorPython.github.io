---
title: "Sublime Text 3搭建c/c++编译运行环境"
date: 2020-01-07T16:06:27+08:00
draft: false
toc: false
isCJKLanguage: true
categories: ["软件配置"]
tags: ["c++","c","环境"]
---

## 前言

我配置的c/c++环境主要是为了写一些简单的算法或者小程序,看重的是`Sublime Text 3`的`轻量`,`启动速度快`,其次你必须先将自己的`cmd`设置为默认`utf-8`编码,这样做主要是为了防止一些编码问题,如果你习惯使用`GBK`编码,<span style='color:red'>请不要看下面的配置 ! ! !</span>

## 设置cmd为默认UTF-8

使用快捷键`win + r`,输入`regedit`,在下面的箭头中所值的位置输入

```sh
计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Command Processor
```

![](https://cdn.jsdelivr.net/gh/CorPython/images@master/img/20200107161642.png)

点击右键-新建，选择`字符串值`。命名为`autorun` 点击右击修改，数值数据填写`chcp 65001`，确定即可

## 配置c/c++环境

![](https://cdn.jsdelivr.net/gh/CorPython/images@master/img/20200107162145.png)

新建两个配置文件,分别命名为

`g++.sublime-build`和`gcc.sublime-build`

`g++.sublime-build`配置如下:

```
{
    "encoding": "utf-8",
    "working_dir": "$file_path",
    "shell_cmd": "g++ -Wall -std=c++11 \"$file_name\" -o \"$file_base_name\"",
    "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
    "selector": "source.c++",
 
    "variants": 
    [
        {   
        "name": "Run in Sublime",
            "shell_cmd": "g++ -Wall -std=c++11 \"$file_name\" -o \"$file_base_name\" && cmd /c \"${file_path}/${file_base_name}\""
        },
        {   
        "name": "Run in CMD",
            "shell_cmd": "g++ -Wall -std=c++11 \"$file\" -o \"$file_base_name\" && start cmd /c \"chcp 65001 & cls & \"${file_path}/${file_base_name}\" & pause\""
        },
        {   
        "name": "gdb Debug",
            "shell_cmd": "g++ -g -std=c++11 \"$file\" -o \"$file_base_name\" && start cmd /c gdb ${file_path}/${file_base_name} & pause"
        }
    ]
}
```

`gcc.sublime-build`配置如下:

```
{
    "encoding": "utf-8",
    "working_dir": "$file_path",
    "cmd": "gcc -Wall \"$file_name\" -o \"$file_base_name\"",
    "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
    "selector": "source.c",
 
    "variants": 
    [
        {   
        "name": "Run in Sublime",
            "shell_cmd": "gcc -Wall \"$file\" -o \"$file_base_name\" && cmd /c \"${file_path}/${file_base_name}\""
        },
        {   
        "name": "Run in CMD",
            "shell_cmd": "g++ -Wall -std=c++11 \"$file\" -o \"$file_base_name\" && start cmd /c \"chcp 65001 & cls & \"${file_path}/${file_base_name}\" & pause\""
        },
        {   
        "name": "gdb Debug",
            "shell_cmd": "gcc -Wall \"$file\" -o \"$file_base_name\" && start cmd /c gdb ${file_path}/${file_base_name} & pause"
        }

    ]
}
```

**关闭软件,重启即可生效**

使用快捷键`ctrl + shift + B`编译运行,如下图:

<span style='color:red'>如果你使用的是win10自带的输入法,请修改编译的快捷键,不然会有冲突 ! ! !</span>

![](https://cdn.jsdelivr.net/gh/CorPython/images@master/img/20200107162641.png)

**切换编译环境看下图**

![](https://cdn.jsdelivr.net/gh/CorPython/images@master/img/image-20200107162615494.png)