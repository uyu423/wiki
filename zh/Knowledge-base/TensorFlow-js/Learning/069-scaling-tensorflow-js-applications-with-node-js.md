---
title: 069：使用 Node.js 扩展 TensorFlow.js 应用程序
description: 
published: true
date: 2023-02-02T23:04:23.265Z
tags: 
editor: markdown
dateCreated: 2023-02-02T23:04:21.725Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [069: Scaling TensorFlow.js Applications with Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/069-scaling-tensorflow-js-applications-with-node-js)
{.links-list}


# 069：使用 Node.js 扩展 TensorFlow.js 应用程序

TensorFlow.js 是一个强大的 JavaScript 机器学习工具，但是当您的 TensorFlow.js 应用程序超出浏览器容量时您会怎么做？在本文中，我们将探讨如何使用 Node.js 扩展 TensorFlow.js 应用程序。

## 什么是 TensorFlow.js？

TensorFlow.js 是一个用于 JavaScript 机器学习的开源库。开发人员使用它来创建在浏览器或 Node.js 中运行的复杂机器学习模型。

## 为什么将 Node.js 用于 TensorFlow.js？

Node.js 是扩展 TensorFlow.js 应用程序的绝佳选择。它快速、高效，并且拥有庞大的库和工具生态系统。

## 如何使用 Node.js 扩展 TensorFlow.js

使用 Node.js 扩展 TensorFlow.js 应用程序有两种主要方法：

1. 使用 `tensorflow.js` Node.js 模块。
2. 使用与 TensorFlow.js 兼容的库，例如 `tfjs-node`。

我们将在下面更详细地探讨这些方法中的每一种。

### 使用 `tensorflow.js` Node.js 模块

`tensorflow.js` Node.js 模块是在 Node.js 中运行 TensorFlow.js 的官方方式。它易于安装和使用。

要安装 `tensorflow.js` Node.js 模块，请运行以下命令：

```
npm install @tensorflow/tfjs
```

要使用 `tensorflow.js` Node.js 模块，请在您的代码中引入它：

```javascript
const tf = require('@tensorflow/tfjs');
```

现在，您可以在 Node.js 应用程序中使用所有 TensorFlow.js API。

### 使用与 TensorFlow.js 兼容的库

如果您想使用与 TensorFlow.js 兼容的库，例如 `tfjs-node`，您需要先安装它。

要安装“tfjs-node”，请运行以下命令：

```
npm install tfjs-node
```

要使用 `tfjs-node`，请在您的代码中要求它：

```javascript
const tf = require('tfjs-node');
```

现在，您可以在 Node.js 应用程序中使用所有 TensorFlow.js API。

## 进一步阅读的资源

- [TensorFlow.js 文档](https://js.tensorflow.org/)
- [tfjs-node 文档](https://github.com/tensorflow/tfjs-node)
- [Node.js 文档](https://nodejs.org/en/docs/)