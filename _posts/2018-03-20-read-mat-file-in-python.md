---
layout: postcn
title: "使用python读取matlab数据文件.mat"
date: 2018-03-20 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: python
tags: [python, matlab]
---

* content 
{:toc} 

一种在matlab和python间共享数据的方法。
<!--more-->

scipy提供了loadmat和savemat来读写.mat文件
```python
import scipy.io as sio
#matlab文件名 
matfn=u'your_file_name'
data=sio.loadmat(matfn)
#注意中括号里面的名称是在.mat中的，在matlab生成数据时确定 
xi = data['xi']
yi = data['yi']
```

python存储.mat文件供matlab使用
```python
import scipy.io as sio
import numpy as np
 
###下面是讲解python怎么读取.mat文件以及怎么处理得到的结果###
load_fn = 'xxx.mat'
load_data = sio.loadmat(load_fn)
load_matrix = load_data['matrix'] #假设文件中存有字符变量是matrix，例如matlab中save(load_fn, 'matrix');当然可以保存多个save(load_fn, 'matrix_x', 'matrix_y', ...);
load_matrix_row = load_matrix[0] #取了当时matlab中matrix的第一行，python中数组行排列
 
###下面是讲解python怎么保存.mat文件供matlab程序使用###
save_fn = 'xxx.mat'
save_array = np.array([1,2,3,4])
sio.savemat(save_fn, {'array': save_array}) #和上面的一样，存在了array变量的第一行
 
save_array_x = np.array([1,2,3,4])
save_array_y = np.array([5,6,7,8])
sio.savemat(save_fn, {'array_x': save_array_x, 'array_x': save_array_x}) #同理，只是存入了两个不同的变量供
```

Reference
1. http://www.jb51.net/article/135384.htm