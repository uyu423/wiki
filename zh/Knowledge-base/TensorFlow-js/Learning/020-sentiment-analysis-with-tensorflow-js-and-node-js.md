---
title: 020：使用 TensorFlow.js 和 Node.js 进行情感分析
description: 
published: true
date: 2023-02-02T11:36:30.910Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:36:29.273Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [020: Sentiment Analysis with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/020-sentiment-analysis-with-tensorflow-js-and-node-js)
{.links-list}


# 020：使用 TensorFlow.js 和 Node.js 进行情感分析

## 介绍

在本文中，我们将介绍如何使用 TensorFlow.js 和 Node.js 进行情绪分析。情感分析是通过计算确定一篇文章是积极的、消极的还是中性的过程。它通常用于衡量社交媒体上的公众舆论，并具有广泛的其他应用。

我们将使用 TensorFlow.js 库，这是一个用于训练和部署机器学习模型的 JavaScript 库。 TensorFlow.js 可以在 Node.js 环境中使用，我们将使用它来进行情绪分析。

## 入门

在我们开始之前，您需要进行一些设置。首先，您需要在计算机上安装 Node.js。您可以从 [Node.js 网站](https://nodejs.org/en/) 下载它。

安装 Node.js 后，您需要安装 TensorFlow.js 库。您可以使用以下命令执行此操作：

```
npm install @tensorflow/tfjs
```

接下来，您需要为我们的情绪分析程序创建一个新文件。我们将其称为“sentiment.js”。您可以使用您最喜欢的文本编辑器来完成此操作。

## 初始化 TensorFlow.js 环境

我们需要在 sentiment.js 文件中做的第一件事是初始化 TensorFlow.js 环境。我们可以使用以下代码来做到这一点：

```javascript
const tf = require('@tensorflow/tfjs');
```

这会将 TensorFlow.js 库加载到我们的程序中，以便我们可以使用它。

## 加载数据集

现在我们已经设置了 TensorFlow.js 环境，我们需要加载我们将用于训练情绪分析模型的数据集。我们将使用 [IMDB 电影评论数据集](https://ai.stanford.edu/~amaas/data/sentiment/)。该数据集包含 50,000 条电影评论，每条评论的标签为 0（负面）或 1（正面）。

我们可以使用以下代码将此数据集加载到我们的程序中：

```javascript
const dataset = tf.data.csv('https://storage.googleapis.com/tfjs-datasets/imdb_reviews.csv');
```

这会将数据集加载到“dataset”变量中。

## 预处理数据集

在我们使用数据集进行训练之前，我们需要对其进行预处理。这涉及将数据集拆分为训练集和测试集，并将文本数据转换为数值向量。

我们可以使用以下代码来做到这一点：

```javascript
const [train, test] = dataset.split(0.8);

const vectorizer = new tf.layers.Embedding(10000, 16);

const trainX = train.map(example => vectorizer.apply(example.text));
const testX = test.map(example => vectorizer.apply(example.text));
const trainY = train.map(example => example.label);
const testY = test.map(example => example.label);
```

此代码会将数据集拆分为训练集和测试集，然后对文本数据进行矢量化。向量化数据将分别存储在训练集和测试集的“trainX”和“testX”变量中。训练集和测试集的标签将分别存储在“trainY”和“testY”变量中。

## 构建模型

现在我们已经对数据集进行了预处理，我们可以构建将用于情绪分析的模型。我们将使用一个带有一个隐藏层的简单神经网络。

我们可以使用以下代码构建模型：

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({ units: 16, activation: 'relu', inputShape: [16] }));
model.add(tf.layers.dense({ units: 1, activation: 'sigmoid' }));
model.compile({ loss: 'binaryCrossentropy', optimizer: 'adam' });
```

此代码将创建一个新的“顺序”模型，然后向该模型添加一个隐藏层和一个输出层。隐藏层有 16 个单元，输出层有 1 个单元。该模型将使用“binaryCrossentropy”损失函数和“adam”优化器进行编译。

## 训练模型

现在我们已经建立了模型，我们可以在我们的数据集上训练它。我们将训练它 10 个时期，这意味着模型将看到训练数据 10 次。

我们可以使用以下代码训练模型：

```javascript
model.fit(trainX, trainY, { epochs: 10 })
  .then(() => {
    // evaluate the model on the test set
  });
```

此代码将在训练集上训练模型，然后在测试集上对其进行评估。

## 评估模型

一旦模型被训练好，我们就可以评估它在测试集上的表现。我们将使用 `model.evaluate()` 方法来执行此操作。

我们可以使用以下代码评估模型：

```javascript
model.evaluate(testX, testY)
  .then(results => {
    // log the results
  });
```

此代码将评估测试集上的模型并打印结果。

## 做出预测

现在我们有了一个经过训练的模型，我们可以用它来对新数据进行预测。为此，我们将使用 `model.predict()` 方法。

我们可以使用以下代码进行预测：

```javascript
const prediction = model.predict(tf.tensor2d([[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16]]));
prediction.print();
```

此代码将对数据“[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16]” 进行预测。 `print()` 方法会将预测打印到控制台。

## 结论

在本文中，我们介绍了如何使用 TensorFlow.js 和 Node.js 进行情绪分析。我们介绍了如何加载和预处理数据集、构建模型、训练模型以及使用模型进行预测。