---
layout: postcn
title: "matlab常用api"
date: 2018-03-21 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: matlab
tags: [matlab, api]
---

* content 
{:toc} 
介绍曾经使用过的、且搜索过后才知道怎么用的api
<!-- more -->

## 保存.mat数据
```matlab
save('your_file_name','variable_name')
```
注意variable_name可以有多个，即把多个矩阵保存在一个.mat文件中