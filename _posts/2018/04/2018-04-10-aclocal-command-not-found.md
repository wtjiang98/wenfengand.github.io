---
layout: postcn
title: "'aclocal-1.15' is missing on your system."
date: 2018-04-10 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: 编程
tags: [yum, centos, configure, aclocal]
---

# 编译出错
```
WARNING: 'aclocal-1.15' is missing on your system.
         You should only need it if you modified 'acinclude.m4' or
         'configure.ac' or m4 files included by 'configure.ac'.
         The 'aclocal' program is part of the GNU Automake package:
         <http://www.gnu.org/software/automake>
```

# 解决方案
无法通过yum install 下载对应的程序

在提示给出的网址中下载automake软件包，依次 `./configure` `make` `make install`后，错误消失。