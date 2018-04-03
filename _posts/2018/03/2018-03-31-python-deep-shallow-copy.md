---
layout: postcn
title: "python中的深复制与浅复制"
date: 2018-03-31 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: python
tags: [python]
---

*所有的bug，都是你的预期与实际不相符造成的。换句话说，就是读书太少*

***

与本文相关的文章： [python的内存管理](blog.stackoverflow.club/memory-control-in-python)

在使用python对数据对预处理，比如归一化、去噪时，发现处理后的数据会有诡异的
现象，比如全部都是一样的，或者某些都是一样的。

调查了一番之后，发现这是由于python中的深浅复制造成的。其实，归根结底这与python中的内存分配与管理方式有关。

下面对不同的复制做出结论。

## 直接引用
类似于`a=[1,2,3] b = a`, 这样的都是直接引用，b的值会随着a值的变动而变动

## 切片复制
切片复制主要是`a=[1, 2, 3] b=a[:]`, 当被复制的对象内部只是基本类型而没有嵌套类型时，切片复制可以实现两个对象的隔离。

注意，嵌套类型指的是列表中还有列表，字典中嵌套列表等等复杂类型。

## 浅复制
指的是`b = copy.copy(a)`的情况，对简单类型有用

## 深复制
指的是`b = copy.deepcopy(a)`的情况，就是你所想象的两个对象互不影响的复制。

## 完整测试
```python
#encoding:utf-8
import numpy as np 
import copy
a = [1, 2 , 3, [4, 5]]
reference_a = a 
slice_copy_a = a[:]
shallow_copy_a = copy.copy(a)
deep_copy_a = copy.deepcopy(a)

# print original
print('Original a is\t\t ', a)
# 修改a的基本元素
a[0] = 100
# 修改a的复杂元素
a[3][0] = 1000

print('Now a is \t\t', a)
print('reference_a is\t\t', reference_a)
print('shallow copy is\t\t ', shallow_copy_a)
print('slice copy is \t\t', slice_copy_a)
print('deep copy is \t\t', deep_copy_a)
```

Reference:
1. http://python.jobbole.com/82294/