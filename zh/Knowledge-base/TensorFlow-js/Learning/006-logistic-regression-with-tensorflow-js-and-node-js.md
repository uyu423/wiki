---
title: 006：使用 TensorFlow.js 和 Node.js 进行逻辑回归
description: 
published: true
date: 2023-02-02T08:04:27.366Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:04:25.795Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [006: Logistic Regression with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/006-logistic-regression-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 进行逻辑回归

在本文中，我们将学习如何使用 TensorFlow.js 和 Node.js 构建逻辑回归模型。

逻辑回归是一种预测二元结果的统计方法。也就是说，它可以用来预测事件是否会发生。例如，我们可以使用逻辑回归来根据某些特征来预测患者是否会患上某种疾病。

逻辑回归是一种线性回归，但有一些重要的区别。首先，结果变量是二进制的，这意味着它只能取两个值（0 或 1）。其次，该模型使用最大似然估计而不是最小二乘法进行拟合。

## 入门

首先，我们需要安装 TensorFlow.js 和 Node.js。我们可以使用以下命令来做到这一点：

```
npm install -g tensorflow
npm install -g node
```

安装 TensorFlow.js 和 Node.js 后，我们可以创建一个名为“logistic-regression.js”的新文件并开始编码。

## 数据

第一步是加载我们的数据。我们将使用 `tensorflow.js` 库将数据加载到 `tf.tensor` 对象中。

```javascript
const tf = require('tensorflow');

// Load the data
const data = tf.tensor([
  [1, 2],
  [2, 3],
  [3, 4],
  [4, 5],
]);
```

## 模型

接下来，我们需要定义我们的模型。我们将使用具有两个输入特征（“x1”和“x2”）和一个输出（“y”）的逻辑回归模型。

```javascript
// Define the model
const model = tf.sequential();
model.add(tf.layers.dense({ units: 1, inputShape: [2] }));
model.compile({ loss: 'binaryCrossentropy', optimizer: 'sgd' });
```

## 训练

现在我们有了数据和模型，我们可以训练我们的模型了。我们将使用 `fit` 方法在数据上训练我们的模型。

```javascript
// Train the model
model.fit(data, tf.tensor([1, 1, 0, 0]), {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    },
  },
});
```

## 预言

一旦我们的模型被训练好，我们就可以用它来进行预测。我们将使用 `predict` 方法来预测新数据的输出。

```javascript
// Make predictions
model.predict(tf.tensor([[5, 6]])).print(); // [[0.5]]
model.predict(tf.tensor([[6, 7]])).print(); // [[0.5]]
```

正如我们所见，我们的模型将两个输入的输出预测为 0.5。这意味着我们的模型预测事件发生的可能性为 50%。

## 结论

在本文中，我们学习了如何使用 TensorFlow.js 和 Node.js 构建逻辑回归模型。我们还了解了如何使用我们的模型对新数据进行预测。