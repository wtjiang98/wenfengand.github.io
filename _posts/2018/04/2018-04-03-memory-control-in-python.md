---
layout: postcn
title: "python中的内存分配与内存管理"
date: 2018-04-03 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: python
tags: [python]
---

与本文相关的文章：[pythonz中的深浅复制](http://blog.stackoverflow.club/python-deep-shallow-copy)

## 内存分配
与你想象中不同的，尤其是从c转过来的程序员，python是一门动态类型的语言，其对象与引用是分离的，与java相似。
每创建一个对象，都会把该对象存储起来，并把引用返回。

## id()
返回内存地址
```python
a = 1
id(a)
hex(id(a))
```

## 返回对象的引用计数 getrefcount
需要注意的是，当使用某个引用作为参数，传递给getrefcount()时，参数实际上创建了一个临时的引用。因此，getrefcount()所得到的结果，会比期望的多1。
```python
from sys import getrefcount

a = [1, 2, 3]
print(getrefcount(a))

b = a
print(getrefcount(b))
```
## 删除某引用
```python
a = 1
del a
```

## 垃圾回收机制

垃圾回收机制是按阈值启动的，这个阈值可以通过以下代码查看
```pyton
import gc
gc.get_threshold()
```

返回一个元组(700,10,10), 表明阈值为700

## 对象的分代（generation）扫描机制 
刚刚创建的对象式是0代，每次垃圾回收机制启动，都会对0代对象扫描。

如果0代对象经历扫描而存活，会被归类为1代。类似的，1代对象会被归类为2代。

如果0代经过一定次数的垃圾回收，启动对0代和1代的扫描。

如果1代也经历了一定次数的垃圾回收，启动对0, 1, 2的扫描。

## 引用环
引用环指的是对象之间的相互引用。如下代码可以产生引用环。
```python
a = []
b = [a]
a.append(b)

del a
del b
```

Python会复制每个对象的引用计数，比如有两个相互引用的对象a和b，此时a的引用计数我们用gc_ref_a 来表示，同理用gc_ref_b 来表示b的引用计数，然后Python会遍历所有的引用对象，这里只有a和b，遍历到a的时候，a指向b，将 b的gc_ref_b的值减1，同理遍历b的时候将a的gc_ref_a的值减1，结果他们的值都为0，最后将不为0的对象保留，为0 的对象进行垃圾回收。