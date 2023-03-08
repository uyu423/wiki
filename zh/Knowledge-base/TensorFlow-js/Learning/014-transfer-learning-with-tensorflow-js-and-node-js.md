---
title: 014：使用 TensorFlow.js 和 Node.js 进行迁移学习
description: 
published: true
date: 2023-02-02T10:04:41.365Z
tags: 
editor: markdown
dateCreated: 2023-02-02T10:04:39.810Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [014: Transfer Learning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/014-transfer-learning-with-tensorflow-js-and-node-js)
{.links-list}


# 介绍

在本文中，我们将研究如何将迁移学习与 TensorFlow.js 和 Node.js 结合使用。迁移学习是一种强大的技术，可以帮助您加速自己的机器学习模型的训练过程。通过从预训练模型开始，您可以节省大量时间和精力，否则这些时间和精力将花费在从头开始训练模型上。

在这篇文章中，我们将讨论以下主题：

- 什么是迁移学习？
- 如何使用 TensorFlow.js 进行迁移学习
- 如何在 Node.js 中使用迁移学习

# 什么是迁移学习？

迁移学习是一种机器学习技术，可让您在新数据集上重复使用预训练模型。当您没有足够的数据从头开始训练模型时，这尤其有用。

迁移学习主要有两种类型：

- **微调：** 这是您采用预训练模型然后在您自己的数据集上进行训练的地方。这通常在您的数据集与用于训练预训练模型的数据集相似时使用。
- **特征提取：**这是您采用预训练模型并使用它从您自己的数据集中提取特征的地方。这通常在您的数据集与用于训练预训练模型的数据集不同时使用。

# 如何在 TensorFlow.js 中使用迁移学习

TensorFlow.js 是一个用于训练和部署机器学习模型的 JavaScript 库。它通过提供一组预训练模型，使您能够将迁移学习与 TensorFlow.js 模型结合使用。

预训练模型是在大型数据集上训练过的模型，然后可供其他人使用。您可以使用这些模型作为训练您自己的模型的起点。

要使用 TensorFlow.js 预训练模型，您首先需要安装 TensorFlow.js 库。您可以使用以下命令执行此操作：

```
npm install @tensorflow/tfjs
```

安装 TensorFlow.js 库后，您可以使用 loadModel() 函数加载预训练模型。例如，要加载 MobileNet 预训练模型，您可以使用以下代码：

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MobileNet model.
const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

加载模型后，您就可以将其用于迁移学习。例如，您可以使用它在您自己的数据集上微调模型。

# 如何在 Node.js 中使用迁移学习

Node.js 是一种 JavaScript 运行时，可让您使用 JavaScript 构建可扩展的网络应用程序。

您可以将 Node.js 与 TensorFlow.js 结合使用来构建使用迁移学习的应用程序。要将 Node.js 与 TensorFlow.js 结合使用，您首先需要安装 TensorFlow.js 库。您可以使用以下命令执行此操作：

```
npm install @tensorflow/tfjs
```

安装 TensorFlow.js 库后，您可以使用 loadModel() 函数加载预训练模型。例如，要加载 MobileNet 预训练模型，您可以使用以下代码：

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MobileNet model.
const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

加载模型后，您就可以将其用于迁移学习。例如，您可以使用它在您自己的数据集上微调模型。

# 结论

在本文中，我们研究了如何通过 TensorFlow.js 和 Node.js 使用迁移学习。迁移学习是一种强大的技术，可以帮助您加速自己的机器学习模型的训练过程。通过从预训练模型开始，您可以节省大量时间和精力，否则这些时间和精力将花费在从头开始训练模型上。