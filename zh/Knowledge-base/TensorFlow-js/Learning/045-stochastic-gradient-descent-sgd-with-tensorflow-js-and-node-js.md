---
title: 045：使用 TensorFlow.js 和 Node.js 的随机梯度下降 (SGD)
description: 
published: true
date: 2023-02-02T17:36:46.296Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:36:41.300Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [045: Stochastic Gradient Descent (SGD) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/045-stochastic-gradient-descent-sgd-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 的随机梯度下降 (SGD)

随机梯度下降 (SGD) 是一种广泛用于训练深度学习模型的优化方法。 SGD 通过在最小化成本函数的方向上迭代更新模型的权重来工作。

TensorFlow.js 是一个 JavaScript 库，用于在浏览器或 Node.js 上训练和部署机器学习模型。在本教程中，我们将展示如何使用 TensorFlow.js 和 SGD 来训练简单的线性回归模型。

## 入门

首先，让我们安装 TensorFlow.js 及其依赖项。我们需要安装 Node.js 和 npm 来执行此操作。

    $ npm 安装@tensorflow/tfjs @tensorflow/tfjs-node

接下来，我们需要为我们的代码创建一个文件。我们将其称为 `sgd.js`。

## 数据

我们将在本教程中使用一个非常简单的数据集。它仅由两列组成：“x”和“y”。 `x` 是从 1 到 100 的数字列表，而 `y` 是这些数字的平方列表。

我们可以使用 TensorFlow.js 轻松生成此数据集：

```javascript
const xs = tf.range(1, 100, 1);
const ys = xs.square();
```

## 该模型

我们的模型将是一个非常简单的线性回归模型。线性回归模型用于预测连续值，如价格或数量。

我们的模型将只有一个权重和一个偏差：

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({ units: 1, inputShape: [1] }));
```

## 成本函数

成本函数是衡量我们的模型运行情况的指标。我们想要最小化成本函数，这意味着我们想要找到一组权重和偏差，使我们的模型的预测尽可能接近实际值。

有许多不同的成本函数可用于线性回归。对于本教程，我们将使用均方误差成本函数：

```javascript
function meanSquaredError(labels, predictions) {
  const error = labels.sub(predictions).square().mean();
  return error;
}
```

## 优化器

优化器是我们用来更新模型的权重和偏差的算法。 SGD 是优化器的热门选择，但还有许多其他选择。

对于本教程，我们将使用学习率为 0.1 的 SGD 优化器：

```javascript
const optimizer = tf.train.sgd(0.1);
```

## 训练模型

现在我们有了数据、模型、成本函数和优化器，可以开始训练模型了。

在 TensorFlow.js 中训练模型很容易。我们只需要在我们的模型上调用 `fit` 方法，传入我们的数据和我们想要训练的时期（迭代）的数量：

```javascript
model.fit(xs, ys, {
  epochs: 100,
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    }
  }
});
```

## 评估模型

一旦模型被训练好，我们就可以在新数据上对其进行评估。在本教程中，我们将生成一个新数据集，其“x”值介于 1 到 10 之间，“y”值介于 1 到 100 之间。

```javascript
const xs = tf.range(1, 10, 1);
const ys = tf.range(1, 100, 1);
```

我们可以使用 `predict` 方法对这个新数据进行预测：

```javascript
const predictions = model.predict(xs);
```

最后，我们可以将预测值与实际值进行比较，看看我们的模型表现如何：

```javascript
predictions.print();
ys.print();
```

## 附加信息

- [TensorFlow.js 文档](https://js.tensorflow.org/)
- [线性回归教程](https://machinelearningmastery.com/linear-regression-tutorial-machine-learning/)
- [SGD 优化器文档](https://www.tensorflow.org/api_docs/python/tf/train/GradientDescentOptimizer)