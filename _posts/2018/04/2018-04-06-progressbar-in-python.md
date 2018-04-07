---
layout: postcn
title: "在python中实现进度条"
date: 2018-04-06 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: python
tags: [python, 进度条]
---

# 试图通过pip
在python2中可以很方便的安装progressbar模块，但是python3中会报如下错误：
```python
Collecting progressbar
  Downloading progressbar-2.3.tar.gz
    Complete output from command python setup.py egg_info:
    Traceback (most recent call last):
      File "<string>", line 1, in <module>
      File "/tmp/pip-build-ghlr5eic/progressbar/setup.py", line 5, in <module>
        import progressbar
      File "/tmp/pip-build-ghlr5eic/progressbar/progressbar/__init__.py", line 59, in <module>
        from progressbar.widgets import *
      File "/tmp/pip-build-ghlr5eic/progressbar/progressbar/widgets.py", line 121, in <module>
        class FileTransferSpeed(Widget):
      File "/home/wenfeng/anaconda3/envs/tensorflow/lib/python3.6/abc.py", line 133, in __new__
        cls = super().__new__(mcls, name, bases, namespace, **kwargs)
    ValueError: 'format' in __slots__ conflicts with class variable
    
    ----------------------------------------
Command "python setup.py egg_info" failed with error code 1 in /tmp/pip-build-ghlr5eic/progressbar/
```
显然，这是由于版本差异造成的。所以，可以考虑自己实现一个progressbar了。

# 自己造轮子

- 类的实现
```python
#!/usr/local/lib
# -*- coding: UTF-8 -*-

import sys, time

class ShowProcess():
    """
    显示处理进度的类
    调用该类相关函数即可实现处理进度的显示
    """
    i = 0 # 当前的处理进度
    max_steps = 0 # 总共需要处理的次数
    max_arrow = 50 #进度条的长度

    # 初始化函数，需要知道总共的处理次数
    def __init__(self, max_steps):
        self.max_steps = max_steps
        self.i = 0

    # 显示函数，根据当前的处理进度i显示进度
    # 效果为[>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]100.00%
    def show_process(self, i=None):
        if i is not None:
            self.i = i
        else：
            self.i += 1
        num_arrow = int(self.i * self.max_arrow / self.max_steps) #计算显示多少个'>'
        num_line = self.max_arrow - num_arrow #计算显示多少个'-'
        percent = self.i * 100.0 / self.max_steps #计算完成进度，格式为xx.xx%
        process_bar = '[' + '>' * num_arrow + '-' * num_line + ']'\
                      + '%.2f' % percent + '%' + '\r' #带输出的字符串，'\r'表示不换行回到最左边
        sys.stdout.write(process_bar) #这两句打印字符到终端
        sys.stdout.flush()

    def close(self, words='done'):
        print ''
        print words
        self.i = 0

if __name__=='__main__':
    max_steps = 100

    process_bar = ShowProcess(max_steps)

    for i in range(max_steps + 1):
        process_bar.show_process()
        time.sleep(0.05)
    process_bar.close()
```

- 测试
```python
process_bar = ShowProcess(max_steps) # 1.在循环前定义类的实体， max_steps是总的步数    
for i in range(max_steps + 1):    
    process_bar.show_process()      # 2.显示当前进度
    time.sleep(0.05)    
process_bar.close('done')            # 3.处理结束后显示消息    
```