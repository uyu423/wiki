---
title: 085：使用 TensorFlow.js 和 Node.js 构建端到端机器学习工作流
description: 
published: true
date: 2023-02-03T02:44:28.068Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:44:26.401Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [085: Building End-to-End Machine Learning Workflows with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/085-building-end-to-end-machine-learning-workflows-with-tensorflow-js-and-node-js)
{.links-list}


# 085：使用 TensorFlow.js 和 Node.js 构建端到端机器学习工作流

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 构建端到端的机器学习工作流。

TensorFlow.js 是一个强大的工具包，用于在浏览器中创建和训练机器学习模型。 Node.js 是一个 JavaScript 运行时，允许您在浏览器之外运行 JavaScript 代码。

这两种技术共同使您能够构建可在任何地方部署的完整机器学习工作流。

## 设置你的环境

在我们深入了解如何构建端到端机器学习工作流的细节之前，让我们花点时间设置我们的开发环境。

您需要在计算机上安装 Node.js 和 npm。您可以在此处找到相关说明：

https://nodejs.org/en/download/

安装 Node.js 和 npm 后，您可以通过运行以下命令安装 TensorFlow.js CLI 工具：

```
npm install -g @tensorflow/tfjs-node
```

## 创建一个新项目

现在我们已经设置了环境，让我们创建一个新项目。我们将从初始化一个新的 npm 项目开始：

```
npm init
```

这将在您的项目目录中创建一个名为“package.json”的文件。此文件包含有关您的项目的信息，包括您的项目所需的依赖项。

接下来，我们将安装项目所需的 TensorFlow.js 和 Node.js 依赖项：

```
npm install @tensorflow/tfjs @tensorflow/tfjs-node
```

## 构建机器学习模型

现在我们已经设置了项目，让我们开始构建我们的机器学习模型。

我们将从在我们的项目目录中创建一个名为“model.js”的文件开始。该文件将包含我们的机器学习模型的代码。

首先，我们需要加载我们将要使用的 TensorFlow.js 和 Node.js 库：

```javascript
const tf = require('@tensorflow/tfjs');
const fs = require('fs');
```

接下来，我们将定义一些用于配置模型的常量：

```javascript
const MODEL_PATH = './model.json';
const INPUT_SHAPE = [28, 28, 1];
const NUM_CLASSES = 10;
```

`MODEL_PATH` 常量定义了包含我们经过训练的模型的文件的路径。 `INPUT_SHAPE` 常量定义我们的模型将要训练的输入数据的形状。 `NUM_CLASSES` 常量定义了我们的模型将被训练来预测的输出类的数量。

接下来，我们将定义一个函数来构建我们的机器学习模型：

```javascript
function buildModel() {
  // We're building a simple machine learning model here
  const model = tf.sequential();
  
  // The first layer of our model is a convolutional layer
  model.add(tf.layers.conv2d({
    inputShape: INPUT_SHAPE,
    kernelSize: 3,
    filters: 16,
    activation: 'relu'
  }));
  
  // The second layer of our model is a pooling layer
  model.add(tf.layers.maxPooling2d({poolSize: 2, strides: 2}));
  
  // The third layer of our model is a flatten layer
  model.add(tf.layers.flatten());
  
  // The fourth layer of our model is a dense layer
  model.add(tf.layers.dense({units: NUM_CLASSES, activation: 'softmax'}));
  
  // We need to compile our model before we can train it
  model.compile({
    optimizer: tf.train.adam(),
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy']
  });
  
  return model;
}
```

该函数定义了一个由四层组成的简单机器学习模型：

- 卷积层
- 池化层
- 扁平层
- 致密层

卷积层负责从输入数据中提取特征。池化层负责对数据进行下采样。展平层负责展平数据。密集层负责将提取的特征映射到输出类。

定义好模型后，我们需要先编译它，然后才能对其进行训练。编译模型配置模型以进行训练。我们需要指定要使用的优化器、损失函数和指标。

在这种情况下，我们使用“adam”优化器、“categoricalCrossentropy”损失函数和“accuracy”指标。

## 训练模型

现在我们已经定义了模型，让我们训练它。我们将从加载训练数据开始。

训练数据存储在 ./data/train.csv 文件中。此文件包含手写数字的 28x28 图像及其标签。

我们将使用 `fs` 模块来读取这个文件的内容：

```javascript
const trainData = fs.readFileSync('./data/train.csv', {encoding: 'utf8'});
```

接下来，我们将把这些数据解析成一个“tf.tensor”数组：

```javascript
const trainTensors = tf.tensor2d(trainData.split('\n').map(row => row.split(',').map(Number)));
```

我们现在已经加载了训练数据并可以使用了。

接下来，我们将定义一个函数来训练我们的模型：

```javascript
async function trainModel(model, trainTensors) {
  // We're training our model for 10 epochs
  const epochs = 10;
  
  // We're using a batch size of 32
  const batchSize = 32;
  
  // We're using the fit method to train our model
  await model.fit(trainTensors, {
    epochs: epochs,
    batchSize: batchSize
  });
}
```

此函数使用 32 的批量大小训练我们的模型 10 个时期。

训练好模型后，我们会将其保存到“MODEL_PATH”文件中：

```javascript
model.save(MODEL_PATH);
```

## 评估模型

现在我们的模型已经训练好了，让我们对其进行评估。我们将从加载测试数据开始。

测试数据存储在 ./data/test.csv 文件中。此文件包含手写数字的 28x28 图像及其标签。

我们将使用 `fs` 模块来读取这个文件的内容：

```javascript
const testData = fs.readFileSync('./data/test.csv', {encoding: 'utf8'});
```

接下来，我们将把这些数据解析成一个“tf.tensor”数组：

```javascript
const testTensors = tf.tensor2d(testData.split('\n').map(row => row.split(',').map(Number)));
```

我们现在已经加载了测试数据并可以使用了。

接下来，我们将定义一个函数来评估我们的模型：

```javascript
async function evaluateModel(model, testTensors) {
  // We're using the evaluate method to evaluate our model
  const results = await model.evaluate(testTensors);
  
  // We're logging the loss and accuracy of our model
  console.log(`loss: ${results[0]} - accuracy: ${results[1]}`);
}
```

此函数根据测试数据评估我们的模型。

## 用模型预测

现在我们的模型已经过训练和评估，让我们用它来进行预测。

我们将从加载要对其进行预测的图像开始。图像存储在 ./data/image.png 文件中。

我们将使用 `fs` 模块来读取这个文件的内容：

```javascript
const imageData = fs.readFileSync('./data/image.png');
```

接下来，我们将把这些数据解析成一个“tf.tensor”：

```javascript
const imageTensor = tf.tensor3d(imageData, [28, 28, 1]);
```

我们现在已经加载了图像数据并可以使用了。

接下来，我们将定义一个函数，该函数将使用我们的模型进行预测：

```javascript
async function predict(model, imageTensor) {
  // We're using the predict method to make a prediction
  const prediction = await model.predict(imageTensor);
  
  // We're logging the prediction that our model made
  console.log(prediction);
}
```

此函数对图像数据进行预测。

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 构建端到端机器学习工作流。

我们已经了解了如何设置开发环境、如何创建新项目、如何构建机器学习模型、如何训练模型、如何评估模型以及如何使用模型进行预测。

如果您有兴趣了解有关 TensorFlow.js 和 Node.js 的更多信息，以下资源可能会对您有所帮助：

- TensorFlow.js 文档：https://js.tensorflow.org/
- Node.js 文档：https://nodejs.org/en/docs/