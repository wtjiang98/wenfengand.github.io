---
layout: postcn
title: "使用python存储多键值的数据"
date: 2018-03-30 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: python
tags: [python]
---
尝试使用hdf5存储，但是出现下述错误
TypeError: Object dtype dtype('O') has no native HDF5 equivalent
字典保存为.h5文件，

## 尝试使用.json存储, 失败
代码如下, [参考](https://blog.csdn.net/u012155582/article/details/78077180)
```python
#保存
dict_name = {1:{1:2,3:4},2:{3:4,4:5}}
f = open('temp.txt','w')
f.write(str(dict_name))
f.close()

#读取
f = open('temp.txt','r')
a = f.read()
dict_name = eval(a)
f.close()
```
但是600M的数据文件保存后只有300K，打开后发现有省略号，截取部分如下：
```json
{('QPSK', 2): array([[[-0.00590147, -0.00234582, -0.00074506, ..., -0.00326824,
         -0.00304144,  0.00569031],
        [-0.00779554, -0.00781637, -0.00401967, ...,  0.01032196,
          0.00841506,  0.00544548]],

```

## 尝试使用pandas保存，近似失败
多键值时，保存为csv后的格式如下：
```
```

## 无可奈何，使用scipy.io中的savemat方法，不同的键值保存为不同的表

具体的方法在这篇笔记里面。
http://blog.stackoverflow.club/read-mat-file-in-python/


