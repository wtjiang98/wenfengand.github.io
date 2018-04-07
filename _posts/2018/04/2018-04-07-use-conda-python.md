---
layout: postcn
title: "使用conda管理python环境"
date: 2018-04-07 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: python
tags: [python, conda]
---

# 问题
不管用的是MS还是Linux，碰到python最头疼的就是各种不同的python版本。一般会出现以下几种情况：
1. python2 和python3希望在一台机器上共存
2. 验证某python软件时，和本地的python环境不兼容，又不想为了验证软件功能而破坏本地环境。

# 解决
使用conda创建各种不同的python环境

# 常用命令
1. 创建环境
```sh
conda create -n env_name python=2.7
```
2. 激活环境
```sh
conda activate env_name
```
3. 退出环境
```sh
conda deactivate
```
4. 显示当前系统下的环境
```sh
conda info -e
```
5. 添加国内镜像
```sh
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/conda config --set show_channel_urls yes
```

如果只是安装基本的python， 安装好之后通过pip安装必备的包，这时候需要把pip的源换为国内的，请移步 http://blog.stackoverflow.club/change-pip-repo-url/

6. 列出已经安装的包
```sh
conda list
```

or

```sh
conda list -n env_name
```

Reference:
1. https://zhuanlan.zhihu.com/p/22678445