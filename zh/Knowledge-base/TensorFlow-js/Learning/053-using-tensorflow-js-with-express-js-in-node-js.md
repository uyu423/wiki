---
title: 053：在 Node.js 中使用 TensorFlow.js 和 Express.js
description: 
published: true
date: 2023-02-02T19:17:22.773Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:17:21.181Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [053: Using TensorFlow.js with Express.js in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/053-using-tensorflow-js-with-express-js-in-node-js)
{.links-list}


# 在 Node.js 中使用 TensorFlow.js 和 Express.js

TensorFlow.js 是一个强大的 JavaScript 机器学习工具。它可以在 Node.js 中与 Express.js Web 框架一起使用，以创建功能强大的应用程序。在本文中，我们将向您展示如何开始使用 TensorFlow.js 和 Express.js。

## 安装依赖

首先，我们需要为我们的项目安装依赖项。我们需要 Express.js 和 TensorFlow.js。我们可以使用以下命令安装它们：

```
npm install express @tensorflow/tfjs
```

## 你好世界

现在我们已经安装了依赖项，让我们创建一个简单的“Hello world”应用程序。我们将在项目的根目录中创建一个名为 index.js 的文件并添加以下代码：

```javascript
const express = require('express');
const tf = require('@tensorflow/tfjs');

const app = express();

app.get('/', (req, res) => {
  res.send('Hello, world!');
});

app.listen(3000, () => {
  console.log('Example app listening on port 3000!');
});
```

此代码创建一个 Express.js 服务器，该服务器侦听端口 3000 并响应“Hello, world!”当访问根 URL 时。

## 使用 TensorFlow.js

现在我们已经启动并运行了简单的 Express.js 服务器，让我们添加一些 TensorFlow.js 代码。我们将首先添加一个路由，该路由响应由 TensorFlow.js 模型生成的字符串。

首先，我们需要创建模型。我们将在名为 model.js 的文件中执行此操作。我们将创建一个简单的模型，它接受一个输入字符串并生成一个输出字符串。输入字符串将作为 one-hot 编码向量输入模型。输出字符串将由模型使用序列到序列架构生成。

```javascript
const tf = require('@tensorflow/tfjs');

// Create the model
const model = tf.sequential();

// Add an LSTM layer
model.add(tf.layers.lstm({
  units: 8,
  inputShape: [8],
  returnSequences: true
}));

// Add a second LSTM layer
model.add(tf.layers.lstm({
  units: 8,
  returnSequences: true
}));

// Add a dense layer
model.add(tf.layers.dense({
  units: 8,
  activation: 'softmax'
}));

// Compile the model
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'rmsprop'
});

// Export the model
module.exports = model;
```

此代码创建一个简单的基于 LSTM 的模型。该模型接受一个 8 个字符的输入字符串并输出一个 8 个字符的字符串。

现在我们有了我们的模型，我们可以添加一个使用它的路由。我们会将以下路由添加到我们的 index.js 文件中：

```javascript
app.get('/generate', (req, res) => {
  // Load the model
  const model = require('./model');

  // Generate a string
  const string = model.predict(tf.oneHot('Hello, world!'.split(''), 8));

  // Send the string to the client
  res.send(string);
});
```

此路由加载我们在 model.js 中创建的模型，并使用它生成字符串。然后将生成的字符串发送到客户端。

## 结论

在本文中，我们向您展示了如何开始使用 TensorFlow.js 和 Express.js。我们创建了一个简单的“Hello world”应用程序和一个使用 TensorFlow.js 模型生成字符串的路由。

## 资源

- [TensorFlow.js](https://js.tensorflow.org/)
- [Express.js](https://expressjs.com/)
- [Node.js](https://nodejs.org/)