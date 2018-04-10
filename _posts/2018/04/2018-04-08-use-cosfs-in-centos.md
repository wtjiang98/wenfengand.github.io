---
layout: postcn
title: "在centos中使用cosfs腾讯云免费存储"
date: 2018-04-08 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: 编程
tags: [yum, centos, cosfs]
---

# 一定额度内免费的对象存储
腾讯云每个月提供50G的存储空间，10G的下行流量，免费的上行流量。最好的地方在于提供了基于fuse的文件系统，可以将对象存储映射为本地文件，非常适合于存储有限的场合，比如vps，可以通过挂载一个对象存储来增加空间。

# 安装环境依赖包
```sh
sudo yum install automake gcc-c++ git libcurl-devel libxml2-devel fuse-devel make openssl-devel

```

# 安装cosfs
```sh
git clone https://github.com/tencentyun/cosfs-v4.2.1 /usr/cosfs
cd /usr/cosfs
./autogen.sh
./configure
make
sudo make install
```
# 配置
```sh
echo <bucketname>:<SecretId>:<SecretKey> > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```
*注意，执行echo时会提醒权限不够，一般都会使用sudo，但这样会导致文件的主人为root，
在执行后续的挂载时如果没有用sudo，会导致 could not determine how to establish security credentials 错误，
解决方案是使用`sudo chown your_name /etc/passwd-cosfs`把文件的所有者变为当前用户*

# 挂载
```sh
cosfs your-APPID:your-bucketname your mount-point -ourl=cos-domain-name -odbglevel=info
```
- your-APPID/ your-bucketname 需要替换为用户真实的信息；
- your-mount-point 替换为本地需要挂载的目录（如 /mnt）；
- cos-domain-name 为存储桶所属地域对应域名，形式为 http://cos.<Region>.myqcloud.com ，其中 Region 为 [可用地域](https://cloud.tencent.com/document/product/436/6224) 中适用于 XML API 的地域简称
- -odbglevel 参数表示信息级别，照写即可。

# 卸载
```sh
fusermount -u /mnt
```
或者
```sh
umount -l /mnt
```
Reference:
1. https://www.cnblogs.com/znsongshu/p/7801939.html
2. https://cloud.tencent.com/document/product/436/6883