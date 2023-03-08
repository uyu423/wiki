---
title: 094：在 TensorFlow.js 和 Node.js 中构建递归神经网络 (RNN)
description: 
published: true
date: 2023-02-03T05:05:04.326Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:05:02.677Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [094: Building Recurrent Neural Networks (RNNs) in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/094-building-recurrent-neural-networks-rnns-in-tensorflow-js-and-node-js)
{.links-list}


# 介绍

递归神经网络 (RNN) 是一种人工神经网络，其中节点之间的连接沿着时间或空间序列形成有向图。这允许它展示时间序列或事件序列的时间动态行为。

在本文中，我们将在 TensorFlow.js 和 Node.js 中构建 RNN。 TensorFlow.js 是一个用于 Web 和 JavaScript 的开源硬件加速机器学习库。 Node.js 是一个跨平台的运行时环境，允许您编写服务器端 JavaScript 代码。

我们将使用 Apple, Inc. (AAPL) 从 2013 年 1 月 1 日到 2016 年 12 月 31 日的每日股价数据集。目标是预测 2017 年 1 月 1 日的开盘股价。

# 先决条件

在开始之前，您需要做一些事情：

- 人工神经网络的基础知识
- 熟悉 JavaScript
- 文本编辑器
- 网络浏览器

# 入门

## 安装 TensorFlow.js

要安装 TensorFlow.js，您可以使用 npm 或 yarn 等包管理器。

```
npm install @tensorflow/tfjs
```

```
yarn add @tensorflow/tfjs
```

或者，您可以在 HTML 文件中使用脚本标签包含 TensorFlow.js 库。

```html
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.3/dist/tf.min.js"></script>
```

## 安装 Node.js

要安装 Node.js，您可以从 [Node.js 网站](https://nodejs.org/en/) 下载安装程序。

## 下载数据集

我们将使用的数据集可在 [此处](https://www.kaggle.com/camnugent/sandp500) 获得。下载 CSV 文件并将其保存在与 JavaScript 文件相同的目录中。

# 构建循环神经网络

## 加载数据集

我们将从将数据集加载到 TensorFlow.js 开始。

```javascript
const tf = require('@tensorflow/tfjs');

const data = tf.loadCSV('AAPL.csv');
```

## 预处理数据

接下来，我们将把数据分成训练集和测试集。我们还将缩放数据，使其介于 0 和 1 之间。这是神经网络的常见预处理步骤。

```javascript
const train_data = data.slice(0, data.length - 7);
const test_data = data.slice(data.length - 7);

const train_x = train_data.map(row => row.slice(1, row.length - 1));
const train_y = train_data.map(row => row[row.length - 1]);

const test_x = test_data.map(row => row.slice(1, row.length - 1));
const test_y = test_data.map(row => row[row.length - 1]);

const x_min = Math.min(...train_x.map(row => Math.min(...row)));
const x_max = Math.max(...train_x.map(row => Math.max(...row)));

const y_min = Math.min(...train_y);
const y_max = Math.max(...train_y);

const train_x_scaled = train_x.map(row => row.map(col => (col - x_min) / (x_max - x_min)));
const test_x_scaled = test_x.map(row => row.map(col => (col - x_min) / (x_max - x_min)));

const train_y_scaled = train_y.map(val => (val - y_min) / (y_max - y_min));
const test_y_scaled = test_y.map(val => (val - y_min) / (y_max - y_min));
```

## 构建模型

现在我们可以构建 RNN。我们将从创建顺序模型开始。

```javascript
const model = tf.sequential();
```

接下来，我们将向模型添加一个循环层。该层将有 10 个单元，输入形状为 1。

```javascript
model.add(tf.layers.simpleRNN({units: 10, inputShape: [1]}));
```

最后，我们将添加一个具有单个单元且输出形状为 1 的密集层。该层将输出预测的股票价格。

```javascript
model.add(tf.layers.dense({units: 1, inputShape: [10]}));
```

## 编译模型

现在我们已经构建了模型，我们需要先编译它才能训练它。我们将使用均方误差 (MSE) 作为我们的损失函数和 Adam 优化器。

```javascript
model.compile({loss: 'meanSquaredError', optimizer: 'adam'});
```

## 训练模型

我们现在准备好训练模型了。我们将训练它 10 个时期，并使用 1 的批量大小。

```javascript
model.fit(tf.tensor2d(train_x_scaled, [train_x_scaled.length, 1]), tf.tensor2d(train_y_scaled, [train_y_scaled.length, 1]), {
  epochs: 10,
  batchSize: 1
});
```

## 预测股票价格

现在模型已经训练好了，我们可以用它来对测试集进行预测。

```javascript
const test_predictions = model.predict(tf.tensor2d(test_x_scaled, [test_x_scaled.length, 1]));
```

## 评估模型

最后，我们可以评估模型在测试集上的性能。

```javascript
const test_loss = tf.losses.meanSquaredError(test_predictions, tf.tensor2d(test_y_scaled, [test_y_scaled.length, 1]));

console.log(test_loss.dataSync());
```

# 结论

在本文中，我们了解了如何在 TensorFlow.js 和 Node.js 中构建循环神经网络。我们还看到了如何预处理数据和训练模型。

虽然我们构建的模型相当简单，但它可以扩展到更复杂的模型。例如，您可以向模型添加更多层或单元，或者您可以使用不同的优化器。

# 资源

- [TensorFlow.js 文档](https://js.tensorflow.org/)
- [Node.js 文档](https://nodejs.org/en/docs/)
- [递归神经网络](https://en.wikipedia.org/wiki/Recurrent_neural_network)
- [使用递归神经网络预测股市](https://t.co/GbU6XfjlbO?amp=1)