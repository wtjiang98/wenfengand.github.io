---
layout: postcn
title: "vscode无法跳转到定义"
date: 2018-03-07 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: 编译器
tags: [编译器, vscode]
---

# 问题描述

在vscode中没有办法通过 ctrl + 左键 跳转到函数定义，使用的语言为python
<!-- more -->
# 问题解决

google该问题，发现在 [这里][1]有类似issue   
原因在于目录中存在中文字符

  
仔细观察我的目录，其中有一个文件夹使用了连字符，即文件名为 opensource-code, 更改为 opensource_code后问题解决

 [1]: https://github.com/Microsoft/vscode-python/issues/571