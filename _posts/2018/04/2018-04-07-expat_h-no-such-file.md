---
layout: postcn
title: "fatal error: expat.h: No such file or directory"
date: 2018-04-07 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: linux
tags: [linux, make, 编译]
---

编译git时出现如标题中的错误，缺少依赖

```sh
yum install expat-devel
```