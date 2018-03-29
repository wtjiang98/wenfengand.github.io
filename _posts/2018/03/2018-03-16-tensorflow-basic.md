---
layout: postcn
title: "tensorflow 常用API"
date: 2018-03-16 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: tensorflow
tags: [tensorflow, 机器学习语言]
---




主要是通读《TensorFlow实战Google深度学习框架》的记录
<!-- more -->

# 不太懂的地方
- p78 交叉熵算完之后的值是n*m的矩阵？
- p89 使用collection增加代码可读性
- p91 使用滑动平均模型
- p107 变量管理
# 使用计算图
```python
#生成计算图
g1 = tf.Graph()
with g1.as_default():
    v = tf.get_variable(
        "v", initializer = tf.zeros_initializer(shape = [1])
    )

#在计算图中读取变量的值
with tf.Session(graph = g1) as sess:
    tf.global_variables_initializer().run()
    with tf.variable_scope("", reuse = True):
        #这行会输出[0.]
        print(sess.run(tf.get_variable("v")))
#如果有两个计算图，可以通过图的名称给隔离开
```
# 张量的属性
对于代码
```python
result = tf.add(a, b, name = "add")
print result
```
此代码的输出是这样的：
```python
Tensor("add:0", shape=(2,),dtype = float32)
```
- 名字 node:src_output

node是节点名称，src_output是当前张量来自节点的第几个输出

- 维度

shape=(2,)说明是一个一维数组，长度为2

- 类型type

注意tensorflow会检查类型，不指定类型时按照默认类型，如1认为是int32, 1.0认为是float32

# 使用with的区别
第一种会话方式

```python
sess = tf.Session()
sess.run()
sess.close()
```

第二种会话方式
```python
with tf.Session as sess:
    sess.run()
```
推荐第二种方式，不需要显式关闭会话
# 神经网络前向传播算法
下图是包含一个隐含层的全连接神经网络
![前向传播算法示例](http://blog.stackoverflow.club/images/2018/03/002.jpg)
w系数：$w^{(1) _{i,j}}$ 表示第1层次数，从后一层的第j个节点连接到前一层的第i个节点

# 神经网络的反向传播算法
综述：在每次迭代的开始，都要选取一小部分数据，称为batch，通过前向传播算法得到神经网络的预测结果。因为训练数据都是有正确答案标注的，所以可以计算预测值与真实值的差距，然后通过反向传播算法更新神经网络参数的取值。

# 激活函数

使用激活函数的目的：如果神经网络是线性的，由于矩阵相乘可以化简，形式上任意层的全连接神经网络和单层的神经网络模型的表达能力相同。
网络结构图中1的由来：用来表示偏置项，1应该是表示这是一个常量

# 损失函数
- 交叉熵

这是一个信息论里面的概念，原本用来估算平均编码长度，这里用来判断预测答案和真实答案之间的距离

$$H(p, q) = - p(x)* log( q(x))$$

q(x)是预测答案，p(x)是正确答案

然而，分类问题中，神经网络的输出并不能严格依据概率分布（即所有的概率相加为1），引出softmax函数

$$softmax(y _i) = e ^{yi} / e^{yi}$$

在tensorflow中相关的代码如下：
```python
#交叉熵计算
#y_是正确答案， y是预测答案
# 乘法使用的是元素相乘，得到的结果是
cross_entropy = - tf.reduce_mean( y_ * tf.log( tf.clip_by_value(y, 1e-10, 1.0)))

#限制张量的数值大小
#将y的范围限制在 1e-10 和 1之间，避免log0 之类的无意义计算
tf.clip_by_value(y, 1e-10, 1.0)

#自带的交叉熵公式
cross_entropy = tf.nn.softmax_cross_entropy_with_logits( labels= y_, logits = y)
```

- 平方损失函数

与分类问题相对， 回归问题主要是对具体数值的预测，一般网络的输出只有一个节点。常用的均方误差

$$MSE(y, y ^') = (y _i - y ^' _i)^2 / n$$

具体函数如下：
```python
mse = tf.reduce_mean(tf.square(y_ - y))
```

- 自定义损失函数

在具体问题，网络的优化目的不同，应该使用不同的损失函数。一个自定义损失函数的例子
```python
loss = tf.reduce_sum( tf.where( tf.greater(v1, v2), (v1 - v2 )*a, (v2 - v1)*b))
```
# 反向传播算法与梯度下降、随机梯度下降
梯度下降可以达到局部最优，但是每次都要计算所有的损失函数。

随机梯度下降(stochastic gradient descent)会计算一条数据的损失函数，甚至达不到局部最优。

实际使用中使用一个batch的损失函数

# 学习率
使用衰减的学习率可以让模型更加稳定。
```python
global_step = tf.Variable(0)

#通过exponential_decay生成学习率
learning_rate = tf.train.exponential_decay( 0.1, global_step, 100, 0.96, staircase = True)

#使用指数衰减的学习率，在minimize中传入了global_step，将自动更新global_step参数，从而学习率也得到更新
learning_step = tf.train.GradientDescentOptimizer( learning_rate).minimize(loss_function, global_step = global_step)
```
# 过拟合
过拟合的表现是模型训练精度高，实测精度差，即泛化能力弱。可以说是模型太复杂，也可以相对的认为训练样本过少。
- 正则化

为了防止过拟合， 在训练的时候不是直接优化损失函数，而是优化 $J(\theta ) + \lambda R(w)$, $R(w)$表示模型的复杂程度, $\lambda$表示模型复杂损失在总损失中的比例

- 模型复杂度函数$R(w)$

L1正则化
$$R(w) = || w ||_1 = |w_i|$$

L2正则化
$$$$

在代码中使用正则化
```python
loss = tf.reduce_mean( tf.square( y_ - y)) + tf.contrib.layers.l2_regular( lambda)(w)
```

# 使用collection增加代码可读性
# 滑动平均模型
在采用随机梯度下降算法训练神经网络时，使用滑动平均模型在很多应用中都可以在一定程度上提高最终模型在测试数据上的表现
# 变量管理
# Save模型与代码优化 
p112
- 保存模型
```python
saver = tf.train.Saver()
with tf.Session() as sess:
    ...
    saver.save(sess, 'your_path')
```
- 恢复模型
```python
variables definitions...
saver = tf.train.Saver()
with tf.Session as sess:
    saver.restore(sess, 'your_path')

```
# 迁移学习与slim
# TFRecord
# 图像预处理
# 数据集
# 循环神经网络
# LSTM

# 指定GPU
在多用户的GPU服务器上跑代码，默认可能会使用GPU0，这时，
如果其他人也使用了GPU0， 很可能会资源分配不足报错。
使用下面的代码可以指定运行的GPU。
```python
import os
os.environ["CUDA_VISIBLE_DEVICES"] = "1"
```



