---
layout: postcn
title: "在window上使用cmake"
date: 2018-01-28 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: 编译器
tags: [编译器, cmake]
---
<!-- more-->
在github上看了很多程序，发现都是用cmake来自动生成makefile，然后进一步执行make来构建程序。

不得不说，cmake的功能很强大，不仅可以生成make的配置文件，还可以生成VS、eclipse的工程文件。但是我在使用时总是碰到很多错误，首先就是cl找不到，用图形化工具时也是找不到。

如果正确地使用cmake？首先，确保自己的系统中存在cmake可以识别的编译工具，但是，*这个编译工具属于半自动识别*，命令行下你需要使用 -G 参数来选择Generator，只有选对正确地Generator，才可以识别到你的工具链。

1.  首先使用MinGW下载MSYS的make工具，然后添加进系统路径，确保在命令行下make可以正常运行
2.  下载cmake，这个可以网络搜索下载，注意添加进系统路径
3.  在工程的根目录下新建 build文件夹，进入这个文件夹
4.  执行 cmake -G (options for generator..) ../ 注意cmake的命令格式，最后的../表明source在上一级目录 很多博客用的都是 . 表明是当前目录，但是会把生成的文件和源文件混在一起
5.  cmake只是生成makefile，进一步生成可执行文件需要执行make