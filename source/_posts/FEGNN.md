---
title: Feature Expansion for Graph Neural Networks
tags:
  - 深度学习
  - 图
  - 关系
categories:
  - 图神经网络
mathjax: true
date: 2023-10-08 11:09:24
abbrlink: FEGNN
description: GNN图神经网络在特征扩展上的论文研究
---
<font size=6 >**Feature Expansion for Graph Neural Networks**</font>
论文源地址：[Feature Expansion for Graph Neural Networks](https://arxiv.org/abs/2305.06142)

# 摘要
&emsp;&emsp;在图神经网络中，通过分析空间模型和频谱模型的特征空间来实现对表征学习和特征空间的系统研究
具体操作为：
&emsp;&emsp;**将图神经网络分解为确定的特征空间和可训练权重---->为使用矩阵空间分析法明确研究特征空间提供了便利**
存在问题：
&emsp;&emsp;**由于重复聚合，特征空间趋于线性相关。在这种情况下，现有模型中共享权重的代表性较差或节点属性的维度有限，导致特征空间受限，从而导致性能不佳。**
提出方法：
&emsp;&emsp;**①：特征子空间扁平化；**
&emsp;&emsp;**②：结构主成分来扩展特征空间；**
实际效果：
&emsp;&emsp;**广泛的实验验证了我们提出的更全面特征空间的有效性，推理时间与基线相当，并证明了其高效的收敛能力**
。
