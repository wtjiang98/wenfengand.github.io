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
待解决

## jekyll build timeout
重新在云主机上部署了jekyll之后，把自己的post传进去，运行jekyll build后
总是卡在`Rebuilding index`处，网上提出安装`gsl`，但是在ubuntu上使用
命令`apt install gsl`无法安装或者推荐的包没有效果，最终的解决方案如下：

在_config.yml中找到`lsi`项，设置为`lsi: false`就可以快速编译成功

## coding pages出现编译错误，无法部署分支
解决方案同 jekyll build timeout项，禁止编译lsi
