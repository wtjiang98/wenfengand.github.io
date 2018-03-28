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
曾经使用过的比较实用的命令
<!-- more -->
## 推送不同名的本地分支到远程分支
    git push remote localBranchName:remoteBranchName
    git push  <远程地址> <本地分支名>:<远程分支名>
## rebase
变基理解得还不是很透彻，[参考页面](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%8F%98%E5%9F%BA)

## 取消文件追踪
```
git rm --cached readme1.txt    删除readme1.txt的跟踪，并保留在本地, 但是远程仓库的内容会被删除
```

## 删除分支 重命名分支
有时候在其他分支上开发了太多功能，需要取代master，即把正在开发分支取代master分支。
首先删除分支
```sh
git branch -D branch_name
```
然后重命名分支
```sh
git branch -m branch_old_name branch_new_name
```

## 撤销git reset
```sh
git reflog
git reset --hard commits_you_want_to_retrieve
```
## 撤销git add
```sh
git reset HEAD
```
## 单个文件撤销更改
1. 如果没有被git add到索引区
```
git checkout a 
```
便可撤销对文件a的修改
2. 如果被git add到索引区，但没有做git commit提交1）

将a从索引区移除（但会保留在工作区）
```
git reset  HEAD a
```
```
git checkout a 
```
3. 如果已被提交
```
git reset  HEAD^
```
先回退当前提交到工作区，然后撤销文件a的修改回退当前提交到工作区
```
git checkout a
```
撤销工作区中文件a的修改

## 纯命令行界面查看文件修改
在执行commit之前执行这个命令
```git
git diff file_name
```

