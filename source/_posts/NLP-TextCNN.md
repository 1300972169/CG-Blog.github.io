---
title: NLP--TextCNN
tags:
  - NLP
  - 自然语言处理
  - 语言模型
categories:
  - NLP
mathjax: true
abbrlink: TextCNN
sticky: 3
swiper_index: 3
date: 2023-08-17 17:55:05
description: 初学TextCNN，对TextCNN以及NLP语言模型的初步了解
---

# TextCNN
TextCNN是{卷积神经网络(CNN)}在自然语言处理(NLP)领域的延伸应用
TextCNN主要应用领域文本分类:二分类，多分类，情感分析，意图识别等

# 算法思路解构
## 1.如何将长文本转换为可计算的向量
TextCNN使用了 word-level Model（基于词级模型），例如
```
英文，比如：I love you
Word-level Model 拆分：I Love You → [I, Love, You] ，拆成3个单词
中文，比如：安红俺想你
Word-level Model 拆分：安红俺想你 → [安红, 俺, 想你] ，拆成3个单词
```
TextCNN是基于Word-level Model（基于词级模型）思路下构造基于词级别的Embedding，利用CNN将变量取得最终的结果,接下来，就是把拆分的词以向量的形式表示了

## 2.TextCNN的模型结构
图片转载，出自[知乎@醉梦江湖](https://pic3.zhimg.com/80/v2-e4d6e2dc0058c00f3915db194874eed2_1440w.webp)
![TextCNNmodel](/assets/image/TextCnnModel.webp)

TextCNN共有4层

1.Word Embedding 层(Sentence Matrix)：负责把文本转换、清洗、切割，构建词向量
2.Convolution 卷积层：将Word Embedding进行卷积，进行变化
3.Pooling 池化层：利用1-MAX降低维度，并能提取重要信息
4.fc Layer 全连接层：，将池化后的输入连接，得到最终分类

## 3.Word Embedding 层
Word Embedding，英文字面意思为语义嵌入。这个词的出现频率非常高。

我们知道计算机是无法处理文本的，它只能处理数字。但语言是有含义的，比如 “算法工程师”和“炼丹师”是在算法下经常见到的词语，那么它们的含义是相近的。

能否找一种方式，把文本转换为数字后可以计算？

还是傅里叶变化思路，我们找到一个函数 $f(X_i)\to Y_i$, 其中：

$X_i$： 表示文本空间的第$i$个词语
$Y_i$:  表示向量空间的第$i$个文本向量的表现形式

这样便将每个样本从文本空间映射到向量空间中。

通俗易懂的形式就是：构建一个词典 vocab，就像字典一样。设定已经出现的词和出现次数，比如设定出现次数>3的词，就添加到词典中。每个词放入词典时候，它都有自己的index，类似主键一样。出现过的沿用第一次放入时的，没出现过就新增一个。

比如“一条，大河，波浪，宽”，查找vocab 这些词的index，为{345,346,347,83}，便完成了从文本到向量的转换。

## 4.Convolution 卷积层
同样的，如果输入的文本直接放入卷积层是不可行的。卷积的作用，就像一段文本提取出一个相对重要的语句含义。

好比一篇文章中，提取出作者的核心思想一样，这个核心思想往往决定了这篇文章究竟是哪个分类。作者借鉴了CNN中卷积思路，利用N-gram，滑动着将语音重要信息提取。
![TextCNNmodel-1](/assets/image/TextCnnModel-1.webp)
比如channel1：长度是4

与Sentence Martrix矩阵对应元素相乘 再相加，得到每个channel输出的 feature map。

与CNN网络不同是，每个filter的宽和输入层是一模一样，即宽都是 5。因此每个filter只能上下滑动，其实每个channel是对不同的词语进行滑动，这种方式也被成为N-gram。
![TextCNNmodel-2](/assets/image/TextCnnModel-2.webp)
再看一个filter 2，channel 2的卷积过程：长度为3
![TextCNNmodel-3](/assets/image/TextCnnModel-3.webp)
## 5.Pooling 池化层
![TextCNNmodel-4](/assets/image/TextCnnModel-4.webp)

池化层的最大作用是：

降低参数数量，减少计算开销
提升模型的泛化性，每一个通道都会产生一个特征图，增强了随机性
TextCNN中使用的是1-max-polling，各个filter下，每个channel都会产生各自的 feature map，利用max-polling找出最大值作为输出层，轻微的偏移不会影响模型整体的判别能力。

比如图中Region ①，channel 1 计算的 feature map 1 = [2, 0, 1]，经过 max-polling 结果2。将每个 feature map输出结果拼接到一起，便成为了整层的输出。

输入到 fc layer中，变得到了最终的分类结果。

# 工程实现
开发环境
anconda + python 3.8.5
编辑器：vs code 

新建 [Config.py]，用于记录一些公共参数方便调用；
``` python
# COnifg.py
# 存放模型配置参数
import argparse
import os.path

def parsers():
    parser = argparse.ArgumentParser(description="TextCNN model of argparse")
    parser.add_argument("--train_file", type=str, default=os.path.join("data", "train.txt"))
    parser.add_argument("--dev_file", type=str,default=os.path.join("data", "ev.txt"))
    parser.add_argument("--test_file", type=str, default=os.path.join("data", "test.txt"))
    parser.add_argument("--classification", type=str,default=os.path.join("data", "class.txt"))
    parser.add_argument("--data_pkl", type=str,default=os.path.join("data", "dataset.pkl"))
    parser.add_argument("--class_num", type=int, default=10)
    parser.add_argument("--max_len", type=int, default=38)
    parser.add_argument("--embedding_num", type=int, default=100)
    parser.add_argument("--batch_size", type=int, default=32)
    parser.add_argument("--epochs", type=int, default=30)
    parser.add_argument("--learn_rate", type=float, default=1e-3)
    parser.add_argument("--num_filters", type=int, default=2, help="卷积产生的通道数")
    parser.add_argument("--save_model_best", type=str, default=os.path.join("model", "best_model.pth"))
    parser.add_argument("--save_model_last", type=str, default=os.path.join("model", "last_model.pth"))
    parser.add_argument("--use_pdserving", type=bool, default=False)
    args = parser.parse_args()
    return args

```
新建Util.py,定义一些工具类方法

## 1.构建Word Embedding
## 2.构建TextCNN Model
## 3.训练模型
## 4.测试集验证