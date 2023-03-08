---
title: 071：使用 TensorFlow.js 和 Node.js 进行 GPU 加速
description: 
published: true
date: 2023-02-02T20:24:33.684Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:24:31.991Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [071: GPU Acceleration with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/071-gpu-acceleration-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 进行 GPU 加速

TensorFlow.js 是一个强大而灵活的 JavaScript 库，用于训练和部署机器学习模型。 Node.js 是一个 JavaScript 运行时，支持服务器端脚本和快速网络应用程序。

借助 TensorFlow.js 和 Node.js，您可以在 Web 和 Node.js 服务器上训练和部署机器学习模型。 TensorFlow.js 提供了一个 JavaScript API，用于在 Web 浏览器和 Node.js 服务器上训练和部署机器学习模型。 Node.js 使您能够在服务器上运行 JavaScript。

在本文中，我们将向您展示如何使用 TensorFlow.js 和 Node.js 在 Web 和 Node.js 服务器上训练和部署机器学习模型。

## 先决条件

要跟进这篇文章，您需要：

- 一台带有网络浏览器和互联网连接的电脑
- 文本编辑器
- Node.js 安装在你的电脑上

## 安装 TensorFlow.js

要安装 TensorFlow.js，您可以使用 Node.js 包管理器 (npm)：

```
npm install @tensorflow/tfjs
```

## 你好，TensorFlow.js

让我们从使用 TensorFlow.js 训练和部署一个简单的机器学习模型开始。我们将使用 MNIST 数据集，它由手写数字的图像组成。

首先，我们需要加载 MNIST 数据集。我们可以使用 TensorFlow.js MNIST 数据集类来做到这一点：

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = new tf.MNISTDataset();
```

接下来，我们需要在 MNIST 数据集上训练机器学习模型。我们将使用称为卷积神经网络 (CNN) 的深度学习模型。 CNN 是一种旨在处理图像的神经网络。

我们可以使用 TensorFlow.js 层 API 训练 CNN：

```javascript
const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});
```

现在我们有了一个机器学习模型，我们可以在 MNIST 数据集上训练它。我们将使用 TensorFlow.js fit API 来训练模型：

```javascript
const trainXs = mnistData.getTrainImagesAsTensors();
const trainYs = mnistData.getTrainLabelsAsTensors();

model.fit(trainXs, trainYs, {
  epochs: 10,
  batchSize: 64
});
```

模型训练完成后，我们可以在 MNIST 测试数据集上对其进行评估。我们将使用 TensorFlow.js 评估 API 来评估模型：

```javascript
const testXs = mnistData.getTestImagesAsTensors();
const testYs = mnistData.getTestLabelsAsTensors();

model.evaluate(testXs, testYs);
```

评估 API 将返回模型在测试数据集上的损失和准确性。

## 部署 TensorFlow.js 模型

一旦训练了机器学习模型，您就可以将其部署到 Web 服务器或 Node.js 服务器。

我们将从将模型部署到 Web 服务器开始。我们可以使用 TensorFlow.js 模型转换器 API 来做到这一点：

```javascript
const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

const converter = tf.modelConverter.createConverter({
  from: 'tensorflowjs_layers_model'
});

const json = converter.toJSON(model);
```

模型转换器 API 将返回模型的 JSON 表示。此 JSON 表示可用于将模型部署到 Web 服务器。

要将模型部署到 Web 服务器，您需要创建一个 HTML 文件和一个 JavaScript 文件。 HTML 文件将包含一个元素，TensorFlow.js 模型将加载到该元素中。 JavaScript 文件将包含将模型加载到元素中的代码。

这是一个示例 HTML 文件：

```html
<html>
  <head>
    <title>TensorFlow.js MNIST Example</title>
  </head>
  <body>
    <h1>TensorFlow.js MNIST Example</h1>
    <div id="container"></div>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs"></script>
    <script src="mnist.js"></script>
  </body>
</html>
```

这是一个示例 JavaScript 文件：

```javascript
const tf = require('@tensorflow/tfjs');

const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

const mnistData = new tf.MNISTDataset();

const testXs = mnistData.getTestImagesAsTensors();
const testYs = mnistData.getTestLabelsAsTensors();

model.evaluate(testXs, testYs);

const converter = tf.modelConverter.createConverter({
  from: 'tensorflowjs_layers_model'
});

const json = converter.toJSON(model);

tf.loadLayersModel('http://localhost:8080/model.json').then(function(model) {
  model.predict(testXs).then(function(predictions) {
    console.log(predictions);
  });
});
```

在 HTML 文件中，我们包含了 TensorFlow.js 脚本和 mnist.js 脚本。 mnist.js 脚本包含将模型加载到 ID 为“container”的元素中的代码。

要运行 HTML 文件，您需要启动 Web 服务器。您可以使用 Node.js http-server 模块来启动 Web 服务器：

```
npm install http-server -g

http-server
```

http-server 模块将在端口 8080 上启动一个 Web 服务器。您可以在 http://localhost:8080 访问 HTML 文件。

## 在 Node.js 服务器上运行 TensorFlow.js 模型

您还可以在 Node.js 服务器上运行 TensorFlow.js 模型。为此，您需要使用 TensorFlow.js Node.js API：

```javascript
const tf = require('@tensorflow/tfjs');

const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

const mnistData = new tf.MNISTDataset();

const testXs = mnistData.getTestImagesAsTensors();
const testYs = mnistData.getTestLabelsAsTensors();

model.evaluate(testXs, testYs);

const converter = tf.modelConverter.createConverter({
  from: 'tensorflowjs_layers_model'
});

const json = converter.toJSON(model);

tf.loadLayersModel('http://localhost:8080/model.json').then(function(model) {
  model.predict(testXs).then(function(predictions) {
    console.log(predictions);
  });
});
```

在上面的代码中，我们加载了 MNIST 数据集并在其上训练了一个机器学习模型。然后我们将模型转换为 JSON 表示并将其加载到 Node.js 服务器中。

要运行上面的代码，您需要启动一个 Node.js 服务器。您可以使用 Node.js Express 模块启动 Node.js 服务器：

```
npm install express -g

express
```

Express 模块将在端口 3000 上启动一个 Node.js 服务器。您可以通过 http://localhost:3000 访问该服务器。

## 结论

在本文中，我们向您展示了如何使用 TensorFlow.js 和 Node.js 在 Web 和 Node.js 服务器上训练和部署机器学习模型。

TensorFlow.js 是一个强大而灵活的 JavaScript 库，用于训练和部署机器学习模型。 Node.js 是一个 JavaScript 运行时，支持服务器端脚本和快速网络应用程序。

借助 TensorFlow.js 和 Node.js，您可以在 Web 和 Node.js 服务器上训练和部署机器学习模型。 TensorFlow.js 提供了一个 JavaScript API，用于在 Web 浏览器和 Node.js 服务器上训练和部署机器学习模型。 Node.js 使您能够在服务器上运行 JavaScript。