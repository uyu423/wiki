---
title: 032：使用 Node.js 部署 TensorFlow.js 模型
description: 
published: true
date: 2023-02-02T14:36:46.581Z
tags: 
editor: markdown
dateCreated: 2023-02-02T14:36:44.820Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [032: Deploying TensorFlow.js Models with Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/032-deploying-tensorflow-js-models-with-node-js)
{.links-list}


# 032：使用 Node.js 部署 TensorFlow.js 模型

TensorFlow.js 是一个用于机器学习的开源 JavaScript 库，它使开发人员能够在浏览器或 Node.js 中训练和部署 ML 模型。

在本文中，我们将学习如何使用 TensorFlow.js 在 Node.js 应用程序中部署预训练的 ML 模型。我们还将学习如何使用 Node.js API 在模型上运行推理。

## 先决条件

在开始之前，您需要具备以下条件：

* 节点.js
* 文本编辑器
* 网络浏览器

## 入门

首先，我们需要安装 TensorFlow.js 库。我们可以使用节点包管理器 (NPM) 执行此操作：

```
npm install @tensorflow/tfjs
```

接下来，我们需要下载预训练的 ML 模型。对于此示例，我们将使用 [MobileNet](https://github.com/tensorflow/tfjs-models/tree/master/mobilenet) 图像分类模型。

下载模型后，我们可以将其部署到我们的 Node.js 应用程序中。

## 部署模型

要部署模型，我们需要创建一个名为“index.js”的新文件。在此文件中，我们将使用“tf.loadModel()”函数加载预训练模型：

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
  });
```

## 使用模型

加载模型后，我们可以使用它对图像进行推理。对于此示例，我们将使用 [TensorFlow.js 图像分类示例](https://github.com/tensorflow/tfjs-examples/tree/master/image-classification)。

首先，我们需要将图像加载到 `tf.Tensor` 中：

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
    const img = tf.tensor3d(imageData, [224, 224, 3]);
  });
```

接下来，我们需要使用 `mobilenet.preprocessInput()` 函数对图像进行预处理：

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
    const img = tf.tensor3d(imageData, [224, 224, 3]);

    // Pre-process the image.
    const preprocessedImg = tf.mobilenet.preprocessInput(img);
  });
```

最后，我们可以使用 model.predict() 函数对图像进行推理：

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
    const img = tf.tensor3d(imageData, [224, 224, 3]);

    // Pre-process the image.
    const preprocessedImg = tf.mobilenet.preprocessInput(img);

    // Run inference.
    model.predict(preprocessedImg).then(predictions => {
      // Use the predictions.
    });
  });
```

`predictions` 变量包含推理的结果。

## 结论

在本文中，我们学习了如何使用 TensorFlow.js 在 Node.js 应用程序中部署预训练的 ML 模型。我们还学习了如何使用 Node.js API 在模型上运行推理。