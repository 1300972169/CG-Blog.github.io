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
&emsp;&emsp;**广泛的实验验证了我们提出的更全面特征空间的有效性，推理时间与基线相当，并证明了其高效的收敛能力。**

# 前期准备


一.抽象出GNN的线性近似
二.在线性近似中分解参数和不带参数的GNN组件：
&emsp;&emsp;①：带参数的GNN组件表示学习的参数，用于对特征重新加权
&emsp;&emsp;②：不带参数的GNN组件视为由节点属性和图结构构建的特征空间

# 论文结果(贡献)
  * 从表征学习出发，我们首次研究了图结构数据中形成的特征空间。基于这一观点，我们研究了典型的空间 GNN 和光谱 GNN，并指出了现有 GNN 因特征空间受限而产生的两个问题。
 * 针对两个问题提出了两种修改方法：
&emsp;&emsp;1) 对特征子空间进行扁平化处理；
&emsp;&emsp;2) 采用结构主成分来扩展整个特征空间。
 * 在同嗜性和异嗜性数据集上进行了广泛的实验，取得了显著的改进，例如，在异嗜性图形上的平均准确率提高了 32%。

 # GNN
 针对GNN的相关描述见：[Note for GNN&Knowledge Grape](https://www.cg-blog.com.cn/posts//Note%20for%20GNN&Knowledge%20Grape.html)

 GCN原本的特征公式为：<font size = 5>$H^{(h+1)}=\sigma(\widetilde{D}^{-\frac{1}{2}}\widetilde{A}\widetilde{D}^{-\frac{1}{2}}H^{(l)}W^{(l)})$</font>

 现在用线性近似代替激活函数得到：<font size =5> $H^{(K)}=\widetilde{A}^K X {\textstyle \prod_{i=0}^{K-1}}W^{(i)} $</font>
 注：$H^{(0)}=X$

 # 提出问题&&解决方法
 ## 问题一:权重共享方法限制了特征空间的表现力
 &emsp;&emsp;具体描述:
 ## 解决方案一:
 ## 问题一:
 &emsp;&emsp;具体描述:
 ## 解决方案二:

