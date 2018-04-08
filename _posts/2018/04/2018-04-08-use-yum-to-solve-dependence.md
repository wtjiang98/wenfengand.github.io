---
layout: postcn
title: "使用yum解决rpm包的依赖性"
date: 2018-04-08 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: 编程
tags: [yum, centos]
---

# 安装rpm包时容易碰到依赖性问题
LibreOffice套件终究还是和MS的不太兼容，比方说表格内文字垂直对齐问题。考虑用WPS暂时替代，但是在下载了rpm包之后直接使用命令`rpm -i ./rpm_package_name`有非常多的依赖包没有安装，一个一个手动安装必然不现实。

# 使用yum做尝试
后来想到yum命令可以自动处理软件的依赖，就尝试了这个命令 `yum install ./rpm_package_name`， 顺利解决各种依赖。