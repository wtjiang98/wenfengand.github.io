---
layout: postcn
title: "在linux中使用sslocal与auto pac"
date: 2018-04-06 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: linux必备
tags: [pac, sslocal, centos, ubuntu]
---
近日重新安装了笔记本的系统，换成了centos, 一个linux的发行版，感觉还不错。奈何没有了windows版本的shadowsocks，就暂时没有了自动翻墙的便捷。

科普一下，自动翻墙是依赖于一个PAC文件，里面放着国内访问不了的域名。这样在上网的时候可以只在访问不了的域名才翻墙，而在访问百度这样的国内网站时不翻墙，以提升速度。

虽然目前的电脑是centos系统，但是autopac的配置也同样适用于其他linux系统。

## 安装shadowsocks
```sh
pip install shadowsocks
```

## 配置shadowsocks
1. 在/etc下创建shadowsocks.json配置文件

这个文件可以放在任何地方
```sh
sudo touch /etc/shadowsocks.json
```
然后用vim或者其他编辑器，在shadowsocks.json中加入如下内容：
```json
{
"server":"your_server_ip",
"server_port":your_server_port,
"password":"your_password",
"method":"your_encrypt_method",
"local":"127.0.0.1",
"local_port":your_local_port
}
```

其中以your_开头的设置，都是按照你的服务器的配置 或者本地配置 来配置的。

## 安装与配置genpac
```python
pip install genpac
```
生成pac文件
```sh
mkdir ~/shadowsocks
cd shadowsocks
genpac --proxy="SOCKS5 127.0.0.1:1080" --gfwlist-proxy="SOCKS5 127.0.0.1:1080" -o autoproxy.pac --gfwlist-url="https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt"
```

## 配置系统的网络proxy
*暂时只有图形界面的配置方法*
按如下路径打开代理配置：

[system] settings -> network -> network proxy

选择代理方式为automatic, 配置url填写为
```url
file:///home/your_name/shadowsocks/autoproxy.pac
```

其中，your_name是需要根据实际情况更改的内容。

Reference:
1. http://blog.leanote.com/post/sxdeveloper/Ubuntu%E4%B8%8B%E8%AE%BE%E7%BD%AEShadowsocks%E7%9A%84%E9%9D%9E%E5%85%A8%E5%B1%80%E4%BB%A3%E7%90%86%EF%BC%88PAC%E8%87%AA%E5%8A%A8%E4%BB%A3%E7%90%86%EF%BC%89

关掉界面就可以愉快地自动pac了。

当然，前提是你有配置好的服务器，本地也开启了sslocal.

另外，发现centos自带的中文输入法一点都不好用，在考虑换成sougou.