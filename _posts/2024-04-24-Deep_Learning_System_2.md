---
title: "'Manual' Neural Networks"
date: 2024-04-24
categories: Deep_Learning_System
---

## 1. 从线性到非线性

### 1.1 线性假设的问题

线性可分假设认为，样本的分类边界应当是若干条直线，这意味着，我们可以使用线性函数（样本空间中的若干超平面）来将不同种类的样本区分开来。如下图

![线性可分情况](https://github.com/Lucas66Zhang/PersonalBlog/blob/main/assets/images/DLS/linear_classifier.png?raw=true)

在这种情况下，我们只使用若干线性映射，就可以将样本合理的进行分类：
$$
h_\theta(x) = \theta^Tx,\quad \theta\in\mathbb{R}^{n\times k}
$$
但是，当样本不满足线性分类假设时，上述线性映射就无法起效，如下图

![非线性可分情况](https://github.com/Lucas66Zhang/PersonalBlog/blob/main/assets/images/DLS/unlinearity.png?raw=true)

> 常见的方法：样本在当前空间线性不可分，我们就寻找一个高维空间，使得样本在高维空间可分。简单地说就是寻找将样本特征维度提升的方法，使升维后的样本特征向量线性可分。
> $$
> h_\theta(x) = \theta^T\phi(x),\quad \theta\in\mathbb{R}^{d\times k},\phi:\mathbb{R}^{n}\to\mathbb{R}^{d}
> $$

### 1.2 那我们如何进行维度的提升？

这个问题其实就是如何构造映射$\phi(\cdot)$，使得映射后的特征向量线性可分。

1. 传统的机器学习会基于对特征的理解以及模型的表现，人为地构造新的特征。
2. 如今的机器学习倾向于设计可以从数据中自主学习特征构造的模型。

首先我们考虑用一个线性映射作为$\phi(\cdot)$，即
$$
\phi(x) = W^Tx
$$
这是不奏效的，因为线性映射的叠加还是线性映射，即$h_\theta(\cdot)$​最终还是线性映射。

一个通用的方法是用一个非线性映射叠加一个线性映射来构造$\phi(\cdot)$，即
$$
\phi(x) = \sigma(W^Tx), \quad W\in\mathbb{R}^{n\times d}, \sigma:\mathbb{R}^{d}\to\mathbb{R}^{d}
$$

> 例子：随机傅里叶特征(random Fourier features)

## 2. 神经网络(Neural Network)

神经网络已经比较熟悉了，这里不再浪费时间描述。以下是选择**深度**神经网络的几个原因。

1. 神经网络受大脑工作原理启发，**但是**它的工作方式并不是大脑的。
2. 多层网络相比于单层网络，在拟合神经网络不能完全拟合的函数(eg. parity function)时更高效。
3. 在控制参数量相同时，深度神经网络比宽度神经网络表现更好，经验上的。

## 3. 反向传播算法(Back-Propagation)

这也是老生长谈了，本质上是复合函数的链式求导法则，是深度学习工程落地的基础之一。