---
title: 091：使用 TensorFlow.js 和 Node.js 构建生成模型
description: 
published: true
date: 2023-02-03T04:17:28.559Z
tags: 
editor: markdown
dateCreated: 2023-02-03T04:17:26.932Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [091: Building Generative Models with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/091-building-generative-models-with-tensorflow-js-and-node-js)
{.links-list}


# 091：使用 TensorFlow.js 和 Node.js 构建生成模型

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 构建生成模型。生成模型是学习如何生成新数据的强大工具，而 TensorFlow.js 是开始使用 JavaScript 进行深度学习的绝佳方式。

## 什么是生成模型？

生成模型是一种机器学习模型，可以学习生成新数据。例如，生成模型可以学习生成新的人脸图像或新的文本片段。

有许多不同类型的生成模型，但最流行的类型之一是生成对抗网络 (GAN)。 GAN 是一种神经网络，由两部分组成：生成器和鉴别器。

生成器被训练来生成新数据，而鉴别器被训练来区分真实数据和生成数据。这两个网络相互竞争，随着它们的训练，生成器越来越擅长愚弄鉴别器。

## 使用 TensorFlow.js 构建生成模型

现在我们已经了解了什么是生成模型，让我们来看看如何使用 TensorFlow.js 构建生成模型。

使用 TensorFlow.js 构建生成模型有两种方法：您可以使用高层 API，也可以使用底层 API。

如果您刚刚开始使用 TensorFlow.js，我们建议您使用高级层 API。 layers API 使得只需几行代码就可以轻松构建模型，并且可以轻松地与现有的 TensorFlow.js 代码一起使用。

要使用图层 API，我们首先需要安装 TensorFlow.js。我们可以使用 npm 来做到这一点：

```
npm install @tensorflow/tfjs
```

安装 TensorFlow.js 后，我们可以将其导入到我们的 Node.js 程序中：

```javascript
const tf = require('@tensorflow/tfjs');
```

现在我们已经安装了 TensorFlow.js，让我们来看看如何使用它来构建生成模型。

我们将从构建一个简单的生成器网络开始。生成器网络将接收一个噪声向量，并根据该噪声生成图像。

首先，我们需要创建一个接收噪声向量并返回生成器网络的函数。我们将使用层 API 来构建我们的生成器网络：

```javascript
function createGenerator(noise_size) {
  const generator = tf.sequential();

  // First, we'll build a fully connected layer that takes in our noise vector
  // and generates an image from that noise.
  generator.add(tf.layers.dense({
    inputShape: [noise_size],
    units: 7 * 7 * 256,
    useBias: false,
    kernelInitializer: tf.initializers.truncatedNormal({ stddev: 0.02 })
  }));

  // Next, we'll add a batch normalization layer.
  generator.add(tf.layers.batchNormalization({
    epsilon: 1e-5,
    momentum: 0.9
  }));

  // Then, we'll add a Leaky ReLU activation layer.
  generator.add(tf.layers.leakyReLU(0.2));

  // Next, we'll reshape our vector into a 7x7x256 image.
  generator.add(tf.layers.reshape({
    targetShape: [7, 7, 256]
  }));

  // We'll then add a series of convolutional layers.
  generator.add(tf.layers.conv2dTranspose({
    kernelSize: [3, 3],
    filters: 256,
    strides: [2, 2],
    padding: 'same',
    kernelInitializer: tf.initializers.truncatedNormal({ stddev: 0.02 })
  }));

  generator.add(tf.layers.batchNormalization({
    epsilon: 1e-5,
    momentum: 0.9
  }));

  generator.add(tf.layers.leakyReLU(0.2));

  generator.add(tf.layers.conv2dTranspose({
    kernelSize: [3, 3],
    filters: 128,
    strides: [2, 2],
    padding: 'same',
    kernelInitializer: tf.initializers.truncatedNormal({ stddev: 0.02 })
  }));

  generator.add(tf.layers.batchNormalization({
    epsilon: 1e-5,
    momentum: 0.9
  }));

  generator.add(tf.layers.leakyReLU(0.2));

  // Finally, we'll add a convolutional layer that outputs a 28x28x1 image.
  generator.add(tf.layers.conv2dTranspose({
    kernelSize: [3, 3],
    filters: 1,
    strides: [2, 2],
    padding: 'same',
    kernelInitializer: tf.initializers.truncatedNormal({ stddev: 0.02 }),
    activation: 'tanh'
  }));

  // We'll return the generator model.
  return generator;
}
```

现在我们有了生成器网络，让我们来看看如何使用它来生成图像。

首先，我们需要创建一个噪声向量。我们可以通过创建一个具有随机正态分布的张量来做到这一点：

```javascript
const noise = tf.randomNormal([1, 100]);
```

接下来，我们将创建我们的生成器网络：

```javascript
const generator = createGenerator(100);
```

现在我们有了生成器网络，我们可以使用它从噪声向量生成图像：

```javascript
const generated_image = generator.predict(noise);
```

生成的图像将是 28x28x1 张量。我们可以将它转换为 JavaScript 数组并使用 plotly.js 库绘制它：

```javascript
const image_array = generated_image.reshape([28, 28]).arraySync();

const data = [
  {
    z: image_array,
    type: 'heatmap'
  }
];

Plotly.newPlot('generated-image', data);
```

您可以运行上面的代码来生成图像。你应该看到这样的东西：

![生成图像](generated-image.png)

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 构建生成模型。生成模型是学习如何生成新数据的强大工具，而 TensorFlow.js 是开始使用 JavaScript 进行深度学习的绝佳方式。