---
title: 008：使用 TensorFlow.js 和 Node.js 的卷积神经网络 (CNN)
description: 
published: true
date: 2023-02-02T08:37:03.777Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:36:59.258Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [008: Convolutional Neural Networks (CNN) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/008-convolutional-neural-networks-cnn-with-tensorflow-js-and-node-js)
{.links-list}


# 介绍

在本文中，我们将研究如何在 TensorFlow.js 和 Node.js 中构建卷积神经网络 (CNN)。我们将使用著名的图像识别数据集 MNIST 数据集来训练我们的 CNN。

卷积神经网络是一种特别适合图像识别任务的神经网络。这是因为它们能够利用图像的空间结构。

# 在 TensorFlow.js 中构建 CNN

我们将从了解如何在 TensorFlow.js 中构建 CNN 开始。如果您不熟悉 TensorFlow.js，它是一个在浏览器中运行的用于机器学习的 JavaScript 库。

首先，我们需要加载 MNIST 数据集。 MNIST 数据集是手写数字图像的集合，每个数字为 28x28 像素。

我们可以使用 TensorFlow.js 的 `tf.data.mnist` 函数加载 MNIST 数据集。此函数返回一个“数据集”对象，然后我们可以使用它来训练我们的 CNN。

```javascript
const mnistData = tf.data.mnist({
  train: true,
  testData: false
});
```

接下来，我们需要定义卷积神经网络。我们将使用顺序模型，这是一种由线性层叠组成的神经网络。

我们将从添加一个“Flatten”层开始，它获取我们的 28x28 图像并将它们展平成一个包含 784 个元素的向量。

```javascript
const model = tf.sequential();

model.add(tf.layers.flatten({
  inputShape: [28, 28]
}));
```

接下来，我们将添加一个“密集”层。这是一个全连接层，这意味着该层中的每个神经元都连接到上一层中的每个神经元。

我们将配置“密集”层以具有 128 个神经元并使用“relu”激活函数。 `relu` 激活函数是神经网络的常见选择。它对任何小于 0 的输入输出 0，对任何大于或等于 0 的输入输出输入。

```javascript
model.add(tf.layers.dense({
  units: 128,
  activation: 'relu',
  inputShape: [784]
}));
```

最后，我们将添加一个包含 10 个神经元和 softmax 激活函数的“密集”层。 `softmax` 激活函数是神经网络输出层的常见选择。它输出 10 个可能数字的概率分布。

```javascript
model.add(tf.layers.dense({
  units: 10,
  activation: 'softmax',
  inputShape: [128]
}));
```

现在我们已经定义了我们的模型，我们需要编译它。当我们编译模型时，我们指定了损失函数和优化器。

损失函数是衡量模型执行情况的指标。我们想要最小化损失函数，这意味着我们希望模型做出尽可能接近真实标签的预测。

优化器是一种用于更新模型以最小化损失函数的算法。有许多不同的优化器可用，但我们将使用 `sgd` 优化器。

```javascript
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'sgd'
});
```

现在我们的模型已经编译好了，我们可以训练它了。我们将训练它 10 个时期，这意味着该模型将看到整个 MNIST 数据集 10 次。

```javascript
model.fit(mnistData, {
  epochs: 10
});
```

# 在 Node.js 中构建 CNN

现在我们已经了解了如何在 TensorFlow.js 中构建 CNN，让我们来看看如何在 Node.js 中执行此操作。

首先，我们需要加载 MNIST 数据集。 MNIST 数据集是手写数字图像的集合，每个数字为 28x28 像素。

我们可以使用 `mnist` 包加载 MNIST 数据集。这个包返回一个 `Dataset` 对象，我们可以用它来训练我们的 CNN。

```javascript
const mnist = require('mnist');

const mnistData = mnist.training(0, 60000);
```

接下来，我们需要定义卷积神经网络。我们将使用顺序模型，这是一种由线性层叠组成的神经网络。

我们将从添加一个“Flatten”层开始，它获取我们的 28x28 图像并将它们展平成一个包含 784 个元素的向量。

```javascript
const model = tf.sequential();

model.add(tf.layers.flatten({
  inputShape: [28, 28]
}));
```

接下来，我们将添加一个“密集”层。这是一个全连接层，这意味着该层中的每个神经元都连接到上一层中的每个神经元。

我们将配置“密集”层以具有 128 个神经元并使用“relu”激活函数。 `relu` 激活函数是神经网络的常见选择。它对任何小于 0 的输入输出 0，对任何大于或等于 0 的输入输出输入。

```javascript
model.add(tf.layers.dense({
  units: 128,
  activation: 'relu',
  inputShape: [784]
}));
```

最后，我们将添加一个包含 10 个神经元和 softmax 激活函数的“密集”层。 `softmax` 激活函数是神经网络输出层的常见选择。它输出 10 个可能数字的概率分布。

```javascript
model.add(tf.layers.dense({
  units: 10,
  activation: 'softmax',
  inputShape: [128]
}));
```

现在我们已经定义了我们的模型，我们需要编译它。当我们编译模型时，我们指定了损失函数和优化器。

损失函数是衡量模型执行情况的指标。我们想要最小化损失函数，这意味着我们希望模型做出尽可能接近真实标签的预测。

优化器是一种用于更新模型以最小化损失函数的算法。有许多不同的优化器可用，但我们将使用 `sgd` 优化器。

```javascript
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'sgd'
});
```

现在我们的模型已经编译好了，我们可以训练它了。我们将训练它 10 个时期，这意味着该模型将看到整个 MNIST 数据集 10 次。

```javascript
model.fit(mnistData, {
  epochs: 10
});
```

# 结论

在本文中，我们了解了如何在 TensorFlow.js 和 Node.js 中构建卷积神经网络。我们还了解了如何在 MNIST 数据集上训练这些网络。