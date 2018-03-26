---
layout: postcn
title: "离线的方式安装tensorflow"
date: 2018-03-23 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: tensorflow
tags: [tensorflow, python]
---


有网的情况下安装tensorflow自然舒服，但是总是由于种种原因，我们需要离线安装。比如，保密，gpu服务器联网需要登录账号然而你又没有上网账号等等。
<!-- more -->

## 方法一：使用pip工具

1. 使用pip导出当前环境(和目标机器相同且已经安装好tensorflow)所有依赖包信息文件
```sh
pip freeze > requirements_source.txt
```
2. 使用pip导出目标环境的依赖包（就是你本来打算在哪台机器上装tensorflow）
```sh
pip freeze > requirements_target.txt
```
3. 使用comm命令导出需要下载的包
```sh
comm - 23 requirements_source.txt requirements_target.txt > download.txt
```
comm命令的使用可以参考 http://blog.stackoverflow.club/linux-shell-command.html

4. 下载所有依赖包到本地（只要能上网，可以运行pip命令的机器）
```sh
pip install -r download.txt -d your_download_dir
```
5. 在目标机器上安装所有依赖
```sh
pip install -r download.txt --no-index --find-links=your_download_dir
```

优点：使用比较文件差异的方式, 把已经有的依赖项给去掉，节省时间
<br>缺点：需要有一台和目标机器一模一样的环境，并且还能联网。通常情况下这很难得，比如我就是用一个cpu的requirements.txt装一个gpu的tensorflow, 其中出现了大量问题，比如cuda版本、linux和windows的whl包的差异，还是挺浪费时间的。

## 方法二：使用脚本自动分析依赖
目标设想：
1. 在目标机上导出依赖文件和驱动信息
2. 找到合适tensorflow whl包，使用脚本解析其依赖关系
3. 递归分析2中的所需包的依赖关系，和1中的依赖关系做对比，下载所需要的包
4. 将所需要的包在目标机器上安装
5. 安装tensorflow

*目前依旧在coding中，测试完之后会发出*


Reference:
1. https://www.zhihu.com/question/60431332/answer/345384976