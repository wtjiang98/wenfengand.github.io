---
layout: postcn
title: "Could not find a version that satisfies the requirement tensorflow (from versions: ) "
date: 2018-03-06 08:00:00 +0800
lang: cn
nav: post
stickie: true 
category: 机器学习
tags: [机器学习, tensorflow]
---
## 安装TensorFlow时碰到如下问题

*   Could not find a version that satisfies the requirement tensorflow (from versions: ) No matching distribution found for tensorflow

### 使用的安装环境

*   win10 + Anaconda （python 3.6 32bit）
*   命令
    
    > C:> conda create -n tensorflow pip python=3.6
    > 
    > C:> activate tensorflow
    > 
    > (tensorflow)C:> # Your prompt should change
    > 
    > (tensorflow)C:> pip install --ignore-installed --upgrade tensorflow-gpu

*   安装时参考的指引[网页][1]

### 解决途径

*   将32bit的Anaconda换为64bit的
*   [依据][2]

 [1]: https://www.tensorflow.org/install/install_windows
 [2]: https://stackoverflow.com/questions/40884668/installing-tensorflow-on-windows-python-3-6-x