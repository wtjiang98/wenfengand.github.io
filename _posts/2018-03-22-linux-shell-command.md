---
layout: postcn
title: "常用的linux命令"
date: 2018-03-22 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: linux命令
tags: [shell]
---


最近在使用实验室的gpu 服务器，发现作为普通用户使用服务器还是和特权用户有很大区别的。
<!-- more -->
## 查看显卡信息
```sh
nvidia-smi
```

## 查看cuda版本
```sh
cat /usr/local/cuda/version.txt
```
## 实时查看系统的负载
```sh
top
```
## 查看已经开机的时间
```sh
uptime
```
## 查看已经登录的用户
```sh
w
```
## 统计当前目录下文件的个数

不包括目录
```sh
ls -l | grep "^-" | wc -l
```
## 统计两个文件的异同
1. comm 

comm [OPTION]... FILE1 FILE2

功能说明：比较两个已排过序的文件。（使用sort排序）

语　　法：comm [-123][--help][--version][第1个文件][第2个文件]

补充说明：这项指令会一列列地比较两个已排序文件的差异，并将其结果显示出来，如果没有指定任何参数，则会把结果分成3栏显示：第1栏仅是在第1个文件中出现过的记录，第2栏是仅在第2个文件中出现过的记录，第3栏则是在第1与第2个文件里都出现过的记录。若给予的文件名改为"-"，则comm指令会从标准输入设备读取数据。

参　　数：

  -1   不显示只在第1个文件里出现过的列。

  -2   不显示只在第2个文件里出现过的列。

  -3   不显示只在第1和第2个文件里出现过的列。

  --help   在线帮助。

  --version   显示版本信息。

例子

comm - 12     就只显示在两个文件中都存在的行；

comm - 23    只显示在第一个文件中出现而未在第二个文件中出现的行；

comm - 123  则什么也不显示。

2. diff

主要用来显示txt1 需要做什么改动可以变成txt2.
```sh
diff txt1 txt2
```
简单比较两个文件，输出带箭头的信息

```sh
diff -c txt1 txt2
```
context模式，输出+ - 号，但是会输出很多无关的内容

```sh
diff -u txt1 txt2
```
Unified模式输出，最精简，只用+ -号输出需要改动的地方，git比较文件差异的时候就是这种。
## 解压命令
- .tar 
<br>解包：tar xvf FileName.tar
<br>打包：tar cvf FileName.tar DirName
- .gz
<br>解压1：gunzip FileName.gz
<br>解压2：gzip -d FileName.gz
<br>压缩：gzip FileName
- .tar.gz 和 .tgz
<br>解压：tar zxvf FileName.tar.gz
<br>压缩：tar zcvf FileName.tar.gz DirName
- .bz2
<br>解压1：bzip2 -d FileName.bz2
<br>解压2：bunzip2 FileName.bz2
<br>压缩： bzip2 -z FileName
- .tar.bz2
<br>解压：tar jxvf FileName.tar.bz2
<br>压缩：tar jcvf FileName.tar.bz2 DirName
- .bz
<br>解压1：bzip2 -d FileName.bz
<br>解压2：bunzip2 FileName.bz
<br>压缩：未知
- .tar.bz
<br>解压：tar jxvf FileName.tar.bz
<br>压缩：未知

## 分屏，多个终端
```sh
tmux
```
注意，每次输入控制tmux的命令前，都要先输入 ctrl + b，即同时按下ctrl 和b按键，然后输入指定的控制键。

控制键 | 效果
------| ----
"     | 上下分屏
%     | 左右分屏
pageup | 向上翻页
pagedown | 向下翻页

如果要退出翻页模式，需要按esc， 不用输入ctrl + b

Reference：
1. comm  https://blog.csdn.net/shuckstark/article/details/7872176
2. diff https://www.cnblogs.com/wangqiguo/p/5793448.html
3. tar http://www.cnblogs.com/eoiioe/archive/2008/09/20/1294681.html