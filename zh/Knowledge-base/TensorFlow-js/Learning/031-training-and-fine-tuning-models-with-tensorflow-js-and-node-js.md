---
title: 031：使用 TensorFlow.js 和 Node.js 训练和微调模型
description: 
published: true
date: 2023-02-02T14:17:56.966Z
tags: 
editor: markdown
dateCreated: 2023-02-02T14:17:55.374Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [031: Training and Fine-Tuning Models with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/031-training-and-fine-tuning-models-with-tensorflow-js-and-node-js)
{.links-list}


# 031：使用 TensorFlow.js 和 Node.js 训练和微调模型

TensorFlow.js 是一个用于数值计算的开源库，可让您在浏览器中创建和训练机器学习模型。 Node.js 是一个 JavaScript 运行时，允许您在浏览器之外运行 JavaScript 代码。在本文中，我们将向您展示如何使用 TensorFlow.js 和 Node.js 来训练和微调机器学习模型。

## 安装 TensorFlow.js

要安装 TensorFlow.js，您需要安装 Node.js 和 npm（Node.js 包管理器）。您可以通过在终端中运行以下命令来检查是否安装了 Node.js：

```
node -v
```

如果您没有安装 Node.js，可以在[此处](https://nodejs.org/en/) 下载它。

安装 Node.js 和 npm 后，您可以使用以下命令安装 TensorFlow.js：

```
npm install @tensorflow/tfjs
```

## 训练模型

现在您已经安装了 TensorFlow.js，您可以开始训练您自己的机器学习模型。在本节中，我们将向您展示如何训练简单的线性回归模型。

首先，让我们创建一些训练数据。我们将使用内置的 tf.tensor2d() 函数来创建具有 10 行和 1 列的二维张量（数组的数组）。我们将用均值为 0 且标准差为 1 的正态分布中的随机数填充张量。

```javascript
const xs = tf.tensor2d([-1, 0, 1, 2, 3, 4], [6, 1]);
const ys = tf.tensor2d([-3, -1, 1, 3, 5, 7], [6, 1]);
```

接下来，我们将定义我们的模型。我们将使用 tf.sequential() 函数来创建顺序模型，它是层的线性堆栈。然后，我们将使用 tf.layers.dense() 函数为模型添加一个密集层。密集层是全连接层，这意味着前一层中的所有节点都连接到密集层中的所有节点。我们将指定密集层有 1 个输出节点，输入形状为 [1]。

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));
```

现在我们已经定义了我们的模型，我们需要编译它。编译模型将为训练配置模型。我们将使用 tf.train.sgd() 函数来创建随机梯度下降优化器。优化器将用于最小化训练期间的损失函数。我们还将指定我们要针对均方误差进行优化。

```javascript
model.compile({optimizer: tf.train.sgd(0.1), loss: 'meanSquaredError'});
```

现在我们的模型已经编译好了，我们可以开始训练它了。我们将使用 model.fit() 函数来训练模型。我们将指定训练数据（xs 和 ys）、时期数 (100) 和批量大小 (1)。时代是模型将通过训练数据的次数。批量大小是模型在更新模型权重之前将使用的训练示例数。

```javascript
model.fit(xs, ys, {epochs: 100, batchSize: 1});
```

## 做出预测

现在我们的模型已经训练好了，我们可以用它来进行预测。我们将使用 model.predict() 函数进行预测。我们将传入值为 3 的一维张量。模型将输出值为 9 的一维张量。

```javascript
model.predict(tf.tensor2d([3], [1, 1])).print();
```

## 微调模型

拥有经过训练的模型后，您可能希望对其进行微调以提高其性能。在本节中，我们将向您展示如何微调预训练模型。

我们将从加载预训练模型开始。我们将使用 tf.loadLayersModel() 函数加载模型。我们需要指定模型的 URL。您可以在 [此处](https://github.com/tensorflow/tfjs-models/tree/master/models) 找到预训练模型列表。

```javascript
const model = tf.loadLayersModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

现在我们已经加载了模型，我们需要编译它。我们将使用与以前相同的 compile() 函数。但是，这次我们将指定我们要优化分类准确性。

```javascript
model.compile({optimizer: tf.train.sgd(0.0001), loss: 'categoricalCrossentropy', metrics: ['accuracy']});
```

现在我们可以开始训练模型了。我们将再次使用 fit() 函数。但是，这次我们将指定轮数 (5) 和验证数据（xs 和 ys）。验证数据用于在每个时期后评估模型。

```javascript
model.fit(xs, ys, {epochs: 5, validationData: [xs, ys]});
```

训练完模型后，我们可以用它来进行预测。我们将再次使用 predict() 函数。这次我们将传递一张狗的图像。该模型将输出一组概率，每个类别一个。最高概率将是模型预测图像所属的类别。

```javascript
model.predict(tf.tensor2d([image], [1, 224, 224, 3])).print();
```

## 结论

在本文中，我们向您展示了如何使用 TensorFlow.js 和 Node.js 来训练和微调机器学习模型。