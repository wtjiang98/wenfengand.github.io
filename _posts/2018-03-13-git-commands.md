---
layout: postcn
title: "git常用命令与解释"
date: 2018-03-13 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: coding
tags: [git, 命令]
---

* content 
{:toc} 
曾经使用过的比较实用的命令

## 推送不同名的本地分支到远程分支
    git push remote localBranchName:remoteBranchName
    git push  <远程地址> <本地分支名>:<远程分支名>
## rebase
变基理解得还不是很透彻，[参考页面](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%8F%98%E5%9F%BA)

## 取消文件追踪
```
git rm --cached readme1.txt    删除readme1.txt的跟踪，并保留在本地。
```