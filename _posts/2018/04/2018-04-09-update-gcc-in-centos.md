---
layout: postcn
title: "在centos中更新gcc到6.4.0"
date: 2018-04-08 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: 编程
tags: [yum, centos, gcc]
---

# 博物馆里的gcc
当时需要编译一个github项目，忽然提示我gcc不支持c++11特性，然后看了下gcc版本，竟然是4.8.5？果断升级啊，无奈软件源中似乎没有更新的版本，只能自己下载源码然后编译。

# 从源码编译
在[1]中可以找到详细的编译过程，按照这个过程走下来竟然成功了！所以也没有太多好讲的，只是把其中四个包发出来，这四个软件包的确不容易收集齐。见[2]



Reference:
1. https://www.linuxidc.com/Linux/2017-10/147256.htm
2. 链接: https://pan.baidu.com/s/1DCaAnYRvVOVg2WKQvbzbEQ 密码: es37