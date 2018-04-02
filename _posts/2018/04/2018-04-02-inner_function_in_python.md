---
layout: postcn
title: "python中的内置函数"
date: 2018-04-02 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: python
tags: [python]
---

## lambda

简短的函数定义
```python
function_my = lambda arg : arg + 1

result = function_my(123)
```
## map

对列表中的每一项都做同样的操作
```python
li = [11, 22, 33]
sl = [1, 2, 3]
new_list = map(lambda a, b: a + b, li, sl)
```

Reference:
1. https://www.cnblogs.com/guigujun/p/6134828.html