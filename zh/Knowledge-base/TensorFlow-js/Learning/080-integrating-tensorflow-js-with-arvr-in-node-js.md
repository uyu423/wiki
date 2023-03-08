---
title: 080：在 Node.js 中将 TensorFlow.js 与 AR/VR 集成
description: 
published: true
date: 2023-02-03T01:36:51.256Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:36:49.562Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [080: Integrating TensorFlow.js with AR/VR in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/080-integrating-tensorflow-js-with-arvr-in-node-js)
{.links-list}


# 080：在 Node.js 中将 TensorFlow.js 与 AR/VR 集成

TensorFlow.js 是一个强大的工具，它允许我们创建机器学习模型并在浏览器中运行它们。这使得它非常适合创建可以利用用户设备处理能力的应用程序，而无需强大的服务器。

在本文中，我们将探索如何使用 TensorFlow.js 创建一个简单的增强现实 (AR) 应用程序。我们将使用 Three.js 库在浏览器中渲染 3D 对象，并使用 AR.js 库跟踪用户的头部并将 3D 对象显示在正确的位置。

## 设置项目

我们将从设置一个新的 Node.js 项目开始。为项目创建一个新目录，并运行 `npm init` 来创建一个 `package.json` 文件。

这个项目需要一些库。使用 `npm` 命令安装以下库：

*`张量流`
*`@tensorflow/tfjs-node`
*`三`
*`ar.js`

## 创建模型

现在我们可以创建用于生成 3D 对象的机器学习模型。我们将在这个例子中使用一个简单的线性回归模型。

创建一个名为“model.js”的新文件并导入“@tensorflow/tfjs-node”库。

```javascript
const tf = require('@tensorflow/tfjs-node');
```

接下来，我们将定义一些用于训练模型的常量。 `LEARNING_RATE` 常量定义了模型学习的速度。 `BATCH_SIZE` 常量定义训练模型时要使用的数据点数。 `EPOCHS` 常量定义了模型应该遍历训练数据的次数。

```javascript
const LEARNING_RATE = 0.01;
const BATCH_SIZE = 10;
const EPOCHS = 10;
```

现在我们可以定义模型了。我们将使用“顺序”模型并添加一个“密集”层。 `dense` 层是一个全连接层，它将输入数据乘以一组权重并添加一个偏置项。

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({ units: 1, inputShape: [1] }));
```

我们需要先编译模型，然后才能训练它。我们将使用 sgd 优化器，这是一个简单的梯度下降优化器。我们还将指定模型应最小化的“损失”函数，以及我们要跟踪的“指标”。在这种情况下，我们将跟踪 `meanSquaredError` 和 `meanAbsoluteError`。

```javascript
model.compile({
  optimizer: tf.train.sgd(LEARNING_RATE),
  loss: 'meanSquaredError',
  metrics: ['meanSquaredError', 'meanAbsoluteError']
});
```

## 训练模型

现在我们已经定义了模型，我们需要在一些数据上对其进行训练。我们将在此示例中使用一个简单的数据集，其中包含 10 个点。

```javascript
const xs = tf.tensor2d([-1, 0, 1, 2, 3, 4, 5, 6, 7, 8], [10, 1]);
const ys = tf.tensor2d([-3, -1, 1, 3, 5, 7, 9, 11, 13, 15], [10, 1]);
```

我们现在可以训练模型了。我们将指定 `batchSize`、`epochs` 的数量以及每个 epoch 之前的数据 `shuffle`。我们还将指定一个“validationData”集，模型将使用它来评估每个时期后的损失和指标。

```javascript
model.fit(xs, ys, {
  batchSize: BATCH_SIZE,
  epochs: EPOCHS,
  shuffle: true,
  validationData: [xs, ys]
}).then(() => {
  // The model is trained!
});
```

## 保存模型

一旦模型被训练好，我们需要保存它以便我们可以在浏览器中使用它。我们可以使用 `tf.node.save` 函数将模型保存到 `.pb` 文件中。

```javascript
tf.node.save(model, './model.pb');
```

## 加载模型

现在我们已经保存了模型，我们可以在浏览器中加载它。我们将使用“tf.loadFrozenModel”函数来加载模型。此函数采用 `modelUrl` 和 `weightsManifestUrl`。 `modelUrl` 是我们在上一步中保存的 `.pb` 文件的路径。 `weightsManifestUrl` 是包含模型权重信息的 JSON 文件的路径。

```javascript
const modelUrl = './model.pb';
const weightsManifestUrl = './weights_manifest.json';

tf.loadFrozenModel(modelUrl, weightsManifestUrl).then(model => {
  // The model is loaded!
});
```

## 生成 3D 对象

现在我们已经加载了模型，我们可以使用它来生成 3D 对象。我们将使用 `tf.tensor` 函数从数字数组创建张量。该张量将用作模型的输入。

```javascript
const input = tf.tensor([-1, 0, 1, 2, 3, 4, 5, 6, 7, 8], [10, 1]);
```

我们现在可以使用 model.predict 方法从输入张量生成预测。此方法返回一个 `tf.Tensor` 对象，我们可以使用它来生成 3D 对象。

```javascript
model.predict(input).then(output => {
  // The output tensor can be used to generate 3D objects!
});
```

## 渲染 3D 对象

现在我们已经生成了 3D 对象，我们需要在浏览器中渲染它们。我们将使用 `three.js` 库来执行此操作。

首先，我们需要创建一个 `Scene` 对象。该对象将包含我们要渲染的 3D 对象。

```javascript
const scene = new THREE.Scene();
```

接下来，我们需要创建一个 `Camera` 对象。该对象定义了我们想要查看场景的视角。

```javascript
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
```

现在我们可以创建 `Renderer` 对象。该对象将获取“Scene”和“Camera”对象并将它们渲染到页面。

```javascript
const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);
```

最后，我们需要创建 3D 对象并将它们添加到“场景”对象中。我们将使用上一步中的“输出”张量来生成 3D 对象。

```javascript
const geometry = new THREE.Geometry();
for (let i = 0; i < output.shape[0]; i++) {
  geometry.vertices.push(new THREE.Vector3(i, output.get(i, 0), 0));
}
const material = new THREE.LineBasicMaterial({ color: 0xff0000 });
const line = new THREE.Line(geometry, material);
scene.add(line);
```

## 动画 3D 对象

现在我们已经渲染了 3D 对象，我们需要为它们设置动画。我们将使用 `requestAnimationFrame` 函数来执行此操作。这个函数告诉浏览器在下一次重绘之前调用指定的函数。

```javascript
function animate() {
  requestAnimationFrame(animate);
  renderer.render(scene, camera);
}
animate();
```

## 追踪用户头部

现在我们已经为 3D 对象制作了动画，我们需要跟踪用户的头部，以便 3D 对象出现在正确的位置。我们将使用 `ar.js` 库来执行此操作。

首先，我们需要创建一个 ARController 对象。该对象将跟踪用户的头部并在正确位置显示 3D 对象。

```javascript
const arController = new ARController(renderer, {
  cameraParametersUrl: './camera_para.dat',
  maxDetectionRate: 60,
  canvasWidth: 640,
  canvasHeight: 480
});
```

接下来，我们需要告诉 ARController 跟踪用户的头部。我们可以使用 `loadNFTMarker` 方法来做到这一点。此方法采用 `markerUrl`，这是标记文件的路径。我们可以使用 `markerUrl` 从 `nft-marker-files` 目录加载标记文件。

```javascript
arController.loadNFTMarker('./nft-marker-files/hiro.jpg');
```

最后，我们需要告诉 ARController 开始跟踪用户的头部。我们可以使用 `startNFTMarkerTracking` 方法来做到这一点。

```javascript
arController.startNFTMarkerTracking();
```

## 显示 3D 对象

现在我们已经跟踪了用户的头部，我们可以在正确的位置显示 3D 对象。我们将使用 `arController.getNFTMarker` 方法来获取用户当前正在查看的标记。此方法返回一个 `THREE.Object3D` 对象，我们可以将其添加到 `Scene` 对象中。

```javascript
const marker = arController.getNFTMarker(0);
scene.add(marker);
```

## 就是这样！

这里的所有都是它的！您现在应该有一个工作的 AR 应用程序，可以在相对于用户头部的正确位置渲染 3D 对象。

## 资源

* [TensorFlow.js](https://js.tensorflow.org/)
* [Three.js](https://threejs.org/)
* [AR.js](https://github.com/jeromeetienne/AR.js)