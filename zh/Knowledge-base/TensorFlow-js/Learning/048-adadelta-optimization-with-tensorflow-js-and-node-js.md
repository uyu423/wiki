---
title: 048：使用 TensorFlow.js 和 Node.js 优化 Adadelta
description: 
published: true
date: 2023-02-02T18:17:52.336Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:17:47.724Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [048: Adadelta Optimization with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/048-adadelta-optimization-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 优化 Adadelta

Adadelta 是一种优化算法，可以用来代替传统的随机梯度下降 (SGD) 来训练深度神经网络。它是一种更健壮、更高效的神经网络训练方法，可与 TensorFlow.js 和 Node.js 一起使用。

## 什么是 Adadelta？

Adadelta 是一种自适应学习率优化算法，非常适合训练深度神经网络。它于2012年由Matthew D. Zeiler和Rob Fergus在论文“[ADADELTA: An Adaptive Learning Rate Method](https://arxiv.org/abs/1212.5701)”中提出，该论文获得了国际最佳论文奖2013 年学习表示会议 (ICLR)。

Adadelta 是 Adagrad 的扩展，Adagrad 是 Duchi 等人于 2011 年提出的另一种自适应学习率优化算法。在论文“[在线学习和随机优化的自适应子梯度方法](https://www.jmlr.org/papers/volume12/duchi11a/duchi11a.pdf)”中。

Adagrad 和 Adadelta 都基于每参数学习率的概念，根据损失函数相对于参数的梯度进行调整。

## Adadelta 是如何工作的？

Adadelta 优化算法通过计算神经网络中每个参数的每个参数学习率来工作。学习率根据损失函数相对于参数的梯度进行调整。

该算法有两个参数：

- `rho`：控制学习率衰减率的参数。通常使用值“0.95”。
- `epsilon`：用于数值稳定性的小参数。通常使用值“1e-6”。

Adadelta优化算法可以总结如下：

1. 将每个参数的学习率“Delta_p”初始化为“0”。
2. 对于每个训练样例“x”和相应的目标“y”：
    1. 计算损失函数关于参数 Delta_p = gradient(loss(x, y), p) 的梯度。
    2. 更新每个参数的学习率：`Delta_p = rho * Delta_p + (1 - rho) * Delta_p^2`。
    3. 更新参数：`p = p - learning_rate * Delta_p / sqrt(epsilon + accumulated_gradients)`。

## Adadelta 对比新加坡元

Adadelta 是一种比传统的随机梯度下降 (SGD) 更稳健、更高效的神经网络训练方法。

SGD 是一种流行的用于训练神经网络的优化算法，但很难调整学习率。如果学习率太低，训练过程会很慢。如果学习率太高，训练过程可能会发散。

Adadelta 不需要指定学习率。学习率根据损失函数的梯度自动调整。这使得它比 SGD 更健壮和高效。

## Adadelta 与 TensorFlow.js 和 Node.js

Adadelta 可以与 TensorFlow.js 和 Node.js 一起使用。

TensorFlow.js 是一个用于训练和部署机器学习模型的 JavaScript 库。 Node.js 是一个 JavaScript 运行时，可用于运行 TensorFlow.js 应用程序。

要将 Adadelta 与 TensorFlow.js 和 Node.js 一起使用，您需要安装 `tensorflow` 和 `@tensorflow/tfjs-node` 模块。

```
$ npm install --save tensorflow
$ npm install --save @tensorflow/tfjs-node
```

然后，您可以使用“tf.train.adadelta”函数使用 Adadelta 优化算法训练神经网络。

```javascript
const tf = require('tensorflow');

// Define the neural network.
const model = tf.sequential();
model.add(tf.layers.dense({ units: 10, inputShape: [5], activation: 'relu' }));
model.add(tf.layers.dense({ units: 1, activation: 'sigmoid' }));

// Compile the model.
model.compile({
  loss: 'binaryCrossentropy',
  optimizer: tf.train.adadelta(),
  metrics: ['accuracy']
});

// Train the model.
model.fit({ x: tf.ones([100, 5]), y: tf.zeros([100]) }, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    }
  }
});
```

## 结论

在本文中，我们了解了如何将 Adadelta 优化算法与 TensorFlow.js 和 Node.js 结合使用。 Adadelta 是一种比传统的随机梯度下降 (SGD) 更稳健、更高效的神经网络训练方法。