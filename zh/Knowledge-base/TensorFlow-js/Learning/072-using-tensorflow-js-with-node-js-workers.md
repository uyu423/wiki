---
title: 072：将 TensorFlow.js 与 Node.js Worker 结合使用
description: 
published: true
date: 2023-02-02T23:37:03.512Z
tags: 
editor: markdown
dateCreated: 2023-02-02T23:37:01.829Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [072: Using TensorFlow.js with Node.js Workers***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/072-using-tensorflow-js-with-node-js-workers)
{.links-list}


# 将 TensorFlow.js 与 Node.js Workers 结合使用

TensorFlow.js 是一个强大的 JavaScript 机器学习工具，Node.js Workers 提供了一种利用多核系统并保持主事件循环平稳运行的好方法。

在本文中，我们将了解如何使用 TensorFlow.js 和 Node.js Worker 来训练机器学习模型。我们将从一个简单的示例开始，让一切正常运行，然后我们将看一个更复杂的示例，展示如何使用工作池并行训练多个模型。

## TensorFlow.js 和 Workers 入门

首先，我们需要安装 TensorFlow.js 和 @tensorflow/tfjs-node Worker 插件。我们可以用 npm 做到这一点：

```
npm install @tensorflow/tfjs @tensorflow/tfjs-node
```

一旦我们安装了 TensorFlow.js 和 Worker 插件，我们就可以开始编写一些代码了。

我们将从训练一个简单的模型开始，对 MNIST 数据集中的手写数字进行分类。首先，我们需要加载数据集：

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MNIST dataset
const mnistData = tf.data.web('https://storage.googleapis.com/tfjs-examples/mnist_train_small.csv');
```

接下来，我们将定义一个函数来将数据集转换为 TensorFlow.js 可以理解的格式。此函数将采用数字数组并返回 TensorFlow.js 张量：

```javascript
// Convert the dataset into a format that TensorFlow.js can understand
const convertToTensor = (data) => {
  // Wrapping this in a tidy will dispose the tensor when we're done
  return tf.tidy(() => {
    // Convert the data to a TensorFlow.js tensor
    const tensor = tf.tensor2d(data, [data.length, 784]);
    
    // Normalize the data
    return tensor.div(tf.scalar(255));
  });
};
```

加载数据集并定义转换函数后，我们就可以训练模型了。我们将定义一个具有两个密集层的简单顺序模型：

```javascript
// Define a simple sequential model
const model = tf.sequential();
model.add(tf.layers.dense({ units: 784, activation: 'relu', inputShape: [784] }));
model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));
```

接下来，我们将使用 Adam 优化器和分类交叉熵损失函数编译模型：

```javascript
// Compile the model
model.compile({
  optimizer: tf.train.adam(),
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy'],
});
```

现在我们准备好训练模型了。我们将使用 fitDataset() 方法，它接受一个 tf.data.Dataset 对象并在数据集上训练模型：

```javascript
// Train the model
model.fitDataset(mnistData, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      console.log(`Epoch ${epoch}: loss = ${logs.loss}, accuracy = ${logs.acc}`);
    },
  },
});
```

就是这样！我们现在已经使用 TensorFlow.js 和 Node.js Workers 训练了一个简单的机器学习模型。

## 并行训练多个模型

在上一节中，我们了解了如何将 TensorFlow.js 与 Node.js Workers 结合使用来训练单个模型。但是，Node.js Worker 也可用于并行训练多个模型。

为此，我们首先需要创建一个工作池。我们可以使用 tf.js-node Worker 插件来做到这一点：

```javascript
const { WorkerPool } = require('@tensorflow/tfjs-node');

// Create a Worker pool with two workers
const pool = new WorkerPool({ numWorkers: 2 });
```

一旦我们有了一个工作池，我们就可以定义一个函数来在数据集上训练模型。这个函数将接受一个数据集和一个模型，它会返回一个解析为训练模型的 Promise：

```javascript
// Define a function to train a model on a dataset
const trainModel = (dataset, model) => {
  return new Promise((resolve, reject) => {
    // Use a tidy to clean up when we're done
    tf.tidy(() => {
      // Train the model
      model.fitDataset(dataset, {
        epochs: 10,
        callbacks: {
          onEpochEnd: (epoch, logs) => {
            console.log(`Epoch ${epoch}: loss = ${logs.loss}, accuracy = ${logs.acc}`);
          },
        },
      })
      .then(() => {
        // Resolve the promise with the trained model
        resolve(model);
      })
      .catch((err) => {
        // Reject the promise with the error
        reject(err);
      });
    });
  });
};
```

定义了 trainModel() 函数后，我们现在可以并行训练多个模型。我们将通过将 trainModel() 函数映射到一组数据集来完成此操作：

```javascript
// Create an array of datasets
const datasets = [
  tf.data.web('https://storage.googleapis.com/tfjs-examples/mnist_train_small.csv'),
  tf.data.web('https://storage.googleapis.com/tfjs-examples/mnist_test.csv'),
];

// Train multiple models in parallel
Promise.all(datasets.map((dataset) => {
  return trainModel(dataset, model);
}))
.then(() => {
  // All models have been trained
  console.log('All models have been trained');
})
.catch((err) => {
  // One or more models failed to train
  console.error(err);
});
```

在此代码中，我们使用 Promise.all() 方法并行训练多个模型。 Promise.all() 方法接受一个 Promise 数组，并返回一个 Promise，该 Promise 在数组中的所有 Promise 都已解析时解析。

## 包起来

在本文中，我们了解了如何将 TensorFlow.js 与 Node.js Workers 结合使用来训练机器学习模型。我们已经从一个简单的示例开始，并且了解了如何使用 Worker 池并行训练多个模型。

如果您有兴趣了解有关 TensorFlow.js 的更多信息，请务必查看 TensorFlow.js 网站 (https://js.tensorflow.org/) 和 TensorFlow.js 示例 (https://github.com/张量流/tfjs 示例）。