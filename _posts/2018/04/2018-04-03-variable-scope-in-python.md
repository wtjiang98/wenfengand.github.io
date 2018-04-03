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
与本文相关的其他文章：
1. [python的内存管理与垃圾回收](http://blog.stackoverflow.club/memory-control-in-python)
2. [python的深浅复制](http://blog.stackoverflow.club/python-deep-shallow-copy)

## 没有代码块作用域
```python
for x in range(5):
    b = x
print(b)

#output 
# 4
```

## 函数作为作用域分割
总结为：
1. 函数内部变量是隐藏的，其他函数不可访问的
2. 函数可以访问外部的，非其他函数的变量
3. 嵌套函数，底层函数可以访问上一层函数的变量，反之不行。
```python
name = 'b'
def function_my():
    name = 'a'

print(name)
#输出
#b
```