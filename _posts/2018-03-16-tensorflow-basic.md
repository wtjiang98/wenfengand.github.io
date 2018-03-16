---
layout: postcn
title: "tensorflow 常用API"
date: 2018-03-16 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: tensorflow
tags: [tensorflow, 机器学习语言]
---


* content 
{:toc} 


主要是通读《TensorFlow实战Google深度学习框架》的记录
<!-- more -->
# 使用计算图
```python
#生成计算图
g1 = tf.Graph()
with g1.as_default():
    v = tf.get_variable(
        "v", initializer = tf.zeros_initializer(shape = [1])
    )

#在计算图中读取变量的值
with tf.Session(graph = g1) as sess:
    tf.global_variables_initializer().run()
    with tf.variable_scope("", reuse = True):
        #这行会输出[0.]
        print(sess.run(tf.get_variable("v")))
#如果有两个计算图，可以通过图的名称给隔离开
```
# 张量的属性
对于代码
```python
result = tf.add(a, b, name = "add")
print result
```
此代码的输出是这样的：
```python
Tensor("add:0", shape=(2,),dtype = float32)
```
- 名字 node:src_output

node是节点名称，src_output是当前张量来自节点的第几个输出

- 维度

shape=(2,)说明是一个一维数组，长度为2

- 类型type

注意tensorflow会检查类型，不指定类型时按照默认类型，如1认为是int32, 1.0认为是float32

# 使用with的区别
第一种会话方式

```python
sess = tf.Session()
sess.run()
sess.close()
```

第二种会话方式
```python
with tf.Session as sess:
    sess.run()
```
推荐第二种方式，不需要显式关闭会话