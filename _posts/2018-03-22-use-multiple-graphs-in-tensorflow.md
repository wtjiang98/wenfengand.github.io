---
layout: postcn
title: "在tensorflow中用多张图实现网络级联"
date: 2018-03-22 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: tensorflow
tags: [tensorflow, python]
---

* content 
{:toc} 
在一个网络的输入依赖与另一个网络的输出时，就要在tensorflow中同时使用多张图。
<!-- more -->

## 使用多张图的起因
如果没有报错，我是懒得使用多张图的。多张图的报错主要是下面这种。
```python 
Tensor(...) must be from the same graph as Tensor
```

## 简单地避开多张图
刚开始我只是在验证阶段需要网络的级联，数据只需要在这个级联网络流动一次。所以采用了reset方式避开问题。
```python
import tensorflow as tf
(code to define graph one)
(session to run graph one)

tf.reset_default_graph()

(code to define graph two)
(session to run graph two)
```
查询这个 reset_default_graph() 可以发现，函数功能是Clears the default graph stack and resets the global default graph.

## 彻底解决问题
我的网络结构是 去噪自编码网络 + CNN识别网络，在简单避开多图问题后，发现CNN的识别效果不理想。仔细看了看中间结果，认为可能是去噪自编码不够好，把原始信号给扭曲了。所以，CNN可能需要学习去噪自编码的输出。那么在DAE的基础上进行训练，就需要数据频繁大量的在两张图中流动，只使用reset不足以解决问题。 直到在一篇博客中发现了多图的建立方法。
```python
g1 = tf.Graph()
    with g1.as_default():
        (code to define tensors)
g2 = tf.Graph()
    with g2.as_default():
        (code to define tensors)
sess_g1 = tf.Session(graph = g1)
sess_g2 = tf.Session(graph = g2)

# run sess doesn't need as_default function
sess_g1.run()
sess_g2.run()
```
`with g.as_default()`这个只在定义tensor前使用，sess.run()是不需要的。
如果使用了类似collection之类的把图的结构分离出来定义的，这些被调用的函数也要位于`with g.as_default()`控制范围内。

## 其他
目前只是自己摸索出来的方法，如果发现了更好的技术途径，会及时更新。