---
title: 011：使用 TensorFlow.js 和 Node.js 的门控循环单元 (GRU)
description: 
published: true
date: 2023-02-02T09:17:22.444Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:17:20.860Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [011: Gated Recurrent Unit (GRU) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/011-gated-recurrent-unit-gru-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 的门控循环单元 (GRU)

在本文中，我们将了解门控循环单元 (GRU) 以及如何使用 TensorFlow.js 和 Node.js 实现它们。

## 什么是门控循环单元？

GRU 是一种循环神经网络 (RNN)。 RNN 是可以处理数据序列（例如文本、音频或时间序列数据）的神经网络。

GRU 是一种 RNN，它使用门来控制网络中的信息流。门帮助网络更好地学习长期依赖关系。

## 使用 TensorFlow.js 实现 GRU

我们将使用 TensorFlow.js 来实现 GRU。 TensorFlow.js 是一个 JavaScript 库，用于在浏览器和 Node.js 中训练和部署机器学习模型。

首先，我们需要安装 TensorFlow.js。我们可以使用以下命令执行此操作：

```
npm install @tensorflow/tfjs
```

接下来，我们需要加载我们将用于训练模型的数据。我们将使用 MNIST 数据集，它是手写数字的数据集。

我们可以使用以下代码加载 MNIST 数据集：

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MNIST dataset.
const mnistData = require('mnist-data');

// Convert the MNIST data to a TensorFlow.js tensor.
const mnistTensor = tf.tensor3d(mnistData.images, [mnistData.images.length, 28, 28]);
```

现在我们已经加载了数据，我们可以定义模型了。我们将使用具有 64 个单元的 GRU。

```javascript
// Define the model.
const model = tf.sequential();
model.add(tf.layers.gru({units: 64, inputShape: [28, 28]}));
model.add(tf.layers.dense({units: 10, activation: 'softmax'}));
```

接下来，我们需要编译模型。我们将使用 Adam 优化器和分类交叉熵损失函数。

```javascript
// Compile the model.
model.compile({optimizer: 'adam', loss: 'categoricalCrossentropy', metrics: ['accuracy']});
```

现在，我们可以训练模型了。我们将训练它 10 个 epoch。

```javascript
// Train the model.
model.fit(mnistTensor, mnistData.labels, {epochs: 10}).then(() => {
  // The model is trained!
});
```

就是这样！我们现在已经训练了一个 GRU 来对手写数字进行分类。

## 使用 Node.js 实现 GRU

我们也可以使用 Node.js 来训练 GRU。 Node.js 是一个 JavaScript 运行时，允许您在浏览器之外运行 JavaScript 代码。

首先，我们需要安装 TensorFlow.js。我们可以使用以下命令执行此操作：

```
npm install @tensorflow/tfjs
```

接下来，我们需要加载我们将用于训练模型的数据。我们将使用 MNIST 数据集，它是手写数字的数据集。

我们可以使用以下代码加载 MNIST 数据集：

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MNIST dataset.
const mnistData = require('mnist-data');

// Convert the MNIST data to a TensorFlow.js tensor.
const mnistTensor = tf.tensor3d(mnistData.images, [mnistData.images.length, 28, 28]);
```

现在我们已经加载了数据，我们可以定义模型了。我们将使用具有 64 个单元的 GRU。

```javascript
// Define the model.
const model = tf.sequential();
model.add(tf.layers.gru({units: 64, inputShape: [28, 28]}));
model.add(tf.layers.dense({units: 10, activation: 'softmax'}));
```

接下来，我们需要编译模型。我们将使用 Adam 优化器和分类交叉熵损失函数。

```javascript
// Compile the model.
model.compile({optimizer: 'adam', loss: 'categoricalCrossentropy', metrics: ['accuracy']});
```

现在，我们可以训练模型了。我们将训练它 10 个 epoch。

```javascript
// Train the model.
model.fit(mnistTensor, mnistData.labels, {epochs: 10}).then(() => {
  // The model is trained!
});
```

就是这样！我们现在已经训练了一个 GRU 来对手写数字进行分类。