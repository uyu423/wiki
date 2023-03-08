---
title: 044：使用 TensorFlow.js 和 Node.js 进行梯度下降
description: 
published: true
date: 2023-02-02T17:18:33.719Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:18:32.053Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [044: Gradient Descent with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/044-gradient-descent-with-tensorflow-js-and-node-js)
{.links-list}


# 044：使用 TensorFlow.js 和 Node.js 进行梯度下降

梯度下降是一种优化算法，用于找到使成本函数最小化的参数值（例如权重和偏差）。它是一种用于训练神经网络的流行算法。

TensorFlow.js 是一个用于训练和部署机器学习模型的 JavaScript 库。 Node.js 是一个 JavaScript 运行时，允许您在服务器上运行 JavaScript 代码。

在本教程中，我们将使用 TensorFlow.js 和 Node.js 训练一个简单的神经网络来执行线性回归。我们将使用梯度下降来找到网络权重和偏差的最佳值。

## 什么是线性回归？

线性回归是一种用于预测连续值的机器学习算法。例如，我们可以使用线性回归来根据房屋的大小、卧室数量和浴室数量来预测房屋的价格。

线性回归是一种监督学习，这意味着我们需要为算法提供训练数据。训练数据由一组输入值 (x) 和相应的输出值 (y) 组成。对于我们的房价示例，输入值可以是大小、卧室数量和浴室数量，输出值是价格。

## 线性回归如何工作？

线性回归的工作原理是找到一组权重 (w) 和偏差 (b)，这些权重 (w) 和偏差 (b) 可最大限度地减少预测值 (ŷ) 与实际值 (y) 之间的误差。

![线性回归](https://cdn-images-1.medium.com/max/1600/1*d7Cg5UC5tM7GtLjTvW0MzA.png)

预测值的计算方法是将输入值 (x) 乘以权重 (w)，然后加上偏差 (b)。

![预测值](https://cdn-images-1.medium.com/max/1600/1*j_q-F1lrVxKbV-_d7JKV2w.png)

通过计算预测值 (ŷ) 和实际值 (y) 之间的差值来计算误差。

![错误](https://cdn-images-1.medium.com/max/1600/1*7VtEOzAj_sXXuTzXrT7yYQ.png)

然后我们可以使用梯度下降来找到最小化错误的权重和偏差。

## 什么是梯度下降？

梯度下降是一种优化算法，用于找到使成本函数最小化的参数值（例如权重和偏差）。

![成本函数](https://cdn-images-1.medium.com/max/1600/1*Xu7B5y9gp0iL5ooBj7LtWw.png)

成本函数衡量预测值 (ŷ) 与实际值 (y) 的差距。我们想找到使成本函数最小化的权重和偏差。

![权重和偏差](https://cdn-images-1.medium.com/max/1600/1*n6sVxWAz7VUgX6Sj7K1vUw.png)

梯度下降通过在最小化成本函数的方向上迭代更新权重和偏差来工作。更新的大小由学习率决定。

![梯度下降](https://cdn-images-1.medium.com/max/1600/1*jw7UwKLnA0sCgq_QPV-_lA.png)

## 在 TensorFlow.js 中实现梯度下降

现在我们已经了解了梯度下降的工作原理，让我们看看如何在 TensorFlow.js 中实现它。

首先，我们需要定义输入值 (x)、输出值 (y) 以及权重 (w) 和偏差 (b) 的初始值。

```javascript
// Define the input values
const x = tf.tensor([
  [1, 2, 3, 4],
  [2, 3, 4, 5],
  [3, 4, 5, 6],
  [4, 5, 6, 7]
]);

// Define the output values
const y = tf.tensor([
  [2],
  [4],
  [6],
  [8]
]);

// Define the initial values for the weights and biases
const w = tf.variable(tf.zeros([4, 1]));
const b = tf.variable(tf.zeros([1]));
```

接下来，我们需要定义代价函数。我们将使用均方误差成本函数。

```javascript
// Define the cost function
function cost(pred, labels) {
  const diff = pred.sub(labels);
  const sqrDiff = diff.square();
  const meanSqrDiff = sqrDiff.mean();
  return meanSqrDiff;
}
```

现在，我们可以定义梯度下降算法。我们将在最小化成本函数的方向上迭代更新权重和偏差。

```javascript
// Define the gradient descent algorithm
async function train(x, y, w, b, epochs, learningRate) {
  for (let i = 0; i < epochs; i++) {
    // Calculate the predicted values
    const pred = x.matMul(w).add(b);

    // Calculate the cost
    const c = cost(pred, y);

    // Print the cost
    console.log("Epoch: " + i + " Cost: " + c.dataSync()[0]);

    // Calculate the gradients
    const grads = tf.grads(c, [w, b]);
    const dw = grads[0];
    const db = grads[1];

    // Update the weights and biases
    w.sub(dw.mul(learningRate));
    b.sub(db.mul(learningRate));
  }
}
```

最后，我们可以调用 train 函数来训练模型。我们将以 0.1 的学习率训练 100 个 epoch 的模型。

```javascript
// Train the model
train(x, y, w, b, 100, 0.1);
```

## 训练模型

现在我们已经了解了如何在 TensorFlow.js 中实现梯度下降，让我们看看如何使用它来训练神经网络来执行线性回归。

首先，我们需要定义输入值 (x)、输出值 (y) 以及权重 (w) 和偏差 (b) 的初始值。

```javascript
// Define the input values
const x = tf.tensor([
  [1, 2, 3, 4],
  [2, 3, 4, 5],
  [3, 4, 5, 6],
  [4, 5, 6, 7]
]);

// Define the output values
const y = tf.tensor([
  [2],
  [4],
  [6],
  [8]
]);

// Define the initial values for the weights and biases
const w = tf.variable(tf.zeros([4, 1]));
const b = tf.variable(tf.zeros([1]));
```

接下来，我们需要定义代价函数。我们将使用均方误差成本函数。

```javascript
// Define the cost function
function cost(pred, labels) {
  const diff = pred.sub(labels);
  const sqrDiff = diff.square();
  const meanSqrDiff = sqrDiff.mean();
  return meanSqrDiff;
}
```

现在，我们可以定义梯度下降算法。我们将在最小化成本函数的方向上迭代更新权重和偏差。

```javascript
// Define the gradient descent algorithm
async function train(x, y, w, b, epochs, learningRate) {
  for (let i = 0; i < epochs; i++) {
    // Calculate the predicted values
    const pred = x.matMul(w).add(b);

    // Calculate the cost
    const c = cost(pred, y);

    // Print the cost
    console.log("Epoch: " + i + " Cost: " + c.dataSync()[0]);

    // Calculate the gradients
    const grads = tf.grads(c, [w, b]);
    const dw = grads[0];
    const db = grads[1];

    // Update the weights and biases
    w.sub(dw.mul(learningRate));
    b.sub(db.mul(learningRate));
  }
}
```

最后，我们可以调用 train 函数来训练模型。我们将以 0.1 的学习率训练 100 个 epoch 的模型。

```javascript
// Train the model
train(x, y, w, b, 100, 0.1);
```

## 测试模型

现在我们已经训练了模型，让我们看看它在一些测试数据上的表现如何。

首先，我们需要定义测试数据。

```javascript
// Define the test data
const xTest = tf.tensor([
  [5, 6, 7, 8],
  [6, 7, 8, 9],
  [7, 8, 9, 10],
  [8, 9, 10, 11]
]);

// Define the expected output values
const yTest = tf.tensor([
  [10],
  [12],
  [14],
  [16]
]);
```

接下来，我们需要计算预测值。

```javascript
// Calculate the predicted values
const pred = xTest.matMul(w).add(b);
```

最后，我们可以将预测值与预期输出值进行比较。

```javascript
// Compare the predicted values to the expected output values
pred.print();
yTest.print();
```

## 结论

在本教程中，我们了解了如何使用梯度下降训练神经网络来执行线性回归。我们还了解了如何在 TensorFlow.js 中实现梯度下降以及如何使用它来训练神经网络。