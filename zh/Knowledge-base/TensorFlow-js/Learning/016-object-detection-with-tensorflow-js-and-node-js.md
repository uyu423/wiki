---
title: 016：使用 TensorFlow.js 和 Node.js 进行对象检测
description: 
published: true
date: 2023-02-02T10:36:33.951Z
tags: 
editor: markdown
dateCreated: 2023-02-02T10:36:32.418Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [016: Object Detection with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/016-object-detection-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 进行对象检测

在本文中，我们将学习如何使用 TensorFlow.js 和 Node.js 对图像执行实时对象检测。

我们将从设置开发环境开始，然后安装 TensorFlow.js 及其依赖项。接下来，我们将编写一个 Node.js 脚本来加载图像，对其运行对象检测，并将结果绘制到屏幕上。最后，我们将查看一些可用于进一步学习的资源。

## 搭建开发环境

在开始之前，我们需要搭建一个开发环境。对于这篇文章，我们将使用 Node.js。

如果您尚未安装 Node.js，可以从 [Node.js 网站](https://nodejs.org/en/) 下载。安装 Node.js 后，您可以创建一个新的项目目录并使用以下命令对其进行初始化：

```
mkdir object-detection
cd object-detection
npm init -y
```

## 安装 TensorFlow.js 及其依赖项

现在我们已经设置了一个项目目录，我们可以安装 TensorFlow.js 及其依赖项。我们将使用 [tfjs-node](https://www.npmjs.com/package/@tensorflow/tfjs-node) 包，它提供了可在 Node.js 上使用的 TensorFlow.js 的实现。

要安装 tfjs-node 及其依赖项，请运行以下命令：

```
npm install @tensorflow/tfjs-node
```

## 编写对象检测脚本

安装 TensorFlow.js 后，我们现在可以编写脚本来对图像执行对象检测。我们将从加载图像开始，然后我们将使用 [tf.data.detectObjects](https://js.tensorflow.org/api/latest/# tf.data.detectObjects) 方法运行对象检测图片。最后，我们将结果绘制到屏幕上。

[此处](https://github.com/tensorflow/tfjs-models/blob/master/tfjs-models/src/object_detection/index.js) 提供了完整的脚本，但我们将在下面介绍关键部分.

首先，我们需要加载 tfjs-node 包：

```javascript
const tf = require('@tensorflow/tfjs-node');
```

接下来，我们将加载 [coco-ssd 模型](https://github.com/tensorflow/tfjs-models/tree/master/tfjs-models/detection)，我们将使用它进行对象检测。 coco-ssd 模型是在 [Common Objects in Context (COCO) 数据集](http://cocodataset.org/# home) 上训练的单次检测模型。

```javascript
const cocoSSD = require('@tensorflow-models/coco-ssd');
```

加载模型后，我们现在可以编写代码来加载图像并在其上运行对象检测。我们将从使用 [tf.node.decodeImage](https://js.tensorflow.org/api/latest/# tf.node.decodeImage) 方法加载图像开始。此方法返回一个解析为包含图像数据的张量的承诺。

```javascript
const image = tf.node.decodeImage(
  fs.readFileSync('./test-image.jpg')
);
```

加载图像后，我们可以使用 [tf.data.detectObjects](https://js.tensorflow.org/api/latest/# tf.data.detectObjects) 方法对其运行对象检测。此方法返回一个解析为对象数组的承诺，每个对象都包含有关检测到的对象的信息，包括对象的类及其在图像中的位置。

```javascript
const predictions = await cocoSSD.detectObjects(image);
```

最后，我们将结果绘制到屏幕上。我们将使用 [tf.node.drawBoxes](https://js.tensorflow.org/api/latest/# tf.node.drawBoxes) 方法在检测到的对象周围绘制框，并使用 [tf.node. writeFile](https://js.tensorflow.org/api/latest/#tf.node.writeFile) 方法将结果写入新的图像文件。

```javascript
const drawnImage = tf.node.drawBoxes(
  image,
  predictions.map(prediction => prediction.bbox)
);
tf.node.writeFile('./test-image-output.jpg', drawnImage.toBuffer());
```

## 运行对象检测脚本

编写脚本后，我们现在可以运行它来对图像执行对象检测。要运行脚本，请使用以下命令：

```
node index.js
```

这将在图像“test-image.jpg”上运行对象检测脚本，并将结果写入“test-image-output.jpg”。

## 进一步学习的资源

- [TensorFlow.js 对象检测](https://js.tensorflow.org/tutorials/object-detection.html)
- [使用 TensorFlow.js 和 Node.js 进行实时对象检测](https://www.twilio.com/blog/real-time-object-detection-tensorflow-js-node-js)
- [使用网络摄像头检测对象](https://codelabs.developers.google.com/codelabs/tensorflowjs-object-detection/index.html)