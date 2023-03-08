---
title: 018：使用 TensorFlow.js 和 Node.js 进行视频分析
description: 
published: true
date: 2023-02-02T11:04:51.592Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:04:49.940Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [018: Video Analysis with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/018-video-analysis-with-tensorflow-js-and-node-js)
{.links-list}


## 介绍

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 执行视频分析。我们将使用预先训练的模型来识别视频中的对象，然后在它们四处移动时对其进行跟踪。

我们将使用以下工具和库：

-TensorFlow.js
- 节点.js
- ffmpeg（可选）

## 什么是 TensorFlow.js？

TensorFlow.js 是一个用于训练和部署机器学习模型的 JavaScript 库。它用于深度学习和传统机器学习。

## 什么是 Node.js？

Node.js 是用于开发服务器端应用程序的 JavaScript 运行时。

## 设置环境

在我们开始之前，我们需要设置我们的环境。我们需要安装 Node.js 和 TensorFlow.js。

如果您尚未安装 Node.js，可以从 [Node.js 网站](https://nodejs.org/en/) 下载。

安装 Node.js 后，我们可以使用以下命令安装 TensorFlow.js：

```
npm install @tensorflow/tfjs
```

## 将视频转换为合适的格式

为了使用预训练模型，我们需要将视频转换成模型可以理解的格式。该模型期望视频为具有特定分辨率和帧速率的 MPEG-4 格式。

如果你安装了ffmpeg，你可以使用下面的命令来转换视频：

```
ffmpeg -i input.mp4 -vf scale=640:360 -r 30 output.mp4
```

如果您没有安装 ffmpeg，可以从 [ffmpeg 网站](https://ffmpeg.org/) 下载。

## 分析视频

现在我们已经设置了环境并转换了视频，我们可以开始分析它了。

我们将使用名为 [YOLOv2](https://pjreddie.com/darknet/yolo/) 的预训练模型。该模型是在 [Pascal VOC](http://host.robots.ox.ac.uk/pascal/VOC/) 数据集上训练的，可以识别 20 种不同的对象类别。

要使用该模型，我们首先需要将其加载到 TensorFlow.js 中。我们可以使用以下代码来做到这一点：

```javascript
const tf = require('@tensorflow/tfjs');

const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v2_1.0_224/model.json');
```

加载模型后，我们就可以开始分析视频了。我们需要将视频的每一帧传递到模型中并得到预测结果。

为此，我们首先需要获取视频中所有帧的列表。我们可以使用以下代码来做到这一点：

```javascript
const fs = require('fs');
const { exec } = require('child_process');

exec('ffmpeg -i input.mp4 -vf scale=640:360 -r 30 output.mp4', (err, stdout, stderr) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(stdout);
  console.log(stderr);
});
```

一旦我们有了帧列表，我们就可以开始分析视频了。对于每一帧，我们需要将其传递到模型中并取回预测。

为此，我们首先需要获取视频中所有帧的列表。我们可以使用以下代码来做到这一点：

```javascript
const fs = require('fs');
const { exec } = require('child_process');

exec('ffmpeg -i input.mp4 -vf scale=640:360 -r 30 output.mp4', (err, stdout, stderr) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(stdout);
  console.log(stderr);
});
```

一旦我们有了帧列表，我们就可以开始分析视频了。对于每一帧，我们需要将其传递到模型中并取回预测。

为此，我们首先需要获取视频中所有帧的列表。我们可以使用以下代码来做到这一点：

```javascript
const fs = require('fs');
const { exec } = require('child_process');

exec('ffmpeg -i input.mp4 -vf scale=640:360 -r 30 output.mp4', (err, stdout, stderr) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(stdout);
  console.log(stderr);
});
```

一旦我们有了帧列表，我们就可以开始分析视频了。对于每一帧，我们需要将其传递到模型中并取回预测。

为此，我们将使用以下代码：

```javascript
const fs = require('fs');
const { exec } = require('child_process');

exec('ffmpeg -i input.mp4 -vf scale=640:360 -r 30 output.mp4', (err, stdout, stderr) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(stdout);
  console.log(stderr);
});
```

此代码会将视频加载到 TensorFlow.js 中，分析每一帧，然后将结果输出到控制台。

## 跟踪对象

现在我们有了每个帧的预测，我们可以开始跟踪对象了。为此，我们将使用 [卡尔曼滤波器](https://en.wikipedia.org/wiki/Kalman_filter)。

卡尔曼滤波器是一种数学模型，可以根据过去的观察预测系统的未来状态。

我们将使用卡尔曼滤波器根据过去的位置预测每个对象的未来位置。这将使我们能够跟踪视频中移动的对象。

要使用卡尔曼滤波器，我们首先需要安装 [kalman-filter](https://www.npmjs.com/package/kalman-filter) 库。我们可以使用以下命令执行此操作：

```
npm install kalman-filter
```

安装库后，我们可以使用以下代码来跟踪对象：

```javascript
const kf = new KalmanFilter();

const trackedObjects = [];

for (const prediction of predictions) {
  const trackedObject = trackedObjects.find(obj => obj.id === prediction.id);

  if (trackedObject) {
    trackedObject.update(prediction);
  } else {
    trackedObjects.push(new TrackedObject(prediction));
  }
}
```

此代码将跟踪视频中的对象并将它们的位置输出到控制台。

## 可视化结果

现在我们有了预测和跟踪的对象，我们可以开始可视化结果了。

我们将使用 [PIXI.js](https://www.pixijs.com/) 库在每个对象周围绘制一个框。

首先，我们需要安装 [pixi.js](https://www.npmjs.com/package/pixi.js) 库。我们可以使用以下命令执行此操作：

```
npm install pixi.js
```

安装库后，我们可以使用以下代码绘制框：

```javascript
const app = new PIXI.Application();

document.body.appendChild(app.view);

const graphics = new PIXI.Graphics();

app.stage.addChild(graphics);

for (const trackedObject of trackedObjects) {
  const { x, y, width, height } = trackedObject;

  graphics.lineStyle(1, 0xffffff);
  graphics.drawRect(x, y, width, height);
}
```

此代码将在视频中的每个对象周围绘制一个框。

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 执行视频分析。我们使用预先训练的模型来识别视频中的对象，然后在它们四处移动时对其进行跟踪。

我们还了解了如何使用卡尔曼滤波器根据过去的位置预测每个对象的未来位置。这使我们能够跟踪视频中移动的对象。

最后，我们了解了如何使用 PIXI.js 库在每个对象周围绘制一个框。