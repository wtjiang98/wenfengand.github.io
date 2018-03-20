---
layout: postcn
title: "latex教程"
date: 2018-03-20 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comments: true
category: 语法
tags: [语法, latex, 教程]
---

* content 
{:toc} 

一篇介绍latex语法的教程，仅介绍我曾经使用过的。
<!--more-->

## 文章开始与结束
```tex
\documentclass{article}
\begin{document}
hello, world
\end{document}
```

在vscode中可以按 `ctrl + alt + t`快速预览。

 ## 增加标题、作者、注释
```tex
\documentclass{article}
\author{wenfengand}
\title{tutorial on latex}
\begin{document}
\maketitle
hello, world
\end{document}
```

## 增加章节
使用下面的关键词可以在文中增加section，并且这些section可以自动添加序号，section后的大括号里面是section标题
```tex
\section{section name}
```

另外还有增加二级和三级标题的关键词
```tex
\subsection{section name}
\subsubsection{section name}
```
## 增加段落
```tex
\paragraph{paragraph name}
```
## 增加目录
把下面的关键词放到`\begin{document}`之后，第一个section之前，可以把目录放到文章开头。
```tex
\tableofcontents
```

## 增加数学公式
行内公式, 排版会和周围的文字对齐。
```tex
This is a formula $a=\delta + c$.
```
行间公式，排版会居中。
```tex
$$a=\Delta + c$$
```
另外，如果vscode中没有装 markdown-math的话可能需要包含一些数学公式包。
```tex
\usepackage{amsmath}
\usepackage{amssymb}
```
之后会专门记录latex的公式。
## 增加图片
首先，包含处理图片的包, 放到`\begin`之前
```tex
\usepackage{graphicx}
```
然后，包含所需要的图片，中括号内放尺寸大小（不填的话会显示原始大小），单位是英寸或者cm, 大括号内放文件路径
```tex
\includegraphics[width=0.1in, height=0.1in]{next.eps}
```

## 添加中文支持
把模板换为ctexart即可，注意增加编码信息, 编码信息必须为UTF8，不能是utf8或者utf-8
```tex
\documentclass[UTF8]{ctexart}
```