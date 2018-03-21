---
layout: postcn
title: "python中的星号表达式(starred expresss)"
date: 2018-03-21 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: python
tags: [python]
---

* content 
{:toc} 
星号表达式，有意思的小东西
<!-- more -->
在使用python给图片加噪声时，用到了 np.random.randn()函数，经测试明明可以输入要用的矩阵大小，得到一个随机数矩阵的，但是一运行就报错，
`TypeError: 'tuple' object cannot be interpreted as an integer`， 搜索这条错误信息没有什么结果。


随后，仔细观察我的代码与例程的不同，发现有个星号的差异。在命令行输入(4,5)得到(4,5), 而输入*(4,5)就得到了错误`SyntaxError: can't use starred expression here`. 

继续搜索，发现星号表达式的作用是在传递形参时，把列表中的各个元素取出来。比如需要两个参数 d1, d2, 但是传入（d1, d2）是不对的， 需要用星号把带括号的(d1, d2)解析出来。