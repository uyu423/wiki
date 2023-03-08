---
title: 043：使用 TensorFlow.js 和 Node.js 提前停止
description: 
published: true
date: 2023-02-02T17:04:41.506Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:04:37.002Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [043: Early Stopping with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/043-early-stopping-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 提前停止

深度学习是一种神经网络技术，它彻底改变了许多领域，包括计算机视觉、自然语言处理和预测建模。 TensorFlow.js 是一个强大的开源库，用于在 JavaScript 中训练和部署深度学习模型。

在这篇文章中，我们将学习如何使用 TensorFlow.js 和 Node.js 实现提前停止，这是一种训练神经网络的技术，有助于防止过度拟合。

## 什么是早停？

提前停止是一种训练神经网络的技术，可以帮助防止过度拟合。当模型在太小或太简单的数据集上训练时，就会发生过度拟合，并且模型开始学习特定于该数据集的模式。这可能会导致模型在新数据上表现不佳。

提前停止是一种通过在模型有机会学习这些模式之前停止训练过程来对抗过度拟合的方法。我们可以通过监控模型在验证集上的性能，并在验证集上的性能开始下降时停止训练过程来做到这一点。

## 使用 TensorFlow.js 实现提前停止

我们将从使用 TensorFlow.js 创建一个简单的神经网络开始。该网络将采用两个输入值并预测第三个连续输出值。我们将在 100 个点的数据集上训练它。

```javascript
const tf = require('@tensorflow/tfjs');

// Create a neural network with two input nodes,
// one hidden layer with two nodes, and one output node
const model = tf.sequential();
model.add(tf.layers.dense({units: 2, inputShape: [2]}));
model.add(tf.layers.dense({units: 1}));

// Compile the model
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

// Generate some synthetic data for training
const xs = tf.tensor2d([[0, 0], [0, 1], [1, 0], [1, 1]]);
const ys = tf.tensor2d([[0], [1], [1], [0]]);

// Train the model
model.fit(xs, ys, {
  epochs: 100,
  validationData: [xs, ys],
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    }
  }
});
```

接下来，我们将添加一个回调，当验证集上的损失开始增加时，该回调将停止训练过程。我们将通过跟踪每个时期的损失，并将当前时期的损失与前一个时期的损失进行比较来做到这一点。如果损失增加，我们将停止训练过程。

```javascript
let previousLoss;

model.fit(xs, ys, {
  epochs: 100,
  validationData: [xs, ys],
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);

      if (previousLoss && log.loss > previousLoss) {
        model.stopTraining = true;
      }
      previousLoss = log.loss;
    }
  }
});
```

## 试试看

您可以[亲自尝试此代码](https://jsfiddle.net/jimmykim/9h5b7eLp/)。

## 附加信息

- [TensorFlow.js](https://js.tensorflow.org/)
- [Node.js](https://nodejs.org/en/)

## 进一步阅读的资源

- [使用 TensorFlow.js 进行过拟合和欠拟合](https://js.tensorflow.org/tutorials/overfitting_and_underfitting.html)
- [提前停止](https://machinelearningmastery.com/how-to-avoid-overfitting-with-early-stopping/)