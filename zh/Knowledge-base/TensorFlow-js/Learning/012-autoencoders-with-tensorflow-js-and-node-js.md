---
title: 012：使用 TensorFlow.js 和 Node.js 的自动编码器
description: 
published: true
date: 2023-02-02T09:36:40.403Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:36:38.724Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [012: Autoencoders with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/012-autoencoders-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 的自动编码器

深度学习是学习复杂数据表示的强大工具。自动编码器是一种神经网络，可用于以无监督方式学习这些表示。

在本文中，我们将使用 TensorFlow.js 和 Node.js 构建一个简单的自动编码器。我们将使用 MNIST 数据集，它由手写数字的图像组成。

## 入门

首先，我们需要安装依赖项。我们将使用以下库：

* [TensorFlow.js](https://www.tensorflow.org/js)
* [mnist](https://www.npmjs.com/package/mnist)

你可以使用 npm 安装它们：

```
npm install tensorflowjs mnist
```

接下来，我们需要加载 MNIST 数据集。我们将使用 mnist 库来执行此操作：

```javascript
const mnist = require('mnist');

// Load the dataset
const dataset = mnist.set(0.7, 0.3);

// Get the training and test sets
const [train, test] = dataset.getTrainingAndTestSets();
```

MNIST 数据集由手写数字图像组成，每个图像为 28x28 像素。我们需要将这些图像展平为大小为 784 的向量，然后才能将它们用作自动编码器的输入。

```javascript
// Flatten the images into vectors
const trainX = train.map(example => example.input);
const testX = test.map(example => example.input);
```

## 构建自动编码器

现在我们有了数据集，我们可以开始构建自动编码器了。我们将使用具有一个隐藏层的全连接神经网络。隐藏层的单元数将少于输入层，这将迫使网络学习数据的压缩表示。

```javascript
// Create the model
const model = tf.sequential();

// Add the input layer
model.add(tf.layers.dense({
  inputShape: [784],
  units: 64
}));

// Add the hidden layer
model.add(tf.layers.dense({
  units: 32
}));

// Add the output layer
model.add(tf.layers.dense({
  units: 784
}));
```

我们需要为模型指定优化器和损失函数。我们将使用 Adam 优化器和均方误差 (MSE) 损失函数。

```javascript
// Compile the model
model.compile({
  optimizer: 'adam',
  loss: 'meanSquaredError'
});
```

## 训练自动编码器

现在我们有了模型，我们可以在训练集上训练它。我们将训练模型 20 个时期。

```javascript
// Train the model
model.fit(tf.tensor2d(trainX), tf.tensor2d(trainX), {
  epochs: 20
}).then(() => {
  // Evaluate the model on the test set
  model.evaluate(tf.tensor2d(testX), tf.tensor2d(testX));
});
```

## 可视化结果

为了可视化训练结果，我们可以使用“tensorflow-vis”库来绘制重建图像。

```javascript
// Install the library
npm install @tensorflow/tfjs-vis

// Load the library
const tfvis = require('@tensorflow/tfjs-vis');

// Plot the results
tfvis.show.image3d(
  model.predict(tf.tensor2d(testX)),
  {
    width: 28,
    height: 28
  }
);
```

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 构建一个简单的自动编码器。我们还看到了如何训练自动编码器和可视化结果。

自编码器可用于各种任务，例如降维、去噪和生成建模。如果您有兴趣了解有关自动编码器的更多信息，我推荐以下资源：

* [深度学习 101 – 自编码器简介](https://towardsdatascience.com/deep-learning-101-introduction-to-autoencoders-3e44bffe2b7d)
* [自动编码器](http://cs.stanford.edu/people/karpathy/convnetjs/demo/autoencoder.html)
* [变分自编码器](https://jmetzen.github.io/2015-11-27/vae.html)