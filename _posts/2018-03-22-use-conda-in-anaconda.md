---
layout: postcn
title: "在Anaconda中使用conda"
date: 2018-03-22 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: python
tags: [conda, python]
---


python代码的依赖包众多，版本也各不相同，安装各种不同的虚拟环境很有必要，尤其是测试github上的代码。
<!-- more -->
## 安装Anaconda
首先，必须确保已经安装了Anaconda. 在 https://www.anaconda.com/download 下载相应版本的安装包。windows直接双击就行，
linux也很简单，运行命令 `bash ~/Downloads/Anaconda3-5.1.0-Linux-x86_64.sh`, 根据提示操作。

在linux 上安装可以参考 https://docs.anaconda.com/anaconda/install/linux 
## 创建虚拟环境
其次，运行如下命令创建虚拟环境：
```python
conda create -n yourenvname python=python_edition
```
其中，yourenvname可以任意命令，python_edition是python版本，可以是 3.5, 3.6, 2.7, ...

如果没有网络连接，可以使用如下命令，克隆一个本地的环境
```python
conda create -n yourenvname --clone root
```

## 激活虚拟环境
使用如下命令
```sh
conda activate your_env_name
```
这时，命令行会变成以`your_env_name`开头的，如下：
```sh
user@user-ubuntu:/home$ conda activate tensorflowcp36
(tensorflowcp36) user@user-ubuntu:/home$
```

以后你运行的所有命令都是在虚拟环境中。

## 取消激活
```sh
conda deactivate
```




