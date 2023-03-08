---
title: 027：使用 TensorFlow.js 和 Node.js 进行异常检测
description: 
published: true
date: 2023-02-02T13:17:49.049Z
tags: 
editor: markdown
dateCreated: 2023-02-02T13:17:47.452Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [027: Anomaly Detection with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/027-anomaly-detection-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 进行异常检测

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 构建异常检测模型。我们将使用过去 140 年的每日温度读数数据集，我们将其分为训练集和测试集。

我们将使用 TensorFlow.js 库来构建和训练我们的模型。 TensorFlow.js 是一个用于训练和部署机器学习模型的 JavaScript 库。 Node.js 是一个 JavaScript 运行时，它允许我们在浏览器之外运行 JavaScript 代码。

我们将使用来自 TensorFlow.js 的顺序模型 API。顺序模型是一种由线性堆叠层组成的神经网络。

## 先决条件

在我们开始之前，您需要做一些事情：

- 文本编辑器。我推荐 [Visual Studio Code](https://code.visualstudio.com/)。
- [Node.js](https://nodejs.org/en/) 安装在您的计算机上。
- 对 JavaScript 有基本的了解。

## 获取数据

第一步是获取数据。我们将使用过去 140 年的每日温度读数数据集。数据集可在 [此处](https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data) 获得。

下载数据集并解压缩。您现在应该有一个名为“GlobalLandTemperaturesByCountry”的文件夹。

## 准备数据

下一步是准备数据。我们需要将数据集拆分为训练集和测试集。我们还需要规范化数据，这意味着缩放数据，使其介于 0 和 1 之间。

我们将使用 [`normalize-dataset`](https://www.npmjs.com/package/normalize-dataset) 包来帮助我们解决这个问题。通过运行以下命令安装它：

```
npm install --save normalize-dataset
```

创建一个名为 `prepare-data.js` 的新文件并添加以下代码：

```javascript
const fs = require('fs');
const path = require('path');
const normalizeDataset = require('normalize-dataset');

const dataPath = path.join(__dirname, 'GlobalLandTemperaturesByCountry.csv');
const data = fs.readFileSync(dataPath, 'utf8');

// Split the data into training and testing sets
const [train, test] = normalizeDataset.splitDataset(data, 0.8);

// Save the training and testing sets to files
fs.writeFileSync(path.join(__dirname, 'train.csv'), train);
fs.writeFileSync(path.join(__dirname, 'test.csv'), test);
```

通过运行以下命令来运行代码：

```
node prepare-data.js
```

现在，您的项目中应该有两个新文件：`train.csv` 和 `test.csv`。这些是我们将用来训练和测试我们的模型的训练和测试集。

## 构建模型

现在我们有了数据，可以开始构建模型了。我们将使用来自 TensorFlow.js 的顺序模型 API。顺序模型是一种由线性堆叠层组成的神经网络。

创建一个名为“model.js”的新文件并添加以下代码：

```javascript
const tf = require('@tensorflow/tfjs');

// Create a sequential model
const model = tf.sequential();

// Add a single hidden layer
model.add(tf.layers.dense({ units: 1, inputShape: [1] }));

// Add an output layer
model.add(tf.layers.dense({ units: 1, activation: 'sigmoid' }));

// Compile the model
model.compile({
  loss: 'binaryCrossentropy',
  optimizer: 'adam'
});

module.exports = model;
```

在上面的代码中，我们创建了一个具有一个隐藏层和一个输出层的顺序模型。我们还使用 `binaryCrossentropy` 损失函数和 `adam` 优化器编译了模型。

## 训练模型

现在我们有了模型，我们需要训练它。我们将通过为模型提供我们之前准备的训练集来做到这一点。

创建一个名为“train.js”的新文件并添加以下代码：

```javascript
const tf = require('@tensorflow/tfjs');
const fs = require('fs');
const path = require('path');

const model = require('./model');

// Read the training set from a file
const trainPath = path.join(__dirname, 'train.csv');
const trainData = tf.data.csv(trainPath, {
  columnConfigs: {
    label: {
      isLabel: true
    }
  }
});

// Train the model
model.fitDataset(trainData, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    }
  }
});
```

在上面的代码中，我们从文件中读取了训练集并将其传递给 fitDataset 函数。此函数将训练模型 10 个时期。一个时期是对整个训练集的一次迭代。

我们还配置了 `onEpochEnd` 回调来记录每个纪元后的损失。损失是衡量模型执行情况的指标。我们希望损失尽可能低。

## 测试模型

现在我们已经训练了我们的模型，我们需要测试它。我们将通过为模型提供我们之前准备的测试集来做到这一点。

创建一个名为 `test.js` 的新文件并添加以下代码：

```javascript
const tf = require('@tensorflow/tfjs');
const fs = require('fs');
const path = require('path');

const model = require('./model');

// Read the testing set from a file
const testPath = path.join(__dirname, 'test.csv');
const testData = tf.data.csv(testPath, {
  columnConfigs: {
    label: {
      isLabel: true
    }
  }
});

// Evaluate the model
model.evaluateDataset(testData).then(results => {
  console.log(`Loss: ${results.loss}`);
});
```

在上面的代码中，我们从文件中读取了测试集并将其传递给“evaluateDataset”函数。此函数将评估模型并返回损失。

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 构建异常检测模型。我们已经准备好数据，构建了模型，并对模型进行了训练和测试。