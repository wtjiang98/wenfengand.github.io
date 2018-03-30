---
layout: postcn
title: "基本python debug使用"
date: 2018-03-27 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: 纯命令行开发
tags: [python]
---
python pdb 使用
<!-- more -->

*使用命令 python -m pdb your_py_file 进入调试界面，输入 help pdb可以查询完整帮助信息*
## 执行命令行debug
```sh
python -m pdb your_python_script
```

## 常用命令
命令 | 功能
-----| ----
break 或 b n  |	设置断点
b           | 显示断点编号
disable n   |   失能第n个断点
cl n        |    删除第n个断点
continue 或 c	| 继续执行程序, 或是跳到下个断点
list 或 l file:n | 	查看当前行的代码段, 指定文件的指定行
jump 或 j | 跳过指定行，中间代码不执行，跳转后继续运行直到断点处
step 或 s |	进入函数
return 或 r |	执行代码直到从当前函数返回
exit 或 q |	中止并退出
next 或 n	| 执行下一行
p 或!	 | 打印变量的值，例如p a
help 或 h	| 帮助


## 条件断点
1. 在设置断点时指定条件
```sh
b file:line_number, your_condition
# for example
b 10, i==8 
```
1. 先设置普通断点, 再设置条件
```sh
b line_number
```
```sh
condition your_condition
```

## 条件断点的组合
- 与条件
`condition i==8 and j==8`

*Note* 条件可以设置为condition i=2, 注意中间没有if， condition if i==2是错误的，但是设置通过，没有错误没有警告，只是无法正常执行条件断点
## 使用调试脚本
在当前目录下创建.pdbrc文件，文件里面是调试脚本。加载pdb时会首先执行里面的命令。
原始的帮助信息如下
```
If a file ".pdbrc" exists in your home directory or in the current
directory, it is read in and executed as if it had been typed at the
debugger prompt.  This is particularly useful for aliases.  If both
files exist, the one in the home directory is read first and aliases
defined there can be overridden by the local file.
```
似乎是为了支持别名而不是为了使能调试脚本，不管了，可以使用调试脚本就可以

以下是我测试用的调试脚本
```sh
b 10 , i==8 and j==8
c 
!print('i is ', i)
!print('j is ', j)
q
```
脚本中出现`!`前缀的，表明是python代码，用来和普通的调试指令区分开

另外，`.pdbrc`文件并不是说文件名后缀是`.pdbrc`，而是整个文件名。

windows系统下无法创建该文件的话，请使用`git bash`脚本工具



Reference：
1. https://blog.csdn.net/eric_sunah/article/details/56484912