---
title: 083：在 Node.js 中将 TensorFlow.js 与其他 ML 框架结合使用
description: 
published: true
date: 2023-02-03T02:17:27.248Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:17:25.689Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [083: Using TensorFlow.js with Other ML Frameworks in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/083-using-tensorflow-js-with-other-ml-frameworks-in-node-js)
{.links-list}


# 在 Node.js 中将 TensorFlow.js 与其他 ML 框架结合使用

TensorFlow.js 是一个强大的 JavaScript 库，用于训练和部署机器学习模型。它可以与其他 ML 框架（例如 TensorFlow Lite）一起使用，以在 Node.js 上运行推理。

在本文中，我们将向您展示如何在 Node.js 中将 TensorFlow.js 与其他 ML 框架结合使用。我们还将提供一些有关如何充分利用 TensorFlow.js 的技巧。

## 将 TensorFlow.js 与 TensorFlow Lite 结合使用

TensorFlow.js 可与 TensorFlow Lite 一起使用以在 Node.js 上运行推理。 TensorFlow Lite 是一个用于在移动设备上运行机器学习模型的轻量级框架。

要将 TensorFlow.js 与 TensorFlow Lite 结合使用，您需要安装 TensorFlow Lite Node.js 绑定。你可以用 npm 做到这一点：

```
npm install @tensorflow/tfjs-node
```

安装绑定后，您可以使用“tensorflow.js”模块加载 TensorFlow Lite 模型并对其运行推理。

以下是如何将 TensorFlow.js 与 TensorFlow Lite 结合使用的示例：

```javascript
const tf = require('@tensorflow/tfjs-node');

// Load a TensorFlow Lite model.
const model = await tf.loadLiteModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_1.0_224/model.json');

// Run inference on a TensorFlow Lite model.
const output = model.predict(tf.zeros([1, 224, 224, 3]));

// Print the output of the model.
console.log(output);
```

## 将 TensorFlow.js 与其他 ML 框架一起使用

TensorFlow.js 还可以与其他 ML 框架（例如 Keras）一起使用，以在 Node.js 上运行推理。

要将 TensorFlow.js 与 Keras 结合使用，您需要安装 TensorFlow.js Node.js 绑定。你可以用 npm 做到这一点：

```
npm install @tensorflow/tfjs
```

安装绑定后，您可以使用 `tf` 模块加载 Keras 模型并对其运行推理。

以下是如何将 TensorFlow.js 与 Keras 结合使用的示例：

```javascript
const tf = require('@tensorflow/tfjs');

// Load a Keras model.
const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_1.0_224/model.json');

// Run inference on a Keras model.
const output = model.predict(tf.zeros([1, 224, 224, 3]));

// Print the output of the model.
console.log(output);
```

## 使用 TensorFlow.js 的技巧

以下是使用 TensorFlow.js 的一些提示：

- 如果您是 TensorFlow.js 的新手，我们建议您从 [TensorFlow.js 入门指南](https://js.tensorflow.org/tutorials/getting-started.html) 开始。
- 如果您将 TensorFlow.js 与其他 ML 框架一起使用，我们建议使用 [TensorFlow.js Node.js 绑定](https://www.npmjs.com/package/@tensorflow/tfjs)。
- 如果您将 TensorFlow.js 与 TensorFlow Lite 结合使用，我们建议使用 [TensorFlow Lite Node.js 绑定](https://www.npmjs.com/package/@tensorflow/tfjs-node)。
- 如果您通过网络浏览器使用 TensorFlow.js，我们建议使用 [基于 WebAssembly 的后端](https://js.tensorflow.org/api/0.12.0/# enabling-webassembly-support)。