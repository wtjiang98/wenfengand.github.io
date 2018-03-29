---
layout: postcn
title: "python argparse 无法传递bool"
date: 2018-03-11 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: python
tags: [python, argparse]
---

## 问题详述

在使用argparse时发现无法传递bool型变量，无论命令行输入True还是False，解析出来之后都是True，代码如下
<!-- more -->
    parser = argparse.ArgumentParser()
    parser.add_argument(
        '--isTrain',
        help='Do you want to train the network?',
        type=bool,
    )
    
    args = parser.parse_args()
    my_bool = args.bool_arg
    

## 问题解决

在搜索了一下后，发现有一种注册回调函数的方法比较好用，代码如下

### 回调函数

    def str2bool(v):
    if v.lower() in ('yes', 'true', 't', 'y', '1'):
        return True
    elif v.lower() in ('no', 'false', 'f', 'n', '0'):
        return False
    else:
        raise argparse.ArgumentTypeError('Unsupported value encountered.')
    

### 正常执行代码

    if __name__ == '__main__':
    parser = argparse.ArgumentParser()
    parser.add_argument(
        '--isTrain',
        type= str2bool,
        nargs = '?', 
        const = True, 
        help='If this is a train process?')
    args, unparsed = parser.parse_known_args()
    if args.isTrain == False:
        isTrain = args.isTrain 
    tf.app.run(main=main)