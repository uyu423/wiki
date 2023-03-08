---
title: 003：了解 TensorFlow.js 核心 API
description: 
published: true
date: 2023-02-02T07:23:28.154Z
tags: 
editor: markdown
dateCreated: 2023-02-02T07:23:26.571Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [003: Understanding TensorFlow.js Core API***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/003-understanding-tensorflow-js-core-api)
{.links-list}


# 了解 TensorFlow.js 核心 API

TensorFlow.js 是一个开源网络框架，允许开发人员在浏览器中训练和部署机器学习模型。 TensorFlow.js 核心 API 是一种低级 API，允许开发人员在 JavaScript 中创建、操作和优化数值计算。

## 什么是张量？

张量是一种表示线性变换的数据结构。简单来说，张量是一个数字数组。在 TensorFlow.js 中，张量具有形状和数据类型。张量的形状是数组的大小和维数，数据类型是张量包含的数据类型（例如 float32、int32、string）。

## 创建张量

有几种方法可以在 TensorFlow.js 中创建张量。最简单的方法是使用 `tf.tensor` 函数从 JavaScript 数组创建张量：

```javascript
const a = tf.tensor([1, 2, 3, 4]);
```

`tf.tensor` 函数还允许您指定张量的形状和数据类型：

```javascript
const b = tf.tensor([1, 2, 3, 4], [2, 2], 'int32');
```

您还可以从标量（单个数字）创建张量：

```javascript
const c = tf.scalar(5);
```

## 操纵张量

可以使用 TensorFlow.js API 中的各种函数来操作张量。例如，您可以使用 `tf.add` 函数添加两个张量：

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = tf.tensor([5, 6, 7, 8]);
const c = tf.add(a, b);
```

您还可以对张量执行逐元素运算。逐元素运算是独立应用于张量中每个元素的运算。例如，您可以使用 `tf.mul` 函数将两个张量按元素相乘：

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = tf.tensor([5, 6, 7, 8]);
const c = tf.mul(a, b);
```

## 转换张量

可以使用 .toXXX 方法将张量转换为其他数据结构。例如，您可以使用 .toArray 方法将张量转换为 JavaScript 数组：

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = a.toArray(); // [1, 2, 3, 4]
```

您还可以使用 .toString 方法将张量转换为字符串：

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = a.toString(); // "1 2 3 4"
```

## 优化计算

TensorFlow.js 提供了多种优化函数，可用于优化数值计算。例如，您可以使用 `tf.clipByValue` 函数将张量值裁剪到指定范围内：

```javascript
const a = tf.tensor([-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5]);
const b = tf.clipByValue(a, -2, 2);
```

您还可以使用 `tf.addN` 函数对张量列表执行逐元素加法：

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = tf.tensor([5, 6, 7, 8]);
const c = tf.tensor([9, 10, 11, 12]);
const d = tf.addN([a, b, c]);
```

## 了解更多

TensorFlow.js 是一个强大的工具，允许开发人员在 JavaScript 中创建、操作和优化数值计算。 TensorFlow.js 核心 API 是一种低级 API，它提供了用于在 JavaScript 中创建、操作和优化数值计算的构建块。

如果您想了解有关 TensorFlow.js 的更多信息，我们建议您查看以下资源：

- TensorFlow.js 文档：https://js.tensorflow.org/
- TensorFlow.js GitHub 存储库：https://github.com/tensorflow/tfjs
- TensorFlow.js 核心 API 参考：https://js.tensorflow.org/api/core.html