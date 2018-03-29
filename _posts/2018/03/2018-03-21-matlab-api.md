---
layout: postcn
title: "matlab常用api"
date: 2018-03-21 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: matlab
tags: [matlab, api]
---


介绍曾经使用过的、且搜索过后才知道怎么用的api
<!-- more -->

## 保存.mat数据
```matlab
save('your_file_name','variable_name')
```
注意variable_name可以有多个，即把多个矩阵保存在一个.mat文件中

## 不显示图像直接保存

*适合生成论文图片*
待更新
## 使用cell保存图片文件名
待更新

## for
for i = 1:5
左右闭区间

## 高维矩阵 
matlab的高维矩阵是从第三维开始的。
a(:,:,1) 后面的1表示第一页。前面的与两维矩阵相同。
https://blog.csdn.net/qq_29540745/article/details/52724365

## 符号运算
首先，定义符号；
```matlab
syms x y
```
然后，定义运算；
```matlab
a = x + y;
```
最后，给x, y 赋值，获得结果。
```matlab
x = 1;
y = 2;
result = eval(a);
```