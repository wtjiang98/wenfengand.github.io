---
layout: postcn
title: "jekyll网站"
date: 2018-03-13 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: website
tags: [website, jekyll]
---


jekyll网站
<!-- more -->
## 显示公式
    1. 在markdown文件中使用公式标签录入公式
    2. 在html页面中添加js代码, 可以是default.html或者post.html
    ```js
    <script type="text/javascript" async
    src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.2/MathJax.js?config=TeX-MML-AM_CHTML">
    </script> 
    ```
## 更改文章的链接
在_config.yml中找 permalink项，改为如下方式即可去掉默认的链接中的时间项
```
permalink: /:title/
```