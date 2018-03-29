---
layout: postcn
title: "基础的python函数备忘"
date: 2018-03-23 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: python
tags: [ python]
---

basic python functions
<!-- more -->

## range
```python
# 返回左开右闭
for i in range(1, 4):
    print(i)
```
```sh
1
2
3
```
## list
list的index从0开始，这点要和matlab区分开

## with
with的作用：打开一个文件或者session后自动关闭，不需要手动关闭。

另外，在with中定义的变量在with外依旧可见

## 格式化输出
1. 使用百分号
```python
print('hello %s%.4f' %('str', 5.0))
```
2. 使用format
```python
print('hello {:.4f}/{:.5f} {}'.format(5,6,'str'))
```