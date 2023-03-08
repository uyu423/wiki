---
title: 061：使用 TensorFlow.js 和 Node.js 进行实时对象检测
description: 
published: true
date: 2023-02-02T21:17:45.261Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:17:43.576Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [061: Real-Time Object Detection with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/061-real-time-object-detection-with-tensorflow-js-and-node-js)
{.links-list}


# 061：使用 TensorFlow.js 和 Node.js 进行实时对象检测

在本文中，我们将学习如何使用 TensorFlow.js 和 Node.js 执行实时对象检测。

## 什么是 TensorFlow.js？

TensorFlow.js 是一个用于 JavaScript 机器学习的开源库。它允许您在浏览器或 Node.js 环境中训练和运行机器学习模型。

## 什么是 Node.js？

Node.js 是一个 JavaScript 运行时环境，允许您在浏览器之外运行 JavaScript 代码。

## 我们如何使用 TensorFlow.js 和 Node.js 进行实时对象检测？

我们可以使用 TensorFlow.js 和 Node.js 通过以下方式执行实时对象检测：

1. 训练机器学习模型来检测图像中的对象。
2. 将模型部署到 Node.js 服务器。
3. 使用服务器实时处理传入图像和检测对象。

## 1. 训练机器学习模型来检测图像中的对象

我们将从训练机器学习模型开始，以检测图像中的对象。为此，我们将使用 MobileNet 模型。 MobileNet 是一种预训练模型，已在大型图像数据集上进行训练。

我们可以使用 MobileNet 通过以下方式执行对象检测：

1.加载MobileNet模型。
2. 将图像传递给模型。
3. 获取模型的预测。

让我们看看如何在代码中做到这一点：

```javascript
// Load the MobileNet model.
const model = await mobilenet.load();

// Classify the image.
const predictions = await model.classify(image);

// Get the model's predictions.
console.log(predictions);
```

## 2. 将模型部署到 Node.js 服务器

训练完模型后，我们可以将其部署到 Node.js 服务器。这将使我们能够处理传入的图像并实时检测物体。

为此，我们需要：

1. 安装 TensorFlow.js 库。
2. 安装 Node.js 库。
3. 创建一个 Node.js 服务器。
4. 将模型部署到服务器。

让我们看看如何在代码中做到这一点：

```javascript
// Install the TensorFlow.js library.
npm install @tensorflow/tfjs

// Install the Node.js library.
npm install node

// Create a Node.js server.
const tf = require('@tensorflow/tfjs');
const express = require('express');
const app = express();

//Deploy the model to the server.
app.use(express.static(__dirname + '/model'));

// Process incoming images and detect objects in real-time.
app.post('/api/detect', async (req, res) => {
  // Classify the image.
  const predictions = await model.classify(req.body.image);

  // Send the predictions to the client.
  res.json(predictions);
});

// Start the server.
app.listen(3000, () => console.log('Server is running on port 3000'));
```

## 3. 使用服务器实时处理传入的图像和检测对象

一旦我们的服务器启动并运行，我们就可以使用它来处理传入的图像并实时检测对象。

为此，我们需要：

1. 向服务器发送图像。
2. 服务器将处理图像并返回预测。
3. 我们可以使用预测来检测图像中的对象。

让我们看看如何在代码中做到这一点：

```javascript
// Send an image to the server.
const image = 'some-image.jpg';

fetch('/api/detect', {
  method: 'POST',
  body: JSON.stringify({ image }),
})
  .then(res => res.json())
  .then(predictions => {
    // Use the predictions to detect objects in the image.
    console.log(predictions);
  });
```

## 结论

在本文中，我们学习了如何使用 TensorFlow.js 和 Node.js 执行实时对象检测。