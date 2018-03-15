---
layout: postcn
title: "tensorflow timeout错误"
date: 2018-03-06 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: 机器学习
tags: [机器学习, tensorflow]
---

## 解决了Could not find a version that satisfies the..., 出现socket.timeout错误
<!-- more-->
### 问题描述

*   在运行命令 > (tensorflow)C:> pip install --ignore-installed --upgrade tensorflow-gpu 

时下载到 10%左右报错，错误为socket.timeout

### 问题解决（任选其一）

*   换镜像源（测试有效）, [参考博客][1]   
    修改pip.conf，各个系统存放的位置不一样，Linux请用find自行查找   
      
    修改好后使用pip正常安装软件就好(Windows7 64bit python3.5的pip.ini位置,需要自己创建 C:\Users\<username>\pip\pip.ini) > [global]   
    > index-url = https://pypi.douban.com/simple</username>
*   重新设置超时时间(没有尝试), [参考博客][2]

> pip3 --default-timeout=100 install -U tensorflow

*   离线下载.whl 包安装，[下载地址][3], 安装命令

> pip3 install your_package_name.whl

 [1]: https://www.cnblogs.com/yaohan/p/6130934.html
 [2]: http://blog.csdn.net/MainTain_/article/details/78501095
 [3]: https://pypi.python.org/pypi/tensorflow-gpu