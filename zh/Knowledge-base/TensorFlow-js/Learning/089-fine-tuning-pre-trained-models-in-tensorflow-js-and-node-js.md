---
title: 089：在 TensorFlow.js 和 Node.js 中微调预训练模型
description: 
published: true
date: 2023-02-03T03:44:04.110Z
tags: 
editor: markdown
dateCreated: 2023-02-03T03:43:59.388Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [089: Fine-Tuning Pre-Trained Models in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/089-fine-tuning-pre-trained-models-in-tensorflow-js-and-node-js)
{.links-list}


# 089：在 TensorFlow.js 和 Node.js 中微调预训练模型

TensorFlow.js 是一个强大的工具，它允许我们在浏览器中训练和部署机器学习模型。在本文中，我们将学习如何在 TensorFlow.js 和 Node.js 中微调预训练模型。

## 什么是预训练模型？

预训练模型是在大型数据集上训练过的机器学习模型。这些模型可用于执行图像分类、对象检测和文本分类等任务。

## 为什么微调预训练模型？

微调预训练模型是机器学习中的常用技术。它允许我们将预训练模型适应我们自己的数据集。当我们的数据集很小或者我们想要提高数据集上预训练模型的性能时，这会很有用。

## 如何微调预训练模型？

微调预训练模型的常用方法有两种：

1. **迁移学习**：我们可以使用预训练模型作为起点，然后在我们自己的数据集上进行训练。当我们的数据集很小时，这是一种常见的技术。

2. **微调**：我们可以使用预训练的模型，然后在我们自己的数据集上对其进行微调。当我们想要提高数据集上预训练模型的性能时，这是一种常用技术。

在这篇文章中，我们将重点关注微调预训练模型。

## 在 TensorFlow.js 中微调预训练模型

TensorFlow.js 提供了用于微调预训练模型的高级 API。我们将使用“tf.fineTuneModel()”函数来微调预训练模型。

首先，我们需要加载一个预训练模型。我们将使用 `tf.loadLayersModel()` 函数从 URL 加载预训练模型。

接下来，我们需要定义模型的输入和输出。我们将使用 `tf.input()` 和 `tf.output()` 函数来定义模型的输入和输出。

最后，我们需要调用 `tf.fineTuneModel()` 函数对预训练模型进行微调。我们需要指定优化器、损失和指标。

以下是如何在 TensorFlow.js 中微调预训练模型的示例：

```javascript
// Load a pre-trained model
const model = tf.loadLayersModel('https://model-url');

// Define the inputs and outputs of the model
const input = tf.input({shape: [28, 28, 1]});
const output = model.outputs[0];

// Fine-tune the model
const model = tf.fineTuneModel(
    model,
    {
      optimizer: tf.train.adam(0.001),
      loss: tf.losses.softmaxCrossEntropy,
      metrics: ['accuracy']
    },
    {
      // We will use a validation split of 0.1
      validationSplit: 0.1
    }
);
```

## 在 Node.js 中微调预训练模型

TensorFlow.js 提供了一个 Node.js API 用于微调预训练模型。我们将使用“tf.node.fineTuneModel()”函数来微调预训练模型。

首先，我们需要加载一个预训练模型。我们将使用 `tf.node.loadLayersModel()` 函数从 URL 加载预训练模型。

接下来，我们需要定义模型的输入和输出。我们将使用 `tf.node.input()` 和 `tf.node.output()` 函数来定义模型的输入和输出。

最后，我们需要调用 `tf.node.fineTuneModel()` 函数对预训练模型进行微调。我们需要指定优化器、损失和指标。

以下是如何在 Node.js 中微调预训练模型的示例：

```javascript
// Load a pre-trained model
const model = tf.node.loadLayersModel('https://model-url');

// Define the inputs and outputs of the model
const input = tf.node.input({shape: [28, 28, 1]});
const output = model.outputs[0];

// Fine-tune the model
const model = tf.node.fineTuneModel(
    model,
    {
      optimizer: tf.train.adam(0.001),
      loss: tf.losses.softmaxCrossEntropy,
      metrics: ['accuracy']
    },
    {
      // We will use a validation split of 0.1
      validationSplit: 0.1
    }
);
```

## 结论

在本文中，我们学习了如何在 TensorFlow.js 和 Node.js 中微调预训练模型。我们看到 TensorFlow.js 提供了一个用于微调预训练模型的高级 API。我们还看到 TensorFlow.js 提供了一个 Node.js API 用于微调预训练模型。