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
## 显示浮动目录
https://blog.csdn.net/hengwei_vc/article/details/47122103

## 更换简洁的主页布局
index_cn.html
```
---
layout: default
nav: index
permalink: /cn/
lang: cn 
---
<div class="content">
    {% for post in site.posts %}
        {% capture y %}{{ post.date | date: "%Y"}}{%endcapture%}
        {% if year != y %}
            {% assign year = y %}
            <h3 class="year">{{ year }}</h3>
        {% endif %}
        <ul class="article-list">
            <li>
                <small>{{ post.date | date: "%Y-%m-%d" }}</small>
                <a href="{{post.url}}" title="{{ post.title }}">{{ post.title }}</a>
            </li>
        </ul>
    {% endfor %}
</div>
```

## 更换页面字体
assets/css/styles.css中找到body中的font-family中的字体，更换为
```css
font-family: 'PT Sans', "HelveticaNeue", "Helvetica Neue", Helvetica, Arial, Hiragino Sans GB, Microsoft YaHei, sans-serif;
```

## 增加toc后导航栏遮挡
