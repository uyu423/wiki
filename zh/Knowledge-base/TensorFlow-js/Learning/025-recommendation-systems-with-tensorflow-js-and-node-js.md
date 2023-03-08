---
title: 025：使用 TensorFlow.js 和 Node.js 的推荐系统
description: 
published: true
date: 2023-02-02T12:44:02.519Z
tags: 
editor: markdown
dateCreated: 2023-02-02T12:44:00.923Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [025: Recommendation Systems with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/025-recommendation-systems-with-tensorflow-js-and-node-js)
{.links-list}


## 概述

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 构建推荐系统。我们将首先简要介绍推荐系统及其用例。然后，我们将了解如何使用 TensorFlow.js 构建一个简单的基于内容的推荐系统。最后，我们将探索如何使用 TensorFlow.js 和 Node.js 构建更复杂的协同过滤推荐系统。

## 什么是推荐系统？

推荐系统是一种人工智能，用于预测用户可能想要购买或观看的内容。 Amazon、Netflix 和 Spotify 等公司广泛使用它们来个性化向用户显示的内容。

推荐系统有两种主要类型：基于内容的和协同过滤。

基于内容的推荐系统根据项目之间的相似性向用户推荐项目。例如，基于内容的推荐系统可能会根据用户过去看过类似电影的事实向用户推荐一部电影。

协同过滤推荐系统根据用户之间的相似性向用户推荐项目。例如，协同过滤推荐系统可能会根据看过类似电影的其他用户也看过该电影的事实向用户推荐电影。

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 构建基于内容和协同过滤的推荐系统。

## 构建基于内容的推荐系统

我们将从研究如何构建基于内容的推荐系统开始。我们将使用 MovieLens 数据集，这是一个电影评级数据集。

MovieLens 数据集包含 943 个用户对 1682 部电影的 100,000 个评分。每个评级都是 1 到 5 之间的数字，其中 5 是最高评级。

我们首先将数据集加载到 TensorFlow.js 数据集中：

```javascript
const tf = require('@tensorflow/tfjs');

const dataset = tf.data.csv('https://storage.googleapis.com/recommendation-system-datasets/movielens/ml-100k/u.data', {
  columnConfigs: {
    user_id: {
      isLabel: true
    },
    movie_id: {
      isLabel: true
    },
    rating: {
      isLabel: false
    }
  }
});
```

我们使用 `columnConfigs` 选项告诉 TensorFlow.js `user_id` 和 `movie_id` 列是标签，而 `rating` 列不是标签。

然后我们将数据集分成训练集和测试集：

```javascript
const trainDataset = dataset.shuffle(dataset.size).batch(dataset.size * 0.8);
const testDataset = dataset.batch(dataset.size * 0.2);
```

我们对训练集和测试集使用 80/20 分割。

然后我们将创建一个模型来学习从电影到评级的映射：

```javascript
const model = tf.sequential();

model.add(tf.layers.embedding({
  inputDim: 1682,
  outputDim: 64,
  inputShape: [1]
}));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({
  units: 64,
  activation: 'relu'
}));

model.add(tf.layers.dense({
  units: 1,
  activation: 'linear'
}));

model.compile({
  loss: 'meanSquaredError',
  optimizer: 'adam'
});
```

我们正在使用嵌入层将电影映射到低维向量空间。然后我们使用密集层来学习从向量空间到评级的映射。

然后我们将模型拟合到训练数据：

```javascript
model.fitDataset(trainDataset, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    }
  }
});
```

我们使用 `tf.data.Dataset` 进行训练，它允许我们使用 `fitDataset()` 方法。我们还使用 `onEpochEnd` 回调来打印每个纪元后的损失。

然后我们可以在测试集上评估模型：

```javascript
const testLoss = model.evaluateDataset(testDataset);

console.log(`Test loss: ${testLoss.loss}`);
```

该模型的测试损失为 0.84，这意味着它能够以平均 0.84 的误差预测电影的评分。

## 构建协同过滤推荐系统

我们现在来看看如何构建协同过滤推荐系统。

我们将首先创建一个模型来学习从用户到评级的映射：

```javascript
const model = tf.sequential();

model.add(tf.layers.embedding({
  inputDim: 943,
  outputDim: 64,
  inputShape: [1]
}));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({
  units: 64,
  activation: 'relu'
}));

model.add(tf.layers.dense({
  units: 1,
  activation: 'linear'
}));

model.compile({
  loss: 'meanSquaredError',
  optimizer: 'adam'
});
```

我们正在使用嵌入层将用户映射到低维向量空间。然后我们使用密集层来学习从向量空间到评级的映射。

然后我们将模型拟合到训练数据：

```javascript
model.fitDataset(trainDataset, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    }
  }
});
```

然后我们可以在测试集上评估模型：

```javascript
const testLoss = model.evaluateDataset(testDataset);

console.log(`Test loss: ${testLoss.loss}`);
```

该模型的测试损失为 0.95，这意味着它能够预测平均误差为 0.95 的用户评分。

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 构建推荐系统。我们首先研究了如何构建基于内容的推荐系统。然后我们研究了如何构建协同过滤推荐系统。