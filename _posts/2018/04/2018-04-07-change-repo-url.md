---
layout: postcn
title: "更换pip的源"
date: 2018-04-07 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: python
tags: [python, 软件源]
---

# 建立pip.conf文件
```sh
cd ~
mkdir .pip
cd .pip
vim pip.conf
```

# 填充pip.conf内容
```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

其他可用的镜像
```
阿里云 http://mirrors.aliyun.com/pypi/simple/ 
  中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/ 
  豆瓣(douban) http://pypi.douban.com/simple/ 
  清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/ 
  中国科学技术大学 http://pypi.mirrors.ustc.edu.cn/simple/
```

Reference:
1. https://blog.csdn.net/chenghuikai/article/details/55258957