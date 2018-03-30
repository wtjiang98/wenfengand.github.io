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

## matplotlib

### ssh远程操作 出现RuntimeError: Invalid DISPLAY variable
添加如下代码
```python
plt.switch_backend('agg')
```
[参考页面](https://www.cnblogs.com/bymo/p/7447409.html)

### 保存图像
使用plt.savefig
```python
import matplotlib.pyplot as plt
plt.savefig("filename.png")
plt.show()
```
注意savefig必须在show之前调用，否则show之后默认开新图，保存的图一片空白

或者，使用gcf方法
```python
fig = plt.gcf()
plt.show()
fig1.savefig('test.jpg', dpi=100)
```

### 图像格式
在plt.savefig()方法中增加format=参数
可选的参数如下：
- jpg
- png
- pdf
- eps
- svg

完整的调用方法为
`plt.savefig('file_name', format='jpg')`
如果不指定format，默认为jpg格式，与文件的后缀名无关

### 
