---
layout: postcn
title: "在win10电脑上配置latex环境"
date: 2018-03-15 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comments: true
category: test
tags: [latex, perl]
---



vscode + latex workshop开写论文
<!-- more -->
在word和latex之间徘徊不定，不知道选用那种工具来写论文更好一些。最终考虑到windows平台的软件都比较消耗硬件资源，我这台电脑还是希望它能服役多年的。所以，掌握了latex写论文后，就打算把笔记本由win10换为ubuntu。

在zhihu.com上看到支持latex的编辑器有很多，但是有一个非常有特色：vs code + latex workshop。 之前由朋友介绍入坑vscode， 的确被它的美征服到了，目前所有类型的代码都是用vscode在写，所以果断选用这一款搭配。

首先，打开vscode，按快捷键`ctl + shift + p`调出一个命令输入弹框，注意这个弹框默认有一个`>`， 删掉这个大于号之后输入`ext`, 注意还要输入回车，进入扩展程序管理界面，输入latex搜索可以看到latex workshop，点击安装就可以。

然后，新建一个文本文件，注意文件名后缀为`.tex`，用vscode打开。在编辑区域点击右键，可以看到有`build latex project`选项。此刻点击会在左下角会显示失败。点击右键，选择`latex workshop: all actions`， 弹出所有命令，选择`show latex complier log`。 重新编译，发现具体的错误是`Error: spawn latexmk ENOENT`。 该错误表明，要么没有添加系统环境变量，要么工具链没有安装。此处为后者。

*latex workshop插件只是一层api，还需要安装latexmk供其调用*

安装latexmk有两个主要步骤，可以参考[这个网页](http://mg.readthedocs.io/latexmk.html)：
1. 安装perl
在 http://strawberryperl.com/ 可以找到适合windows的perl安装包，下载安装即可。 安装好后可以在windows powershell 或者cmd 输入 `perl -v`，如果有版本信息说明安装成功，否则继续google错误原因。
2. 安装 MikTeX Package Manager
在 https://miktex.org/ 可以找到安装包，下载安装


上述安装过程完成后，重新用vscode打开.tex文件，选择`build latex project`, 在.tex文件的目录下出现 .pdf文件，latex环境配置成功。

附上一个简单的latex文件内容，用来测试环境：
```tex
\documentclass{article}
\begin{document}
hello, world
\end{document}
\end{document}
```