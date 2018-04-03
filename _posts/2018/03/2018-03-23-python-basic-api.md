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

### 画多个子图

共享x y轴的意思是，多张图是否使用同一个单位刻度，共享后只会在最左边的y轴和最下边的
x轴标出数字，其他轴只有单位刻度。
```python
import numpy as np 
import matplotlib.pyplot as plt 

x = np.linspace(0, 2*np.pi, 400)
y = np.sin(x**2)

# 不共享y轴
f, (ax1, ax2) = plt.subplots(1, 2, sharey=False)
ax1.plot(x, y)
ax1.set_title('Not sharing Y axis')
ax2.scatter(x, y)

# 共享y轴
f, (ax1, ax2) = plt.subplots(1, 2, sharey=True)
ax1.plot(x, y)
ax1.set_title('Sharing Y axis')
ax2.scatter(x, y)


plt.show()

```
Creates four polar axes, and accesses them through the returned array
```python
>>> fig, axes = plt.subplots(2, 2, subplot_kw=dict(polar=True))
>>> axes[0, 0].plot(x, y)
>>> axes[1, 1].scatter(x, y)
```

### 增加子图的title
```python
ax.set_title('Simple plot')
```
[参考](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.subplots.html)

### 画grid
```python
 plt.grid(True, color='grey', linestyle='-', linewidth=1)
 ```

 ### 关闭坐标刻度
 ```python
 plt.xticks([])
 plt.yticks([])
 ```

 ### 关闭坐标轴
 整个坐标系统都不见了，只剩下曲线
 ```python
 plt.axis('off')
 ```

 ### 设置图像dpi
 ```python
 plt.savefig(..., dpi=150)
 ```

 ### 坐标轴不可见
 ```python
 frame = plt.gca()
 frame.axes.get_yaxis().set_visible(False)
 frame.axes.get_xaxis().set_visible(False)
 ```
## zip函数
zip() 函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的列表。

如果各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同，利用 * 号操作符，可以将元组解压为列表。
```python
>>>a = [1,2,3]
>>> b = [4,5,6]
>>> c = [4,5,6,7,8]
>>> zipped = zip(a,b)     # 打包为元组的列表
[(1, 4), (2, 5), (3, 6)]
>>> zip(a,c)              # 元素个数与最短的列表一致
[(1, 4), (2, 5), (3, 6)]
>>> zip(*zipped)          # 与 zip 相反，可理解为解压，返回二维矩阵式
[(1, 2, 3), (4, 5, 6)]
```