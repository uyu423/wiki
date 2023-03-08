---
title: 013：使用 TensorFlow.js 和 Node.js 的生成对抗网络 (GAN)
description: 
published: true
date: 2023-02-02T09:44:15.298Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:44:13.589Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [013: Generative Adversarial Networks (GAN) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/013-generative-adversarial-networks-gan-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 的生成对抗网络 (GAN)

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 创建生成对抗网络 (GAN)。我们将使用 GAN 基于 MNIST 数据集生成手写数字的新图像。

## 什么是 GAN？

GAN 是一种用于生成建模的神经网络。生成建模是机器学习中的一项任务，其目标是生成与训练数据相似的新数据。

GAN 由两个神经网络、一个生成器和一个鉴别器组成。生成器网络将噪声作为输入并生成与训练数据相似的图像。鉴别器网络将图像作为输入并尝试将它们分类为真实的或虚假的。

生成器和鉴别器网络在零和博弈中一起训练，生成器的目标是欺骗鉴别器认为生成的图像是真实的，而鉴别器的目标是正确地将图像分类为真实的或假的。

## 设置项目

在我们开始训练我们的 GAN 之前，我们需要设置我们的项目。我们将使用以下库：

- [TensorFlow.js](https://js.tensorflow.org/)
- [节点获取](https://www.npmjs.com/package/node-fetch)
- [@tensorflow/tfjs-node](https://www.npmjs.com/package/@tensorflow/tfjs-node)

您可以使用 npm 安装这些库：

```
npm install tensorflowjs node-fetch @tensorflow/tfjs-node
```

## 加载 MNIST 数据集

我们将为 GAN 使用 MNIST 数据集。 MNIST 数据集是手写数字的集合，每个数字都表示为 28x28 的灰度图像。

我们可以使用 node-fetch 库从 TensorFlow.js 数据集存储库加载 MNIST 数据集：

```javascript
const tf = require('@tensorflow/tfjs-node');
const fetch = require('node-fetch');

// Load the MNIST dataset from the TensorFlow.js Datasets repository.
const mnistDataset = await tf.data.web('https://storage.googleapis.com/tfjs-datasets/mnist.json');
```

## 预处理 MNIST 数据集

一旦我们加载了 MNIST 数据集，我们需要对其进行预处理，以便它可以用于训练我们的 GAN。

首先，我们将 28x28 灰度图像转换为 32x32 RGB 图像。我们还将规范化像素值在 [-1, 1] 范围内。

```javascript
// Convert the 28x28 grayscale images into 32x32 RGB images.
const mnistImages = mnistDataset.images.map(image => tf.image.resizeBilinear(image, [32, 32]));

// Normalize the pixel values to be in the range [-1, 1].
const mnistImages = mnistImages.map(image => image.toFloat().div(tf.scalar(255)).sub(tf.scalar(1)));
```

## 创建生成器网络

现在我们已经预处理了 MNIST 数据集，我们可以开始创建我们的 GAN。

首先，我们将创建生成器网络。生成器网络将噪声向量作为输入并生成与训练数据相似的图像。

我们将使用 100 维的噪声向量。我们将使用 tf.layers.dense 层将噪声向量映射到 32x32x3 尺寸的图像。

```javascript
// Create the generator network.
const generator = tf.sequential();

// Map the noise vector to an image with 32x32x3 dimensions.
generator.add(tf.layers.dense({inputShape: [100], units: 32 * 32 * 3}));
generator.add(tf.layers.reshape({targetShape: [32, 32, 3]}));
```

## 创建鉴别器网络

接下来，我们将创建鉴别器网络。鉴别器网络将图像作为输入并尝试将其分类为真实的或虚假的。

我们将使用 tf.layers.conv2d 层为鉴别器创建一个卷积神经网络。我们还将使用 tf.layers.leakyReLU 层为网络添加非线性。

```javascript
// Create the discriminator network.
const discriminator = tf.sequential();

// Add a convolutional layer.
discriminator.add(tf.layers.conv2d({inputShape: [32, 32, 3], filters: 16, kernelSize: 3, strides: 2, padding: 'same'}));

// Add a Leaky ReLU layer.
discriminator.add(tf.layers.leakyReLU());

// Add another convolutional layer.
discriminator.add(tf.layers.conv2d({filters: 32, kernelSize: 3, strides: 2, padding: 'same'}));

// Add another Leaky ReLU layer.
discriminator.add(tf.layers.leakyReLU());

// Add a flatten layer.
discriminator.add(tf.layers.flatten());

// Add a fully connected layer.
discriminator.add(tf.layers.dense({units: 1}));

// Add a sigmoid activation layer.
discriminator.add(tf.layers.activation({activation: 'sigmoid'}));
```

## 训练 GAN

现在我们已经创建了生成器和鉴别器网络，我们可以训练我们的 GAN。

首先，我们将创建一个结合生成器和鉴别器网络的 GAN 模型。

接下来，我们将使用 tf.train.adamOptimizer 优化器编译 GAN 模型。

最后，我们将使用 tf.train.ganTrain() 方法训练 GAN 模型。

```javascript
// Create a GAN model that combines the generator and discriminator.
const gan = tf.sequential();

// Add the generator to the GAN.
gan.add(generator);

// Freeze the generator.
generator.trainable = false;

// Add the discriminator to the GAN.
gan.add(discriminator);

// Compile the GAN using the Adam optimizer.
gan.compile({loss: 'binaryCrossentropy', optimizer: tf.train.adamOptimizer()});

// Train the GAN.
for (let i = 0; i < 100; i++) {
  // Get a batch of real images.
  const realImages = mnistImages.slice(i * 10, (i + 1) * 10);

  // Generate a batch of fake images.
  const noise = tf.randomNormal([10, 100]);
  const fakeImages = generator.predict(noise);

  // Create a batch of labels for the real and fake images.
  const realLabels = tf.ones([10, 1]);
  const fakeLabels = tf.zeros([10, 1]);

  // Train the discriminator on the real and fake images.
  const loss = await gan.fit([realImages, fakeImages], [realLabels, fakeLabels], {
    epochs: 1,
    batchSize: 10
  });

  // Generate and show a batch of fake images.
  const noise = tf.randomNormal([10, 100]);
  const fakeImages = generator.predict(noise);
  fakeImages.forEach((image, i) => {
    const canvas = document.createElement('canvas');
    canvas.width = 28;
    canvas.height = 28;
    const ctx = canvas.getContext('2d');
    const imageData = new ImageData(28, 28);
    const data = image.dataSync();
    for (let j = 0; j < 28 * 28; j++) {
      const k = j * 4;
      const imgIdx = j;
      imageData.data[k + 0] = (data[imgIdx + 0] + 1) * 127;
      imageData.data[k + 1] = (data[imgIdx + 1] + 1) * 127;
      imageData.data[k + 2] = (data[imgIdx + 2] + 1) * 127;
      imageData.data[k + 3] = 255;
    }
    ctx.putImageData(imageData, 0, 0);
    document.body.appendChild(canvas);
  });
}
```

## 生成新图像

一旦 GAN 被训练好，我们就可以用它来生成新的图像。

首先，我们将生成一个 100 维的噪声向量。

接下来，我们将使用生成器网络从噪声向量生成图像。

最后，我们将在屏幕上显示生成的图像。

```javascript
// Generate a noise vector with 100 dimensions.
const noise = tf.randomNormal([1, 100]);

// Use the generator to generate an image from the noise vector.
const generatedImage = generator.predict(noise);

// Show the generated image.
const canvas = document.createElement('canvas');
canvas.width = 28;
canvas.height = 28;
const ctx = canvas.getContext('2d');
const imageData = new ImageData(28, 28);
const data = generatedImage.dataSync();
for (let i = 0; i < 28 * 28; i++) {
  const j = i * 4;
  const imgIdx = i;
  imageData.data[j + 0] = (data[imgIdx + 0] + 1) * 127;
  imageData.data[j + 1] = (data[imgIdx + 1] + 1) * 127;
  imageData.data[j + 2] = (data[imgIdx + 2] + 1) * 127;
  imageData.data[j + 3] = 255;
}
ctx.putImageData(imageData, 0, 0);
document.body.appendChild(canvas);
```

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 创建 GAN。我们还了解了如何使用 GAN 生成手写数字的新图像。

如果你想了解更多关于 GAN 的知识，我推荐以下资源：

- [生成对抗网络](https://arxiv.org/abs/1406.2661)（研究论文）
- [Deep Learning with JavaScript](https://www.manning.com/livevideo/deep-learning-with-javascript)（视频课程）
- [TensorFlow 中的生成对抗网络](https://www.tensorflow.org/tutorials/generative/gan)（教程）