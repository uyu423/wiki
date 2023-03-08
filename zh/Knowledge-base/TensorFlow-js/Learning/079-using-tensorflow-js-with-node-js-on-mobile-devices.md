---
title: 079：在移动设备上使用 TensorFlow.js 和 Node.js
description: 
published: true
date: 2023-02-03T01:17:41.863Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:17:40.285Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [079: Using TensorFlow.js with Node.js on Mobile Devices***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/079-using-tensorflow-js-with-node-js-on-mobile-devices)
{.links-list}


## 介绍

TensorFlow.js 是一个开源库，可用于在浏览器或 Node.js 服务器上开发和训练机器学习模型。在这篇文章中，我们将专注于在移动设备上使用 TensorFlow.js 和 Node.js。

与传统的服务器端机器学习框架相比，TensorFlow.js 具有许多优势，例如更高的灵活性和可移植性。移动设备通常资源受限，因此能够在设备上运行机器学习模型是一个巨大的优势。

## 设置环境

在我们开始之前，我们需要设置我们的开发环境。我们需要安装 Node.js 和 TensorFlow.js 库。

可以从官方网站（https://nodejs.org/en/）下载并安装 Node.js。安装 Node.js 后，我们可以使用 Node Package Manager (npm) 安装 TensorFlow.js。

```
npm install @tensorflow/tfjs
```

## 你好，TensorFlow.js！

现在我们已经设置好了环境，让我们来编写我们的第一个 TensorFlow.js 程序吧！

```javascript
// Load the TensorFlow.js library
const tf = require('@tensorflow/tfjs');

// Define a TensorFlow.js model
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));

// Compile the model
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

// Fit the model to the data
const xs = tf.tensor2d([-1.0, 0.0, 1.0, 2.0, 3.0, 4.0], [6, 1]);
const ys = tf.tensor2d([-3.0, -1.0, 1.0, 3.0, 5.0, 7.0], [6, 1]);

model.fit(xs, ys, {epochs: 500}).then(() => {
  // Use the model to predict the output of a new Tensor
  model.predict(tf.tensor2d([5], [1, 1])).print();
});
```

在这个程序中，我们首先使用 require() 函数加载 TensorFlow.js 库。然后我们使用 tf.sequential() 函数定义一个顺序模型。

接下来，我们使用 tf.layers.dense() 函数向模型添加一个密集层。该层有一个单元并期望大小为 1 的输入。

添加层后，我们使用 tf.compile() 函数编译模型。我们指定我们要使用均方误差损失函数和随机梯度下降优化器。

最后，我们使用 tf.fit() 函数将模型拟合到数据。我们指定要运行 500 个训练周期。

训练模型后，我们使用 tf.predict() 函数来预测新 Tensor 的输出。在这种情况下，我们预测张量 [5] 的输出。

## 在移动设备上运行 TensorFlow.js

现在我们已经了解了如何编写 TensorFlow.js 程序，让我们看看如何在移动设备上运行它。

有两种方法可以在移动设备上运行 TensorFlow.js：使用网络浏览器或使用本机应用程序。

如果我们想使用网络浏览器，我们需要确保我们的 TensorFlow.js 程序正在网络服务器上运行。我们可以使用任何 Web 服务器，但对于本示例，我们将使用 Node.js。

首先，我们需要安装 http-server npm 包。

```
npm install http-server
```

安装 http-server 包后，我们可以使用它从命令行启动 Web 服务器。

```
http-server
```

这将在端口 8080 上启动一个 Web 服务器。我们现在可以通过在 Web 浏览器中转到 http://localhost:8080 来访问我们的 TensorFlow.js 程序。

如果我们想使用原生应用程序，我们需要使用特定于平台的 TensorFlow.js 库。对于 iOS，我们可以使用 TensorFlow Lite Swift 库 (https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/swift)。对于 Android，我们可以使用 TensorFlow Lite Android 库 (https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/android)。

## 结论

在本文中，我们了解了如何在移动设备上将 TensorFlow.js 与 Node.js 结合使用。与传统的服务器端机器学习框架相比，TensorFlow.js 具有许多优势，例如更高的灵活性和可移植性。移动设备通常资源受限，因此能够在设备上运行机器学习模型是一个巨大的优势。