---
title: 036：将预训练模型与 TensorFlow.js 和 Node.js 结合使用
description: 
published: true
date: 2023-02-02T15:36:43.932Z
tags: 
editor: markdown
dateCreated: 2023-02-02T15:36:42.355Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [036: Using Pretrained Models with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/036-using-pretrained-models-with-tensorflow-js-and-node-js)
{.links-list}


# 介绍

在本文中，我们将学习如何将预训练模型与 TensorFlow.js 和 Node.js 结合使用。我们将从讨论什么是预训练模型以及它们为何有用开始。然后，我们将介绍如何在 TensorFlow.js 中加载和使用预训练模型。最后，我们将了解如何使用 Node.js 部署预训练模型。

# 什么是预训练模型？

预训练模型是已经在大型数据集上训练过的模型。这些模型可用于执行各种任务，例如图像分类、对象检测和文本分类。

预训练模型很有用，因为它们允许我们使用大型数据集的知识，而无需从头开始训练我们自己的模型。这可以为我们节省很多时间和精力。

# 加载预训练模型

TensorFlow.js 提供了许多预训练模型，可以在您自己的应用程序中加载和使用。要加载预训练模型，您首先需要安装 TensorFlow.js。您可以使用 npm 执行此操作：

```
npm install @tensorflow/tfjs
```

安装 TensorFlow.js 后，您可以使用 tf.loadModel() 函数加载预训练模型。例如，要加载 MobileNet 模型，您可以使用以下代码：

```javascript
const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

# 使用预训练模型

加载预训练模型后，您可以使用它执行各种任务。例如，如果您使用的是预训练图像分类模型，则可以使用该模型对图像进行分类。

要使用预训练模型，您首先需要获取模型的输入层和输出层。您可以使用 model.inputs 和 model.outputs 属性执行此操作。例如，要获取 MobileNet 模型的输入层和输出层，您可以使用以下代码：

```javascript
const inputLayer = model.inputs[0];
const outputLayer = model.outputs[0];
```

拥有模型的输入层和输出层后，您可以使用 tf.tidy() 函数运行推理。 tf.tidy() 函数将清理在推理过程中创建的任何 tf.js 张量。这很重要，因为 tf.js 张量会占用大量内存。

要使用 tf.tidy() 函数，您需要传递一个包含运行推理代码的函数。此功能将在整洁的上下文中执行。例如，要在 MobileNet 模型上运行推理，您可以使用以下代码：

```javascript
const results = tf.tidy(() => {
  // inputLayer is a tf.js Tensor with shape [1, 224, 224, 3]
  // outputLayer is a tf.js Tensor with shape [1, 1000]
  const output = model.predict(inputLayer);
  return output.dataSync();
});
```

# 部署预训练模型

训练完模型后，您需要对其进行部署，以便其他应用程序可以使用它。 TensorFlow.js 提供了多种部署预训练模型的方法。

部署预训练模型的一种方法是使用 tf.model.save() 函数。此函数会将模型保存到 JSON 文件中。例如，要保存 MobileNet 模型，您可以使用以下代码：

```javascript
await model.save('file:///model');
```

然后，您可以使用 tf.loadModel() 函数从 JSON 文件加载模型。

另一种部署预训练模型的方法是使用 tf.model.toJSON() 函数。此函数将模型作为 JSON 对象返回。例如，要将 MobileNet 模型作为 JSON 对象获取，您可以使用以下代码：

```javascript
const modelAsJSON = model.toJSON();
```

然后，您可以将 JSON 对象保存到文件或数据库中。

# 结论

在本文中，我们学习了如何将预训练模型与 TensorFlow.js 和 Node.js 结合使用。我们已经了解了如何加载和使用预训练模型，以及如何部署预训练模型。