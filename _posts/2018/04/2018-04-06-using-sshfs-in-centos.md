---
layout: postcn
title: "在linux系统下使用sshfs映射网络地址"
date: 2018-04-06 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: 编程
tags: [linux, sshfs, 网络文件系统]
---
## 事出有因
最近在用远程的gpu服务器做开发，把所有的workspace般到服务器上。但这样会造成文件的编辑问题，因为远程的服务器没有桌面，用命令行可以借助vim写单个文件，管理整个文件夹或者工程有点力不从心。当然，主要是不想费太多功夫死磕vim。

## 可行方案
为了应对这个困难，我先后采取了几种措施：
1. 学习linux下的vim命令，安装vim插件。这个推荐一个开源项目, https://github.com/BillWang139967/Vim.git   这个项目可以傻瓜式安装，然后享受vim丰富的插件带来的福利。差不多把vim做成了IDE，可以代码补全。
2. 使用winscp（当时自己用的还是win），它有个GUI界面，可以直接鼠标点文件，用本地编辑器打开，可以解决代码自动补全的问题。但是阅读代码时跨文件的函数调转、利用vscode做git的操作都不能实现。
3. 采用某种类似nfs的机制，把远程目录映射到本地，可以一举解决以上问题。

## 网络地址映射
其实最难的地方在于找一个不需要在服务器端安装软件的方案，因为服务器我没有sudo权限。后来就找到了sshfs这款。

原理很简单，就是一个基于ssh的文件传输协议，只要服务器可以ssh登陆就可以。

在centos上的安装过程如下：
```sh
yum install -y epel-release

yum -y install fuse-sshfs

sshfs -o rw your_name@host_name_or_ip_add:/remote_dir /localdir -p your_ssh_port
```
然后就可以愉快地写代码了。

之前花了点时间，当时并不知道软件名称，一直在尝试`yum install sshfs`，后来就在github上找源代码编译，而编译又各种报错。

Reference:
1. https://blog.csdn.net/sunny05296/article/details/77722081