---
layout: postcn
title: "归一化在机器学习中的重要作用"
date: 2018-04-01 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: 机器学习
tags: [机器学习, tensorflow, 数据预处理]
---

## 前言
最近在做去噪自编码器，直接把用于MNIST的网络结构拿过来用，结果却很差。

主要表现为即使数据没有噪声，重构后的数据也有明显的失真。

## 解决途径
把送入自编码器的数据归一化到[0,1]之间，因为我所使用的自编码器的激活函数是sigmoid和relu，
两者的输入都要求在[0,1]之间。

## 有待以后更新
各种激活函数的分析