---
layout: postcn
title: "python argparse模块使用"
date: 2018-03-08 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: python
tags: [python, argparse]
---

在研究TensorFlow代码时发现广泛存在着argparse模块的使用，所以简单地学习下如何使用该模块。
<!-- more-->
# 指定参数、可选参数与未解析参数的混合使用

    import argparse
    def main():
        parser = argparse.ArgumentParser()
        parser.add_argument(
            '--data_dir',
            type=str,
            help='Directory for storing input data')
        parser.add_argument('integer', type = int, help = 'display an integer')
        FLAGS, unparsed = parser.parse_known_args()
        #args = parser.parse_args()
        if FLAGS.data_dir:
            print(FLAGS.data_dir)
        if FLAGS.integer:
            print(FLAGS.integer)
        if unparsed:
            print(unparsed)
    if __name__ == '__main__':
        main()
    

# 要点分析

*   使用argparse.ArgumentParser()增加一个解析器对象
*   用add_argument()方法增加一个参数，注意参数前加"--"为可选参数，否则为必选参数
*   使用parse_known_args()方法解析，返回的第一个参数为已解析的对象，第二个为未解析对象
*   使用已解析对象即可访问传入参数