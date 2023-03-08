---
title: 038：使用 TensorFlow.js 和 Node.js 进行数据预处理
description: 
published: true
date: 2023-02-02T15:43:30.873Z
tags: 
editor: markdown
dateCreated: 2023-02-02T15:43:29.349Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [038: Data Preprocessing with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/038-data-preprocessing-with-tensorflow-js-and-node-js)
{.links-list}


# 038：使用 TensorFlow.js 和 Node.js 进行数据预处理

在本文中，我们将学习如何预处理数据以用于 TensorFlow.js 和 Node.js。

数据预处理是机器学习中的关键步骤。人们常说数据预处理占机器学习工作的 80%。这样做的原因是数据的质量对机器学习算法的性能有巨大的影响。

有许多不同的方法来预处理数据。您使用的方法将取决于您拥有的数据类型和您使用的机器学习算法。

在这篇文章中，我们将重点介绍两种数据预处理方法：

- 归一化
- 数据扩充

## 归一化

规范化是一种用于重新缩放数据以使其在特定范围内的技术。规范化数据的方法有很多种，但最常用的方法是将数据重新缩放到范围 [0, 1]。

这可以使用 min-max 方法来完成，该方法重新缩放数据，使最小值为 0，最大值为 1。

为此，我们首先需要找到数据的最小值和最大值。然后我们可以使用以下公式重新缩放数据：

```
x' = (x - min) / (max - min)
```

其中 x 是原始数据，x' 是重新缩放后的数据，min 是最小值，max 是最大值。

我们可以使用 min-max 方法重新调整训练集中的数据。然后我们可以使用重新缩放的数据来训练我们的机器学习算法。

## 数据扩充

数据增强是一种用于人为增加训练数据大小的技术。这是通过从现有数据创建新数据点来完成的。

有许多不同的方法可以进行数据扩充。最常见的方法是使用随机变换来创建新的数据点。

例如，我们可以通过少量随机旋转图像来创建一个新的数据点。我们还可以随机裁剪图像以创建新的数据点。

数据增强是一种强大的技术，可用于提高机器学习算法的性能。

## 结论

在这篇文章中，我们了解了两种数据预处理方法：归一化和数据扩充。我们还学习了如何在 TensorFlow.js 和 Node.js 中实现这些方法。