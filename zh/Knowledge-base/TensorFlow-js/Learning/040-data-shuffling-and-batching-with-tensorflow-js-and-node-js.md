---
title: 040：使用 TensorFlow.js 和 Node.js 进行数据洗牌和批处理
description: 
published: true
date: 2023-02-02T16:17:34.681Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:17:33.109Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [040: Data Shuffling and Batching with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/040-data-shuffling-and-batching-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 进行数据洗牌和批处理

TensorFlow.js 是一个 JavaScript 库，用于在浏览器和 Node.js 上训练和部署机器学习模型。

在本教程中，我们将学习如何使用 TensorFlow.js 对数据进行洗牌和批处理。我们将涵盖以下主题：

* 什么是数据改组，为什么它很重要？
* 如何用 TensorFlow.js 打乱数据？
* 如何使用 TensorFlow.js 批量处理数据？
* 如何与TensorFlow.js 一起shuffle 和batch 数据？

## 什么是数据改组，为什么它很重要？

在训练机器学习模型时，重要的是在每个时期之前打乱数据。这是因为，如果不打乱数据，模型可能会过度拟合数据集中的前几个样本。

数据改组是对数据集中的样本进行随机重新排序的过程。这可以在每个纪元之前或之后完成。

洗牌数据有两个主要好处：

* 它有助于防止模型过度拟合数据集中的前几个样本。
* 它可以帮助模型更快地收敛，因为它在每个时期看到不同的样本。

## 如何使用 TensorFlow.js 打乱数据？

要使用 TensorFlow.js 对数据进行混洗，我们首先需要将数据转换为“tf.data.Dataset”。

我们可以使用 `tf.data.array()` 或 `tf.data.tensor()` 方法来做到这一点：

```js
// Convert an array into a dataset
const dataset = tf.data.array([1, 2, 3, 4, 5]);

// Convert a tensor into a dataset
const dataset = tf.data.tensor([1, 2, 3, 4, 5]);
```

一旦我们有了数据集，我们就可以使用`tf.data. shuffle()` 方法来打乱数据：

```js
const shuffledDataset = dataset.shuffle();
```

## 如何使用 TensorFlow.js 批量处理数据？

要使用 TensorFlow.js 批处理数据，我们首先需要将数据转换为“tf.data.Dataset”。

我们可以使用 `tf.data.array()` 或 `tf.data.tensor()` 方法来做到这一点：

```js
// Convert an array into a dataset
const dataset = tf.data.array([1, 2, 3, 4, 5]);

// Convert a tensor into a dataset
const dataset = tf.data.tensor([1, 2, 3, 4, 5]);
```

一旦我们有了数据集，我们就可以使用`tf.data. batch()` 方法来批处理数据：

```js
const batchedDataset = dataset.batch(2);
```

## 如何使用 TensorFlow.js 对数据进行 shuffle 和 batch？

要使用 TensorFlow.js 对数据进行混洗和批处理，我们首先需要将数据转换为“tf.data.Dataset”。

我们可以使用 `tf.data.array()` 或 `tf.data.tensor()` 方法来做到这一点：

```js
// Convert an array into a dataset
const dataset = tf.data.array([1, 2, 3, 4, 5]);

// Convert a tensor into a dataset
const dataset = tf.data.tensor([1, 2, 3, 4, 5]);
```

一旦我们有了数据集，我们就可以使用`tf.data. shuffle()` 和 `tf.data. batch()` 方法对数据进行洗牌和批处理：

```js
const shuffledAndBatchedDataset = dataset.shuffle().batch(2);
```