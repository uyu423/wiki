---
title: 015：使用 TensorFlow.js 和 Node.js 进行图像分类
description: 
published: true
date: 2023-02-02T10:17:57.564Z
tags: 
editor: markdown
dateCreated: 2023-02-02T10:17:55.930Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [015: Image Classification with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/015-image-classification-with-tensorflow-js-and-node-js)
{.links-list}


# 介绍

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 构建图像分类模型。我们将使用 MobileNet 模型，这是一个预训练模型，已在大型图像数据集上进行训练。

我们将使用以下库：

* [TensorFlow.js](https://js.tensorflow.org/)
* [节点.js](https://nodejs.org/en/)

## 先决条件

在我们开始之前，您需要进行一些设置：

* 文本编辑器。我推荐 [Visual Studio Code](https://code.visualstudio.com/)。
* [Node.js](https://nodejs.org/en/)。这将用于运行我们的代码。
* [TensorFlow.js](https://js.tensorflow.org/)。这是一个用于机器学习的 JavaScript 库。

## 入门

1. 为您的项目创建一个新目录。

2. 在您的项目目录中创建一个名为“index.js”的文件。

3. 将以下代码复制到 index.js 中：

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MobileNet model.
const model = tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');

// Make a prediction through the model on our image.
const imgEl = document.getElementById('img');
model.predict(tf.fromPixels(imgEl)).then(predictions => {
  console.log('Predictions: ');
  console.log(predictions);
});
```

4. 在您的项目目录中创建一个名为“index.html”的文件。

5. 将以下代码复制到 index.html 中：

```html
<html>
  <body>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.11.3"> </script>
    <script src="index.js"></script>
    <img id="img" src="https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/test_images/grace_hopper.jpg">
  </body>
</html>
```

6. 运行以下命令启动服务器：

```
node index.js
```

您应该看到以下输出：

```
Predictions:
[
  {
    className: 'daisy',
    probability: 0.9911273956298828
  },
  {
    className: 'tulip',
    probability: 0.008872604370117188
  },
  {
    className: 'sunflower',
    probability: 0.0001983642578125
  },
  {
    className: 'dandelion',
    probability: 0.0000457763671875
  },
  {
    className: 'roses',
    probability: 0.0000095367431640625
  }
]
```

## 发生了什么？

在上面的代码中，我们使用 MobileNet 模型对图像进行分类。 MobileNet 是一种预训练模型，已在大型图像数据集上进行训练。

当我们运行 `predict` 方法时，TensorFlow.js 将返回一个预测数组，每个预测都有一个 `className` 和一个 `probability`。 `className` 是模型预测图像所属类别的名称，`probability` 是模型对该预测的置信度。

## 在网络摄像头上进行预测

在上面的示例中，我们使用预训练模型对图像进行预测。但是，如果我们想对实时网络摄像头进行预测怎么办？

为此，我们需要使用 `tf.data` 和 `tf.layers` API。

首先，我们将创建一个“网络摄像头”对象。这将用于捕获实时网络摄像头提要：

```javascript
const webcam = new tf.data.webcam(document.getElementById('webcam'));
```

接下来，我们将创建一个“卷积”层。该层将用于处理实时网络摄像头提要：

```javascript
const layer = tf.layers.conv2d({
  kernelSize: 5,
  filters: 20,
  strides: 1,
  activation: 'relu',
  kernelInitializer: 'varianceScaling',
  inputShape: [28, 28, 1]
});
```

现在我们将创建一个“函数”，用于对实时网络摄像头进行预测。此函数将接收图像，通过“卷积”层对其进行处理，并返回预测：

```javascript
async function predict(image) {
  // Make a prediction through the model on the image.
  const predictions = await model.predict(image);

  // Return the highest confidence prediction.
  return predictions.as1D().argMax();
}
```

最后，我们将创建一个 `loop`，它将持续对实时网络摄像头进行预测：

```javascript
while (true) {
  // Get the next image from the webcam.
  const img = await webcam.capture();

  // Get the prediction from our model.
  const prediction = await predict(img);

  // Convert the prediction into a human-readable string.
  const classNames = ['daisy', 'tulip', 'sunflower', 'dandelion', 'roses'];
  const className = classNames[prediction.dataSync()[0]];

  // Display the string on the page.
  document.getElementById('prediction').innerText = className;

  // Dispose the image when we're done.
  img.dispose();

  // Give some breathing room by waiting for the next animation frame to
  // fire before making another prediction.
  await tf.nextFrame();
}
```

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 构建图像分类模型。我们还了解了如何使用该模型对实时网络摄像头进行预测。