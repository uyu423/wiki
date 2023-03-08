---
title: 004：TensorFlow.js 中的张量和运算
description: 
published: true
date: 2023-02-02T07:36:26.975Z
tags: 
editor: markdown
dateCreated: 2023-02-02T07:36:25.423Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [004: Tensors and Operations in TensorFlow.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/004-tensors-and-operations-in-tensorflow-js)
{.links-list}


# 介绍

TensorFlow.js 是用于机器学习的强大 JavaScript 库，其主要功能之一是能够处理张量。在本文中，我们将了解什么是张量以及如何在 TensorFlow.js 中使用它们。

# 什么是张量？

张量是向量的推广。矢量通常被认为是一维数字数组，但张量可以被认为是任何维度的数组。正如向量可以与标量相加和相乘一样，张量也可以。

张量经常用于机器学习，因为它们可以用于以多种方式表示数据。例如，图像可以表示为三维张量，图像的高度、宽度和深度是三个维度。

# 张量流.js

TensorFlow.js 是一个用于机器学习的 JavaScript 库，可让您以多种方式使用张量。在本文中，我们将介绍在 TensorFlow.js 中使用张量的几种方法。

# 创建张量

可以使用 tf.tensor 函数从 JavaScript 数组创建张量。例如，以下代码创建一个值为 1、2、3 和 4 的二维张量：

```javascript
const t = tf.tensor([[1, 2], [3, 4]]);
```

您还可以使用 tf.ones、tf.zeros 和 tf.fill 函数创建具有特定值的张量。例如，以下代码创建一个二维张量，其值为 1、0、1 和 0：

```javascript
const t = tf.ones([2, 2]);
```

# 操纵张量

可以通过多种方式操纵张量。操作张量的最常见方法是使用 tf.transpose 函数。此函数置换张量的维度。例如，以下代码创建一个值为 1、2、3 和 4 的二维张量，然后置换维度以创建一个值为 1、3、2 和 4 的新张量：

```javascript
const t = tf.tensor([[1, 2], [3, 4]]);
const t2 = t.transpose();
```

也可以使用 tf.reshape 函数重塑张量。此函数返回一个新张量，其值与原始张量相同但形状不同。例如，以下代码创建一个值为 1、2、3 和 4 的二维张量，然后将其整形为值为 1、2、3、4 的一维张量：

```javascript
const t = tf.tensor([[1, 2], [3, 4]]);
const t2 = t.reshape([4]);
```

# 在 TensorFlow.js 中使用张量

TensorFlow.js 提供了多种处理张量的函数。在本节中，我们将了解一些最常用的函数。

tf.tensor 函数可用于从 JavaScript 数组创建张量。 tf.ones 和 tf.zeros 函数可用于分别创建全 1 或全 0 的张量。 tf.fill 函数可用于创建具有给定值的张量。

tf.transpose 函数可用于置换张量的维度。 tf.reshape 函数可用于重塑张量。

tf.concat 函数可用于沿给定维度连接两个或多个张量。 tf.split 函数可用于沿给定维度拆分张量。

tf.add、tf.sub、tf.mul 和 tf.div 函数可用于分别对两个张量执行逐元素加法、减法、乘法和除法。

tf.matMul 函数可用于对两个二维张量执行矩阵乘法。

tf.sum 函数可用于计算张量中所有元素的总和。 tf.mean 函数可用于计算张量中所有元素的平均值。

# 结论

在这篇文章中，我们了解了什么是张量以及如何在 TensorFlow.js 中使用它们。我们已经了解了如何创建张量以及如何操纵它们。我们还了解了如何使用各种函数在 TensorFlow.js 中处理张量。