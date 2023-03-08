---
title: 019：使用 TensorFlow.js 和 Node.js 进行文本分类
description: 
published: true
date: 2023-02-02T11:19:05.673Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:19:04.012Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [019: Text Classification with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/019-text-classification-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 进行文本分类

在本文中，我们将学习如何使用 TensorFlow.js 和 Node.js 构建文本分类模型。文本分类是自然语言处理中的一项常见任务，它是分析和处理人类语言数据的过程。

我们将使用烂番茄网站上的电影评论数据集。该数据集包含每条评论的文本，以及指示评论是正面还是负面的标签。我们将使用此数据集来训练一个模型，该模型可以阅读新评论并预测它们是正面的还是负面的。

## 先决条件

在我们开始之前，您需要做一些事情：

- 在您的计算机上安装 Node.js 和 npm
- 文本编辑器或 IDE
- JavaScript的基础知识

## 入门

首先，我们需要创建一个新的 Node.js 项目。为您的项目创建一个新目录并使用 npm 对其进行初始化：

```
mkdir text-classification
cd text-classification
npm init -y
```

这将为您的项目创建一个 package.json 文件。接下来，我们需要安装我们将要使用的依赖项。我们将使用 TensorFlow.js，一个用于在 JavaScript 中处理机器学习的库，以及 natural 库，它提供了一些处理人类语言数据的有用函数。

```
npm install --save @tensorflow/tfjs natural
```

安装依赖项后，我们现在可以开始编码了。在您的项目目录中创建一个名为 index.js 的新文件并添加以下代码：

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here
```

这将导入 TensorFlow.js 和自然库，我们将在下一节中使用它们。

## 准备数据

在我们训练模型之前，我们需要准备数据。电影评论数据集位于一个名为 reviews.csv 的文件中，您可以[在此处下载](https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv)。

将以下代码添加到 index.js 以加载和准备数据：

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here

// Load the dataset
const csvUrl = 'https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv';
const { data, labels } = tf.data.csv(csvUrl);

// Shuffle the data
const shuffledData = data.shuffle();

// Split the data into training and test sets
const [trainData, testData] = shuffledData.split([0.8, 0.2]);

// Convert the labels to a one-hot encoding
const trainLabels = trainData.map((_, i) => labels[i]).oneHot(2);
const testLabels = testData.map((_, i) => labels[i]).oneHot(2);

// Normalize the data
const trainDataNormalized = trainData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

const testDataNormalized = testData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});
```

让我们看看这段代码做了什么：

- 第一行从 URL 加载数据集。这个数据集是 CSV 格式的，所以我们使用 tf.data.csv() 函数来加载它。
- 第二行打乱数据。这很重要，因为我们不希望模型学习评论的顺序，只学习评论本身。
- 第三行将数据分成训练集和测试集。训练集用于训练模型，测试集用于评估模型。
- 第四行将标签转换为单热编码。这是机器学习中表示分类数据的常用方法。
- 第五行和第六行规范化数据。此步骤很重要，因为它确保模型不会过度拟合训练数据。

## 构建模型

现在我们已经准备好数据，我们可以构建模型了。我们将使用双向长短期记忆 (BiLSTM) 模型，这是一种递归神经网络 (RNN)。

将以下代码添加到 index.js 以构建模型：

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here

// Load the dataset
const csvUrl = 'https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv';
const { data, labels } = tf.data.csv(csvUrl);

// Shuffle the data
const shuffledData = data.shuffle();

// Split the data into training and test sets
const [trainData, testData] = shuffledData.split([0.8, 0.2]);

// Convert the labels to a one-hot encoding
const trainLabels = trainData.map((_, i) => labels[i]).oneHot(2);
const testLabels = testData.map((_, i) => labels[i]).oneHot(2);

// Normalize the data
const trainDataNormalized = trainData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

const testDataNormalized = testData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

// Build the model
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 1000,
  outputDim: 32,
  inputLength: 100
}));
model.add(tf.layers.bidirectional({
  layer: tf.layers.lstm({
    units: 32
  })
}));
model.add(tf.layers.dense({
  units: 2,
  activation: 'softmax'
}));
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

// Train the model
model.fit(trainDataNormalized, trainLabels, {
  epochs: 5,
  validationData: [testDataNormalized, testLabels]
}).then(() => {
  // Evaluate the model
  const results = model.evaluate(testDataNormalized, testLabels);
  console.log(results);
});
```

此代码执行以下操作：

- 第一行使用顺序模型构建模型。这是一种由线性堆叠层组成的模型。
- 第二行添加一个 Embedding 层。该层用于将输入数据转换为矢量表示。
- 第三行添加一个双向层。该层用于处理双向数据。
- 第四行添加了一个长短期记忆（LSTM）层。该层用于长时间记住信息。
- 第五行添加一个 Dense 层。该层用于根据数据进行预测。
- 第六行编译模型。此步骤配置模型以进行训练。
- 第七行训练模型。此步骤需要几分钟才能完成。
- 第八行评估模型。此步骤将模型的准确性打印到控制台。

## 做出预测

现在我们有了一个经过训练的模型，我们可以用它来进行预测。将以下代码添加到 index.js 中进行预测：

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here

// Load the dataset
const csvUrl = 'https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv';
const { data, labels } = tf.data.csv(csvUrl);

// Shuffle the data
const shuffledData = data.shuffle();

// Split the data into training and test sets
const [trainData, testData] = shuffledData.split([0.8, 0.2]);

// Convert the labels to a one-hot encoding
const trainLabels = trainData.map((_, i) => labels[i]).oneHot(2);
const testLabels = testData.map((_, i) => labels[i]).oneHot(2);

// Normalize the data
const trainDataNormalized = trainData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

const testDataNormalized = testData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

// Build the model
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 1000,
  outputDim: 32,
  inputLength: 100
}));
model.add(tf.layers.bidirectional({
  layer: tf.layers.lstm({
    units: 32
  })
}));
model.add(tf.layers.dense({
  units: 2,
  activation: 'softmax'
}));
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

// Train the model
model.fit(trainDataNormalized, trainLabels, {
  epochs: 5,
  validationData: [testDataNormalized, testLabels]
}).then(() => {
  // Evaluate the model
  const results = model.evaluate(testDataNormalized, testLabels);
  console.log(results);
  
  // Make a prediction
  const prediction = model.predict(['this movie was great']);
  console.log(prediction);
});
```

此代码执行以下操作：

- 第一行从 URL 加载数据集。这个数据集是 CSV 格式的，所以我们使用 tf.data.csv() 函数来加载它。
- 第二行打乱数据。这很重要，因为我们不希望模型学习评论的顺序，只学习评论本身。
- 第三行将数据分成训练集和测试集。训练集用于训练模型，测试集用于评估模型。
- 第四行将标签转换为单热编码。这是机器学习中表示分类数据的常用方法。
- 第五行和第六行规范化数据。此步骤很重要，因为它确保模型不会过度拟合训练数据。
- 第七行使用顺序模型构建模型。这是一种由线性堆叠层组成的模型。
- 第八行添加一个Embedding层。该层用于将输入数据转换为矢量表示。
- 第九行添加一个双向层。该层用于处理双向数据。
- 第十行添加了一个长短期记忆（LSTM）层。该层用于长时间记住信息。
- 第十一行添加了一个 Dense 层。该层用于根据数据进行预测。
- 第十二行编译模型。此步骤配置模型以进行训练。
- 第十三行训练模型。此步骤需要几分钟才能完成。
- 第十四行评估模型。此步骤将模型的准确性打印到控制台。
- 第十五行做出预测。此步骤将预测打印到控制台。

## 结论

在本文中，我们学习了如何使用 TensorFlow.js 和 Node.js 构建文本分类模型。我们从加载和准备数据开始，然后我们构建并训练了一个模型。最后，我们使用模型进行预测。

文本分类是自然语言处理中的一项常见任务，本文展示了如何使用 TensorFlow.js 和 Node.js 构建文本分类模型。