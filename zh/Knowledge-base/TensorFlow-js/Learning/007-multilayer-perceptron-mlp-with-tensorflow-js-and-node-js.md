---
title: 007：使用 TensorFlow.js 和 Node.js 的多层感知器 (MLP)
description: 
published: true
date: 2023-02-02T08:17:32.617Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:17:30.974Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [007: Multilayer Perceptron (MLP) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/007-multilayer-perceptron-mlp-with-tensorflow-js-and-node-js)
{.links-list}


## 介绍

在本文中，我们将介绍如何使用 TensorFlow.js 和 Node.js 构建多层感知器 (MLP)。我们将回顾神经网络和深度学习背后的基本概念，以及如何使用 TensorFlow.js 实现它们。到本文结束时，您将能够构建自己的神经网络并使用它们来解决现实世界中的问题。

## 什么是多层感知器？

多层感知器 (MLP) 是一种神经网络。神经网络是一种机器学习算法，用于对数据中的复杂模式进行建模。 MLP 是一种特定类型的神经网络，由多层神经元组成。

MLP 的第一层是输入层，它接收输入数据。第二层是隐藏层，它将输入数据转换为新的表示。隐藏层之后是输出层，它产生 MLP 的输出。

## 使用 TensorFlow.js 构建 MLP

TensorFlow.js 是一个用于构建神经网络和机器学习模型的 JavaScript 库。它可以在浏览器和 Node.js 中使用。

为了使用 TensorFlow.js，我们首先需要安装它。我们可以使用节点包管理器 (NPM) 执行此操作：

```
npm install @tensorflow/tfjs
```

安装 TensorFlow.js 后，我们可以将其导入到我们的项目中：

```javascript
const tf = require('@tensorflow/tfjs');
```

现在我们已经安装并导入了 TensorFlow.js，我们可以开始构建我们的 MLP。

第一步是定义输入层。我们可以使用 `input` 函数来做到这一点：

```javascript
const inputLayer = tf.input({shape: [2]});
```

`input` 函数将一个对象作为参数。该对象的“shape”属性定义了输入数据的形状。在本例中，我们使用的是二维输入，因此 `shape` 属性设置为 `[2]`。

接下来，我们需要定义隐藏层。我们可以使用 `layers` 函数来做到这一点：

```javascript
const hiddenLayer = tf.layers.dense({
  units: 4,
  activation: 'sigmoid',
  inputShape: [2]
});
```

`layers` 函数以一个对象作为参数。 `units` 属性定义层中神经元的数量。 `activation` 属性定义了层的激活函数。在这种情况下，我们使用 sigmoid 激活函数。 `inputShape` 属性定义输入数据的形状。

最后，我们需要定义输出层。我们可以使用 `layers` 函数来做到这一点：

```javascript
const outputLayer = tf.layers.dense({
  units: 1,
  activation: 'sigmoid',
  inputShape: [4]
});
```

与隐藏层一样，“units”属性定义了层中神经元的数量。 `activation` 属性定义了层的激活函数。在这种情况下，我们再次使用 sigmoid 激活函数。 `inputShape` 属性定义输入数据的形状。

现在我们已经定义了 MLP 的层，我们需要连接它们。我们可以使用 `sequential` 函数来做到这一点：

```javascript
const model = tf.sequential();
```

`sequential` 函数将层数组作为参数。在本例中，我们传入了输入层、隐藏层和输出层。

现在我们的模型已经定义好了，我们需要编译它。我们可以使用 `compile` 函数来做到这一点：

```javascript
model.compile({
  optimizer: 'sgd',
  loss: 'meanSquaredError'
});
```

`compile` 函数将一个对象作为参数。 `optimizer` 属性定义了将用于训练模型的优化器。在这种情况下，我们使用随机梯度下降 (SGD) 优化器。 `loss` 属性定义了将用于评估模型的损失函数。在这种情况下，我们使用均方误差 (MSE) 损失函数。

现在我们的模型已经编译好了，我们可以训练它了。我们可以使用 `fit` 函数来做到这一点：

```javascript
model.fit(x, y, {
  epochs: 100,
  batchSize: 32
});
```

`fit` 函数采用三个参数：训练数据 (`x`)、目标数据 (`y`) 和指定训练参数的对象。 `epochs` 属性定义了训练时期的数量。 `batchSize` 属性定义每个训练批次中的样本数。

一旦模型被训练好，我们就可以用它来进行预测。我们可以使用 `predict` 函数来做到这一点：

```javascript
model.predict(x).print();
```

`predict` 函数接受一组输入数据 (`x`) 并返回一组预测。 `print` 函数将预测打印到控制台。

## 结论

在本文中，我们介绍了如何使用 TensorFlow.js 和 Node.js 构建多层感知器 (MLP)。我们回顾了神经网络和深度学习背后的基本概念，以及如何使用 TensorFlow.js 实现它们。到本文结束时，您应该能够构建自己的神经网络并使用它们来解决现实世界中的问题。