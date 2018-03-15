---
layout: postcn
title: "在s32ds中使用静态库"
date: 2018-01-28 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: 嵌入式
tags: [嵌入式, s32ds]
---
逐步描述了搭建环境的步骤
<!-- more-->
1.  新建eclipse工程的时候选择c\c++工程而不是 S32DS 工程， 后者直接使用交叉工具链。选择static library。
2.  在新建工程的下一步中直接选择交叉工具链，或者建好工程后选择 project->Properties->C/C++ Build->Settings->Cross Settings 选择交叉工具链的prefix和path， 在power pc中是powerpc-eabivle-和C:\NXP\S32DS_Power_v2017.R1\Cross_Tools\powerpc-eabivle-4_9\bin， 这个需要根据自己的安装路径做修改。
3.  optional 如果要为每一个函数生成一个section， 需要在编译选项中加上 -ffunction-sections， 在eclipse中的位置是project->Properties->C/C++ Build->Settings->Cross Gcc Compiler-> Miscellaneous, 在other flags中直接填入-ffunction-sections. 
4.  编译后，生成的库名为lib+工程名+.a

5.  打开需要添加库的工程，设置库的名称与搜索库的路径，库的名称与step 4 中的工程名相同，搜索路径为库文件所在的路径。

6.  设置只链接需要的库函数，这样可以减小image的大小 & 除去错误（比如库函数a中调用了没有实现的函数，在此设置下我们只要不调用库函数a就不会链接出错） 具体的路径：project->Properties->C/C++ Build->Settings->Stand S32DS C Linker-> Miscellaneous， 选中remove unused sections。 注意需要把properties的窗口放到足够大小才会显示下部的复选框。