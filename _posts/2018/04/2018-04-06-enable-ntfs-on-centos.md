---
layout: postcn
title: "python中的变量名作用域"
date: 2018-04-03 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: python
tags: [python]
---
新安装的centos并不支持ntfs格式，导致原始机械硬盘和u盘的内容它都无法挂载。这时候需要安装ntfs-3g提供文件系统格式支持。
```sh
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo

yum update;yum install ntfs-3g

yum install ntfs-3g
```