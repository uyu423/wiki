---
title: 076：在边缘计算中使用 TensorFlow.js 和 Node.js
description: 
published: true
date: 2023-02-03T00:37:57.396Z
tags: 
editor: markdown
dateCreated: 2023-02-03T00:37:55.793Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [076: Using TensorFlow.js with Node.js in Edge Computing***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/076-using-tensorflow-js-with-node-js-in-edge-computing)
{.links-list}


# 在边缘计算中使用 TensorFlow.js 和 Node.js

TensorFlow.js 是一个使用数据流图进行数值计算的开源库。它可以在 Node.js 中用于在边缘设备上训练和部署机器学习模型。

在本文中，我们将介绍如何结合使用 TensorFlow.js 和 Node.js 在边缘设备上训练和部署机器学习模型。

## 什么是 TensorFlow.js？

TensorFlow.js 是一个使用数据流图进行数值计算的开源库。 TensorFlow.js 是一个 JavaScript 库，用于在浏览器和 Node.js 上训练和部署机器学习模型。

TensorFlow.js 最初由 Google Brain 团队开发，用于 TensorFlow 机器学习平台。

## 什么是 Node.js？

Node.js 是一个基于 Chrome 的 V8 JavaScript 引擎构建的 JavaScript 运行时。 Node.js 是用于开发服务器端应用程序的开源跨平台运行时环境。

Node.js 应用程序是用 JavaScript 编写的，可以在 OS X、Microsoft Windows、Linux 和 FreeBSD 上的 Node.js 运行时中运行。

## 入门

为了将 TensorFlow.js 与 Node.js 一起使用，您需要安装以下内容：

- 节点.js
-TensorFlow.js

您可以使用以下命令安装 Node.js 和 TensorFlow.js：

```
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
```

```
npm install @tensorflow/tfjs
```

## 你好世界

让我们首先使用 TensorFlow.js 和 Node.js 创建一个简单的“Hello World”程序。

创建一个名为“hello-world.js”的文件并添加以下代码：

```javascript
const tf = require('@tensorflow/tfjs');

tf.tensor([1, 2, 3, 4]).print();
```

使用以下命令运行程序：

```
node hello-world.js
```

您应该看到以下输出：

```
Tensor
    [[1],
     [2],
     [3],
     [4]]
```

## 训练机器学习模型

现在我们已经了解了如何将 TensorFlow.js 与 Node.js 结合使用，让我们尝试训练一个简单的机器学习模型。

我们将使用 MNIST 数据集，它包含 70,000 张手写数字的灰度图像。图像大小为 28x28 像素。

MNIST 数据集分为三部分：60,000 张用于训练的图像、10,000 张用于测试的图像和 10,000 张用于验证的图像。

我们将使用 TensorFlow.js 层 API 来构建我们的机器学习模型。层 API 是一种高级 API，可以轻松构建神经网络。

首先，我们需要加载 MNIST 数据集。我们可以使用 tf.data API 来做到这一点。

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();
}

run();
```

接下来，我们将使用 tf.sequential API 定义我们的机器学习模型。

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });
}

run();
```

现在我们已经定义了我们的机器学习模型，我们需要训练它。我们可以使用 tf.fit API 来做到这一点。

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  return model.fit(images, labels, {
    batchSize,
    epochs
  });
}

run();
```

一旦我们的机器学习模型经过训练，我们就可以使用它对新数据进行预测。

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  model.fit(images, labels, {
    batchSize,
    epochs
  });

  const testImages = images.slice(0, 1000);
  const testLabels = labels.slice(0, 1000);

  const accuracy = model.evaluate(testImages, testLabels);

  console.log('Accuracy:', accuracy[1]);
}

run();
```

## 部署机器学习模型

一旦我们训练了我们的机器学习模型，我们就可以将它部署到边缘设备进行推理。

我们将使用 TensorFlow.js Node.js API 将我们的机器学习模型部署到边缘设备。 Node.js API 是一种低级 API，允许您在 Node.js 上运行 TensorFlow.js 程序。

首先，我们需要将机器学习模型转换为 TensorFlow.js Node.js 格式。我们可以使用 tf.node.save API 来做到这一点。

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  model.fit(images, labels, {
    batchSize,
    epochs
  });

  tf.node.save(model, 'model.json');
}

run();
```

一旦我们的机器学习模型转换为 TensorFlow.js Node.js 格式，我们就可以将其部署到边缘设备。

我们需要在边缘设备上安装 TensorFlow.js Node.js API。我们可以使用以下命令执行此操作：

```
npm install @tensorflow/tfjs-node
```

现在已经安装了 TensorFlow.js Node.js API，我们可以使用 tf.node.load API 来加载我们的机器学习模型。

```javascript
const tf = require('@tensorflow/tfjs-node');

async function run() {
  const model = await tf.node.load('model.json');
}

run();
```

加载机器学习模型后，我们可以使用它对新数据进行预测。

```javascript
const tf = require('@tensorflow/tfjs-node');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  model.fit(images, labels, {
    batchSize,
    epochs
  });

  tf.node.save(model, 'model.json');

  const testImages = images.slice(0, 1000);
  const testLabels = labels.slice(0, 1000);

  const accuracy = model.evaluate(testImages, testLabels);

  console.log('Accuracy:', accuracy[1]);
}

run();
```

## 结论

在本文中，我们了解了如何结合使用 TensorFlow.js 和 Node.js 在边缘设备上训练和部署机器学习模型。

TensorFlow.js 是一个强大的数值计算库，可用于在边缘设备上训练和部署机器学习模型。

Node.js 是一个 JavaScript 运行时，可用于在边缘设备上运行 TensorFlow.js 程序。

TensorFlow.js Node.js API 是一个低级 API，允许您在 Node.js 上运行 TensorFlow.js 程序。

## 资源

- [TensorFlow.js](https://js.tensorflow.org/)
- [Node.js](https://nodejs.org/en/)
- [ MNIST 数据集](http://yann.lecun.com/exdb/mnist/)