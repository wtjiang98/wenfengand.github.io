---
layout: postcn
title: "mpc5748g sdhc调试"
date: 2018-01-28 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: 嵌入式
tags: [嵌入式, SD卡]
---

* content 
{:toc} 

## 现象：

在测试工程中无法初始化SD卡，但是在示例工程中却可以
<!-- more-->
## 猜测

可能是引脚初始化的问题

## 解决方案

使用debug中的查看寄存器功能记录了两个工程中与SDHC相关的引脚的寄存器值，发现如下不同：

寄存器名称 | 该寄存器对应的引脚 | 正常工作的寄存器内容 | 不正常工作的寄存器内容 ----- ---| ---- --------- | -------------------| -----------------  
MSCR120| PH8 |0x0208 0001| 0x3208 0001 MSCR131 |PI3 |0x020B 0003| 0x320B 0003 MSCR70 |PE6 |0x020B 0005 | 0x320B 0005 MSCR71 |PE7 |0x0208 0005 | 0x3208 0005

这里的不同是 测试工程中MSCR寄存器中用的是Half drive strength with slew rate control 在示例工程中使用的是 Full driver strength without slew rate control

随后，在测试工程中修改driver strength 和slew rate control后，SD卡初始化正常

## 后续工作：

1.  曾经把示例工程中的Generated_Code搬移到测试工程中，没有效果，意味着什么？  
    后记: 只是文件的搬移，创建时间没有改变，所以不会参与编译。 如果把该文件的时间戳更新一下，现象就会与预期相符
2.  串口经常出现乱码，是否和driver strength and slew rate control有关系  
    后记: 没有关系，这个是opensda自己的问题，换用外部串口就好了
3.  了解driver strength and slew rate control 的内涵, and what's pad? 
    *   driver strength 实际上是有很多并联的驱动模块，寄存器里选择哪种strength，就会有多少驱动模块加入到IO口中
    *   slew rate control 暂时没有权威资料，但是这个与IO口信号的上升沿陡峭程度有关。slew rate越高，可以捕捉到越快的变化电平，但是噪声也会增加，可能会引起无动作。
    *   pad 我翻译不好，pad应该是GPIO系统中的一部分，一个pad里面包含寄存器和驱动，对应一个实物的引脚。[一个对pad解释较为清楚的文档][1]

## 其他

*   刚刚发现自己的markdown编辑器不能识别表格？有待以后解决
*   至于具体表格里面哪一栏是正常工作的记不清楚了，使用S32DS内置的样例工程测试下就好

 [1]: https://matt.ucc.asn.au/mirror/electron/GPIO-Pads-Control2.pdf