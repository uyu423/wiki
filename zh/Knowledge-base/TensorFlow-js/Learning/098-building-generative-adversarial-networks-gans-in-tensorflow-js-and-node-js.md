---
title: 098：在 TensorFlow.js 和 Node.js 中构建生成对抗网络 (GAN)
description: 
published: true
date: 2023-02-03T06:04:52.624Z
tags: 
editor: markdown
dateCreated: 2023-02-03T06:04:51.001Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [098: Building Generative Adversarial Networks (GANs) in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/098-building-generative-adversarial-networks-gans-in-tensorflow-js-and-node-js)
{.links-list}


# 098：在 TensorFlow.js 和 Node.js 中构建生成对抗网络 (GAN)

希望使用 TensorFlow.js 和 Node.js 构建生成模型的开发人员可以使用生成对抗网络 (GAN) 来实现。在本文中，我们将指导您完成在 TensorFlow.js 和 Node.js 中构建 GAN 的过程。

## 什么是 GAN？

GAN 是一种神经网络，用于从头开始生成新数据。该网络由两部分组成：生成器和鉴别器。生成器负责生成新的数据，鉴别器负责判断数据的真假。

## 在 TensorFlow.js 中构建 GAN

构建 GAN 的第一步是创建一个名为“gan.js”的新文件。我们将从要求 `tensorflow` 和 `tfjs-node` 模块开始：

```javascript
const tf = require('tensorflow');
const tfNode = require('tfjs-node');
```

接下来，我们将定义生成器和鉴别器模型：

```javascript
// Generator
const generator = tf.sequential();
generator.add(tf.layers.dense({units: 100, inputShape: [100]}));
generator.add(tf.layers.batchNormalization());
generator.add(tf.layers.leakyReLU());
generator.add(tf.layers.dense({units: 784, activation: 'tanh'}));

// Discriminator
const discriminator = tf.sequential();
discriminator.add(tf.layers.dense({units: 784, inputShape: [784]}));
discriminator.add(tf.layers.leakyReLU());
discriminator.add(tf.layers.dense({units: 1, activation: 'sigmoid'}));
```

在上面的代码中，我们定义了一个生成器，它接收 100 维噪声向量并输出 784 维向量（即 28x28 图像）。我们还定义了一个鉴别器，它接受 784 维向量并输出一个值来指示向量是真实的还是假的。

接下来，我们需要编译模型：

```javascript
// Generator
generator.compile({
  optimizer: tf.train.adam(0.0001),
  loss: 'binaryCrossentropy'
});

// Discriminator
discriminator.compile({
  optimizer: tf.train.adam(0.0001),
  loss: 'binaryCrossentropy'
});
```

在上面的代码中，我们指定应使用学习率为 0.0001 的 Adam 优化器优化模型。我们还指定了两个模型的损失函数应该是二元交叉熵。

## 训练 GAN

现在我们已经定义并编译了模型，我们可以开始训练 GAN。训练过程包括两个步骤：训练判别器和训练生成器。

### 训练判别器

训练 GAN 的第一步是训练判别器。为此，我们将使用生成器生成一批假数据，并使用训练数据集生成一批真实数据。然后我们将在这两批数据上训练鉴别器。

```javascript
// Train the discriminator
for (let i = 0; i < 1000; i++) {
  // Generate a batch of fake data
  const noise = tf.randomNormal([batchSize, 100]);
  const fakeData = generator.predict(noise);

  // Generate a batch of real data
  const realData = tf.data.nextBatch(batchSize, [784]);

  // Train the discriminator
  const xs = tf.concat([fakeData, realData], 0);
  const ys = tf.concat([tf.zeros([batchSize, 1]), tf.ones([batchSize, 1])], 0);
  discriminator.fit(xs, ys);
}
```

在上面的代码中，我们使用生成器生成了一批假数据，并使用训练数据集生成了一批真实数据。然后我们将这两批数据连接起来，并根据它们训练鉴别器。

### 训练生成器

现在判别器已经训练好了，我们可以训练生成器了。我们将通过生成一批噪声向量并将它们传递给生成器来完成此操作。然后我们将在这些噪声向量上训练生成器。

```javascript
// Train the generator
for (let i = 0; i < 1000; i++) {
  // Generate a batch of noise vectors
  const noise = tf.randomNormal([batchSize, 100]);

  // Train the generator
  const ys = tf.ones([batchSize, 1]);
  generator.fit(noise, ys);
}
```

在上面的代码中，我们生成了一批噪声向量并将它们传递给生成器。然后我们在这些噪声向量上训练了生成器。

## 生成新数据

现在 GAN 已经训练完毕，我们可以用它来生成新数据。为此，我们将生成一批噪声向量并将它们传递给生成器。

```javascript
// Generate a batch of noise vectors
const noise = tf.randomNormal([batchSize, 100]);

// Generate new data
const generatedData = generator.predict(noise);
```

在上面的代码中，我们生成了一批噪声向量并将它们传递给生成器。这产生了一批可用于任何目的的新数据。