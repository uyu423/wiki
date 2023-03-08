---
title: 039：使用 TensorFlow.js 和 Node.js 进行数据扩充
description: 
published: true
date: 2023-02-02T16:04:31.536Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:04:29.953Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [039: Data Augmentation with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/039-data-augmentation-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 进行数据扩充

## 介绍

数据增强是一种通过从现有数据样本生成新数据样本来人为增加数据集大小的技术。当原始数据集很小并且您想使用尽可能多的数据训练机器学习模型时，这尤其有用。

TensorFlow.js 是一个用于训练和部署机器学习模型的 JavaScript 库。 Node.js 是一个 JavaScript 运行时环境，允许您在 Web 浏览器之外运行 JavaScript 代码。

在本文中，我们将学习如何使用 TensorFlow.js 和 Node.js 执行数据扩充。我们将从了解什么是数据扩充及其有用的原因开始。然后，我们将了解如何在 TensorFlow.js 中实现数据增强。最后，我们将学习如何使用 Node.js 运行我们的数据增强代码。

## 什么是数据增强？

数据增强是一种通过从现有数据样本生成新数据样本来人为增加数据集大小的技术。当原始数据集很小并且您想使用尽可能多的数据训练机器学习模型时，这尤其有用。

数据扩充通过对现有数据样本应用一组转换来工作。然后将转换后的样本用作新的数据样本。例如，如果我们有一个图像数据集，我们可以通过对图像应用旋转、裁剪和翻转等变换来执行数据增强。这将生成可用作数据集一部分的新图像。

数据增强的好处是它可以帮助提高机器学习模型的性能。这是因为扩充后的数据集比原始数据集更大且包含更多种类。这可以帮助模型学习更通用的模式。

## TensorFlow.js 中的数据增强

TensorFlow.js 是一个用于训练和部署机器学习模型的 JavaScript 库。它可以在浏览器或 Node.js 环境中使用。

可以使用“tf.data.Dataset”API 在 TensorFlow.js 中执行数据扩充。此 API 允许您将转换应用于数据集。 `tf.image` 模块包含一组可用于执行图像增强的函数。

要在 TensorFlow.js 中使用数据增强，我们首先需要创建一个“tf.data.Dataset”对象。然后我们可以使用 `tf.image` 模块将转换应用到这个数据集。最后，我们可以使用 .forEachAsync() 方法在每个数据样本上运行增强代码。

## 节点

Node.js 是一个 JavaScript 运行时环境，允许您在 Web 浏览器之外运行 JavaScript 代码。它可用于创建服务器端应用程序。

Node.js 带有一组可用于执行各种任务的内置模块。对于数据扩充，我们将使用 fs 模块，它允许我们读取和写入文件。

## 例子

在此示例中，我们将使用 MNIST 数据集。该数据集包含手写数字的图像。我们将使用“tf.image”模块对该数据集执行数据扩充。

首先，我们需要加载 MNIST 数据集。我们可以使用 `fs` 模块来做到这一点。


```javascript
var fs = require('fs');

var mnistData = fs.readFileSync('mnist.csv', {encoding: 'utf-8'});
```

接下来，我们需要解析 MNIST 数据。我们可以使用“tf.data.csv”模块来做到这一点。


```javascript
var csv = require('@tensorflow/tfjs-data/src/data/csv');

var mnistDataset = csv.parse(mnistData, {
  columnConfigs: {
    label: {
      isLabel: true
    }
  }
});
```

现在我们有了数据集，我们可以开始应用数据扩充了。我们将从创建一个“tf.data.Dataset”对象开始。


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: sample.xs,
    ys: sample.ys
  };
});
```

接下来，我们将对数据集应用“tf.image.resizeBilinear()”转换。此转换将调整图像的大小。


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: tf.image.resizeBilinear(sample.xs, [28, 28]),
    ys: sample.ys
  };
});
```

我们还可以将“tf.image.rotate()”转换应用于数据集。此转换将旋转图像。


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: tf.image.rotate(sample.xs, tf.scalar(Math.random() * 2.0 * Math.PI)),
    ys: sample.ys
  };
});
```

最后，我们将对数据集应用“tf.image.flipLeftRight()”转换。此转换将水平翻转图像。


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: tf.image.flipLeftRight(sample.xs),
    ys: sample.ys
  };
});
```

现在我们已经应用了转换，我们可以使用 .forEachAsync() 方法在每个数据样本上运行数据增强代码。


```javascript
mnistDataset.forEachAsync(function(sample) {
  // augment data here
});
```

## 结论

在本文中，我们学习了如何使用 TensorFlow.js 和 Node.js 执行数据扩充。我们已经了解了如何使用 `tf.data.Dataset` API 将转换应用于数据集。我们还看到了如何使用 .forEachAsync() 方法在每个数据样本上运行数据增强代码。