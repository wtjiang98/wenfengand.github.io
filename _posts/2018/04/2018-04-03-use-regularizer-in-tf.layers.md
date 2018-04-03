---
layout: postcn
title: "在tf.layers. 高层api中使用正则化"
date: 2018-04-03 08:00:00 +0800
lang: cn
nav: post
stickie: false 
comment: true
category: python
tags: [python]
---

```python
#定义正则化函数
regularizer = tf.contrib.layers.l2_regularizer(scale=0.01)
#在初始化中加入正则化函数
conv1 = tf.layers.conv1d(
    inputs = x_image,
    filters= first_conv_filter_n,
    kernel_size= ( first_conv_filter_y),
    strides=1,
    padding='same',
    activation=tf.nn.relu,
    kernel_initializer= tf.random_normal_initializer(stddev=0.1),
    kernel_regularizer= regularizer,
    use_bias= True
)
#得到正则化值
add_loss =  tf.losses.get_regularization_loss()
```