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

Reference：
1. https://blog.csdn.net/eric_sunah/article/details/56484912