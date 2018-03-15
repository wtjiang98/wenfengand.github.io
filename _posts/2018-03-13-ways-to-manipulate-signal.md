---
layout: postcn
title: "在辐射源特征识别上的信号处理方法"
date: 2018-03-13 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: 信号与信息处理
tags: [辐射源, 特征识别, 论文咀嚼]
---

一篇雷达辐射源特征识别的论文解析。
<!-- more -->
这两天看了一篇论文，有关辐射源特征识别的，觉得很有意思。
## 论文出处
2016 9th International Congress on Image and Signal Processing, BioMedical Engineering and Informatics(CISP-BMEI 2016)
## 作者信息
Xiaohu Ru, Chao Gao, Zheng Liu, Zhitao Huang, Wenli Jiang
College of Electronic Science and Engineering, National University of Defense Technology
Changsha, Hunan, 410073, P.R. China
## 特征提取方案

提出了一个公式，用来衡量信号的不同部分的UIM强度

假设信号被分为了$N_{seg}$部分：$z_k, k=1, 2, \cdots, N_{seg}$，这里$z_k$是第$k$个列向量。把$z_k$的傅里叶变换表述为$Z_k(f)$，那么UIM的强度可以可以按如下定义

$$ \Delta ^ {UIM} _k = \int ^{f_s/2} _{-f_s/2}
|

|Z_k(f-f_0)/ \alpha |^2

-

|sinc(Tf)|^2
|
$$

其中， $f_s$是采样速率，$\alpha$是$Z_k(f)$的最大幅度，$f_0$是信号$z_k$的载波频率， $T$是信号持续时长, $sinc(t)$是sinc函数$sin(\pi t)/\pi t$。

将采样得到的点标记为$z(i), i=1,2, \cdots, N$, 所以共有N的采样点。以往的特征提取方法认为所有的点都是同样重要的，所以所有的点都参与了计算，导致运算负担加重。这里会提出一种同时减少计算量且不会丢失UIM信息的方法。
- 第一步
把信号分为 $N_{seg}$个部分。相邻的部分可以重叠，计算UIM强度，将结果写为 $\Delta ^{UIM} _k= 1,2,\cdots, N_{seg}$.

- 第二步
在 $\Delta ^{UIM} _k$的基础上，把信号分为不重叠的$N_h + N_l$部分。$N_h$是高强度UIM部分，$N_l$是低强度UIM部分。用$z ^{HD} _k, z ^{LD} _k$表示划分后的结果。通常，$z ^{LD} _k$在信号中占据大部分。
- 第三步
对$z ^{LD} _k$进行降采样。可以先选择一个整数 $m _k$，然后从$z ^{LD} _k$中每隔$m _k$个点选出一个点，这些选出的点构成新的向量 $z ^{LDDS} _k$，采样率是 $f_s / m_k$. 为了去除混叠效应，需要在降采样之前加入低通滤波器。
- 第四步
将第二步第三步得到的信号拼接起来，可以用不同的权重因子来代表不同的重要程度。
