---
title: 017：使用 TensorFlow.js 和 Node.js 进行图像分割
description: 
published: true
date: 2023-02-02T10:44:35.956Z
tags: 
editor: markdown
dateCreated: 2023-02-02T10:44:34.204Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [017: Image Segmentation with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/017-image-segmentation-with-tensorflow-js-and-node-js)
{.links-list}


# 介绍

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 执行图像分割。图像分割是将图像划分为不同区域的过程。这通常用于计算机视觉应用程序以识别图像中的对象。

我们将使用 [TensorFlow.js](https://js.tensorflow.org/) 库进行图像分割。 TensorFlow.js 是一个用于训练和部署机器学习模型的 JavaScript 库。它用于浏览器中的深度学习和 Node.js。

我们将在示例中使用 [Node.js](https://nodejs.org/) 运行时。 Node.js 是一个 JavaScript 运行时，允许您在浏览器之外运行 JavaScript 代码。它通常用于服务器端编程。

## 入门

在开始之前，我们需要安装 TensorFlow.js 和 Node.js 依赖项。我们可以使用 [npm](https://www.npmjs.com/) 包管理器来做到这一点。

首先，为我们的项目创建一个新目录：

```
mkdir image-segmentation
```

接下来，我们需要初始化一个新的 npm 项目。我们可以通过运行以下命令来完成此操作：

```
npm init -y
```

这将在我们的项目目录中创建一个名为“package.json”的新文件。该文件包含有关我们项目的信息，例如我们需要安装的依赖项。

现在，我们可以安装 TensorFlow.js 和 Node.js 依赖项。我们将使用 [tfjs-node](https://www.npmjs.com/package/@tensorflow/tfjs-node) 包，它允许我们在 Node.js 中运行 TensorFlow.js。

要安装依赖项，请运行以下命令：

```
npm install @tensorflow/tfjs-node
```

这将在我们的项目中安装 TensorFlow.js 和 Node.js 依赖项。

## 加载图像

现在我们已经安装了依赖项，可以开始编写图像分割程序了。

首先，我们需要加载图像。我们将使用 [tf.node.decodeImage](https://js.tensorflow.org/api/latest/# node.decodeImage) 函数来加载我们的图像。此函数接收包含图像数据的“缓冲区”并返回包含图像数据的“tf.Tensor3D”。

我们可以使用 [fs](https://nodejs.org/api/fs.html) 模块读取图像数据，该模块是 Node.js 标准库的一部分。 [fs.readFile](https://nodejs.org/api/fs.html# fs_fs_readfile_path_options_callback) 函数接受图像的路径并将图像数据作为“缓冲区”返回。

要使用 `fs` 模块，我们需要将其导入到我们的程序中。我们可以使用 [require](https://nodejs.org/api/modules.html# modules_require_id) 函数来做到这一点。

```javascript
const fs = require('fs');
```

现在我们已经导入了 `fs` 模块，我们可以使用 `fs.readFile` 函数来读取我们的图像数据。

```javascript
const imageData = fs.readFileSync('image.jpg');
```

`imageData` 变量现在包含我们的图像数据作为 `buffer`。

接下来，我们需要解码我们的图像数据。我们可以使用 `tf.node.decodeImage` 函数来做到这一点。

```javascript
const imageTensor = tf.node.decodeImage(imageData);
```

`imageTensor` 变量现在包含我们的图像数据作为 `tf.Tensor3D`。

## 预处理图像

在执行图像分割之前，我们需要对图像进行预处理。这涉及对我们的图像数据执行一些操作以准备分割。

首先，我们需要调整图像的大小。我们将使用 [tf.image.resizeBilinear](https://js.tensorflow.org/api/latest/# tf.image.resizeBilinear) 函数来调整图像大小。此函数接受图像“tf.Tensor”和大小（“[高度，宽度]”）并返回调整大小的图像“tf.Tensor”。

我们将调整图像大小为 `[128, 128]`。

```javascript
const imageSize = [128, 128];
const imageTensor = tf.image.resizeBilinear(imageTensor, imageSize);
```

`imageTensor` 变量现在包含我们调整大小的图像数据作为 `tf.Tensor3D`。

接下来，我们需要规范化我们的图像数据。我们将使用 [tf.image.normalize](https://js.tensorflow.org/api/latest/# tf.image.normalize) 函数来标准化我们的图像。此函数接收图像“tf.Tensor”并返回归一化图像“tf.Tensor”。

我们将通过减去平均值并除以标准差来标准化我们的图像。

```javascript
const imageTensor = tf.image.normalize(imageTensor, [0, 255], -1, 1);
```

`imageTensor` 变量现在包含我们的标准化图像数据作为 `tf.Tensor3D`。

## 执行图像分割

现在我们已经对图像进行了预处理，我们可以执行图像分割。我们将使用 [tf.image.segmentation.segmentationKMeans](https://js.tensorflow.org/api/latest/# tf.image.segmentation.segmentationKMeans) 函数来执行图像分割。此函数接收图像“tf.Tensor”并返回分割图“tf.Tensor”。

我们将把图像分割成“4”个区域。

```javascript
const numSegments = 4;
const segmentationMap = tf.image.segmentation.segmentationKMeans(imageTensor, numSegments);
```

`segmentationMap` 变量现在包含我们的分割图作为 `tf.Tensor3D`。

## 可视化分割图

现在我们已经分割了图像，我们需要可视化分割图。我们可以使用 [tf.tensor3d](https://js.tensorflow.org/api/latest/# tf.tensor3d) 函数来做到这一点。此函数接受一个数字数组并返回一个“tf.Tensor3D”。

首先，我们需要将分割图“tf.Tensor”转换为数组。我们可以使用 [tf.tensor3d](https://js.tensorflow.org/api/latest/# tf.tensor3d) 函数来做到这一点。

```javascript
const segmentationMapArray = segmentationMap.arraySync();
```

`segmentationMapArray` 变量现在包含我们的分割图作为数组。

接下来，我们需要将分割图数组转换为“tf.Tensor3D”。我们可以使用 [tf.tensor3d](https://js.tensorflow.org/api/latest/# tf.tensor3d) 函数来做到这一点。

```javascript
const segmentationMapTensor = tf.tensor3d(segmentationMapArray);
```

`segmentationMapTensor` 变量现在包含我们的分割图作为 `tf.Tensor3D`。

最后，我们可以使用 [tf.image.resizeBilinear](https://js.tensorflow.org/api/latest/# tf.image.resizeBilinear) 函数可视化我们的分割图。此函数接受图像“tf.Tensor”和大小（“[高度，宽度]”）并返回调整大小的图像“tf.Tensor”。

我们会将分割图调整为图像的原始大小。

```javascript
const segmentationMapImage = tf.image.resizeBilinear(segmentationMapTensor, [imageHeight, imageWidth]);
```

`segmentationMapImage` 变量现在包含我们的分割图作为 `tf.Tensor3D`。

## 保存分割图

现在我们已经可视化了我们的分割图，我们需要保存它。我们可以使用 [tf.node.encodePng](https://js.tensorflow.org/api/latest/# node.encodePng) 函数来做到这一点。此函数接收图像“tf.Tensor”并返回包含 PNG 数据的“缓冲区”。

我们可以使用 [fs](https://nodejs.org/api/fs.html) 模块将这些数据写入文件。 [fs.writeFile](https://nodejs.org/api/fs.html# fs_fs_writefile_file_data_options_callback) 函数接受文件路径、要写入的数据和回调函数。

要使用 `fs` 模块，我们需要将其导入到我们的程序中。我们可以使用 [require](https://nodejs.org/api/modules.html# modules_require_id) 函数来做到这一点。

```javascript
const fs = require('fs');
```

现在我们已经导入了 `fs` 模块，我们可以使用 `fs.writeFile` 函数将我们的分割地图数据写入文件。

```javascript
const segmentationMapData = tf.node.encodePng(segmentationMapImage);
fs.writeFileSync('segmentation-map.png', segmentationMapData);
```

这会将我们的分割地图数据写入名为“segmentation-map.png”的文件。

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 执行图像分割。我们还了解了如何可视化分割图并将其保存到文件中。

图像分割是计算机视觉应用的强大工具。 TensorFlow.js 使在浏览器和 Node.js 中执行图像分割变得容易。