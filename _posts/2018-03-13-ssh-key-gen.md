---
layout: postcn
title: "使用公钥作为密码"
date: 2018-03-13 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: 工具
tags: [工具, coding, rsa]
---



碰到过的关于公钥的问题

<!-- more -->
## 设置了pass phrase后嫌麻烦，又该怎样去除呢？
首先进入私钥所在目录
 
    cd ~/.ssh/
然后使用ssh-keygen命令
  
    ssh-keygen -f id-rsa -p
按提示操作即可
terminal的输出是这样的

``` linenos
$ ssh-keygen -f id_rsa -p
Enter old passphrase:
Enter new passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved with the new passphrase.
```