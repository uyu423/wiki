---
title: 092：在 TensorFlow.js 和 Node.js 中使用变分自动编码器 (VAE)
description: 
published: true
date: 2023-02-03T04:36:31.914Z
tags: 
editor: markdown
dateCreated: 2023-02-03T04:36:27.083Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [092: Using Variational Autoencoders (VAEs) in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/092-using-variational-autoencoders-vaes-in-tensorflow-js-and-node-js)
{.links-list}


# 在 TensorFlow.js 和 Node.js 中使用变分自动编码器 (VAE)

变分自动编码器 (VAE) 是学习数据潜在表示的强大工具。在本文中，我们将了解如何使用 VAE 在 TensorFlow.js 和 Node.js 中学习 MNIST 数据的潜在表示。

## 什么是 VAE？

VAE 是一种概率模型，可用于学习数据的潜在表示。 VAE 类似于自动编码器，因为它们学习将数据压缩到潜在空间中。然而，VAE 是概率模型，这意味着它们可用于从潜在空间生成新的数据样本。

## VAE 是如何工作的？

VAE 通过学习数据的潜在表示来工作。潜在空间是一个低维空间，可以捕获数据的基本特征。然后 VAE 使用这个潜在空间来生成新的数据样本。

## 如何在 TensorFlow.js 中使用 VAE？

要在 TensorFlow.js 中使用 VAE，您需要先安装 TensorFlow.js 库。您可以使用 Node.js 包管理器执行此操作：

```
npm install @tensorflow/tfjs
```

接下来，您需要加载 MNIST 数据。您可以使用 tf.data.Dataset API 执行此操作：

```javascript
const mnistData = tf.data.dataset.mnist({
  train: true,
  testData: false
});
```

现在，您需要创建 VAE。您可以使用 tf.layers.vae() 函数执行此操作：

```javascript
const vae = tf.layers.vae({
  encoder: {
    inputShape: [28, 28, 1],
    latentDimensions: 2
  },
  decoder: {
    outputShape: [28, 28, 1]
  }
});
```

最后，您需要训练 VAE。您可以使用 fit() 方法执行此操作：

```javascript
vae.fit(mnistData, {
  epochs: 10
});
```

## 如何在 Node.js 中使用 VAE？

要在 Node.js 中使用 VAE，您需要先安装 TensorFlow.js 库。您可以使用 Node.js 包管理器执行此操作：

```
npm install @tensorflow/tfjs
```

接下来，您需要加载 MNIST 数据。您可以使用 tf.data.Dataset API 执行此操作：

```javascript
const mnistData = tf.data.dataset.mnist({
  train: true,
  testData: false
});
```

现在，您需要创建 VAE。您可以使用 tf.layers.vae() 函数执行此操作：

```javascript
const vae = tf.layers.vae({
  encoder: {
    inputShape: [28, 28, 1],
    latentDimensions: 2
  },
  decoder: {
    outputShape: [28, 28, 1]
  }
});
```

最后，您需要训练 VAE。您可以使用 fit() 方法执行此操作：

```javascript
vae.fit(mnistData, {
  epochs: 10
});
```

## 结论

在本文中，我们了解了如何使用 VAE 在 TensorFlow.js 和 Node.js 中学习 MNIST 数据的潜在表示。 VAE 是学习数据潜在表示的强大工具。