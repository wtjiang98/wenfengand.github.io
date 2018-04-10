---
layout: postcn
title: "configure: error: cannot run C compiled programs"
date: 2018-04-10 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: 编程
tags: [yum, centos, configure,make]
---

# 编译baidupcs项目时碰到问题
执行./configure出现以下错误

configure: error: cannot run C compiled programs.

# 解决方案
指定host类型
```sh
./configure --host=x86_64
```