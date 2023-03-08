---
title: 042：使用 TensorFlow.js 和 Node.js 进行超参数调优
description: 
published: true
date: 2023-02-02T16:44:18.750Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:44:14.180Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [042: Hyperparameter Tuning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/042-hyperparameter-tuning-with-tensorflow-js-and-node-js)
{.links-list}


# 042：使用 TensorFlow.js 和 Node.js 进行超参数调优

在本文中，我们将学习如何使用 TensorFlow.js 和 Node.js 进行超参数调整。

超参数调整是通过为模型的超参数选择最佳值来优化机器学习模型的过程。超参数调整的目标是找到使模型在未见数据上获得最佳性能的超参数值。

有几种不同的方法来调整超参数。一种流行的方法是网格搜索，它涉及通过尝试所有可能的值组合来详尽地搜索超参数的最佳值。

另一种流行的方法是贝叶斯优化，它使用概率模型来指导搜索超参数的最佳值。

在这篇文章中，我们将使用 TensorFlow.js 和 Node.js 来实现一个使用贝叶斯优化的简单超参数调整实验。

## 先决条件

在我们开始之前，您需要做一些事情才能跟进：

- 对机器学习及其工作原理有基本的了解
- 文本编辑器或 IDE
- Node.js 安装在你的机器上

## 入门

我们将从创建一个新的 Node.js 项目开始。为您的项目创建一个新目录并使用 npm 对其进行初始化：

```
mkdir hyperparameter-tuning
cd hyperparameter-tuning
npm init -y
```

接下来，我们将安装项目所需的依赖项。我们需要 [ BayesOptimization ](https://www.npmjs.com/package/bayesopt) 和 [ TensorFlow.js ](https://www.npmjs.com/package/@tensorflow/tfjs) 包：

```
npm install --save bayesopt @tensorflow/tfjs
```

安装依赖项后，我们现在可以创建项目文件。在您的项目目录中创建一个名为“index.js”的文件并添加以下代码：

```javascript
const tf = require('@tensorflow/tfjs');
const BayesOptimization = require('bayesopt');

// TODO: implement our hyperparameter tuning experiment
```

我们将从要求我们安装的依赖项开始。我们还将创建一个 TODO 注释来提醒我们需要在哪里实施超参数调整实验。

## 实现超参数调优实验

现在我们已经设置了项目，我们可以开始实施我们的超参数调整实验。

我们将从定义要优化的参数开始。对于这个实验，我们将优化简单线性回归模型的学习率和批量大小。我们还将定义要搜索每个参数的值范围：

```javascript
const params = {
  learningRate: {
    type: 'float',
    min: 0.0001,
    max: 0.1
  },
  batchSize: {
    type: 'int',
    min: 1,
    max: 100
  }
};
```

接下来，我们将定义我们的目标函数。这是我们将要优化的功能。在这种情况下，我们想要找到导致验证集错误率最低的超参数值：

```javascript
const objective = (params, done) => {
  // TODO: implement our objective function
};
```

我们稍后会实现我们的目标函数。现在，我们只需要定义它。

定义了参数和目标函数后，我们现在可以创建贝叶斯优化对象：

```javascript
const bo = new BayesOptimization(params, objective);
```

我们现在可以开始优化我们的目标函数。我们将运行优化 20 次迭代并使用默认采集函数（预期改进）：

```javascript
bo.optimize(20, (err, result) => {
  if (err) {
    console.error(err);
  } else {
    console.log(result);
  }
});
```

我们现在可以实现我们的目标函数。我们将从加载 [波士顿住房数据集 ](https://archive.ics.uci.edu/ml/datasets/Housing) 并将其拆分为训练集和验证集开始：

```javascript
const loadData = () =>
  tf.data.csv('https://archive.ics.uci.edu/ml/machine-learning-databases/housing/housing.data', {
    columnConfigs: {
      medv: {
        isLabel: true
      }
    }
  });

const splitData = (data) =>
  data.shuffle().splitBatch(0.2);
```

接下来，我们将定义我们的线性回归模型：

```javascript
const createModel = () =>
  tf.sequential({
    layers: [
      tf.layers.dense({ inputShape: [13], units: 1 })
    ]
  });
```

现在我们可以实现我们的目标函数了。我们将从 params 对象获取超参数的值开始：

```javascript
const objective = (params, done) => {
  const learningRate = params.learningRate;
  const batchSize = params.batchSize;
  // TODO: implement our objective function
};
```

接下来，我们将加载数据并将其拆分为训练集和验证集：

```javascript
const objective = (params, done) => {
  const learningRate = params.learningRate;
  const batchSize = params.batchSize;

  loadData()
    .then(splitData)
    .then(([train, val]) => {
      // TODO: implement our objective function
    });
};
```

现在我们可以创建我们的模型并使用我们正在优化的超参数对其进行编译：

```javascript
const objective = (params, done) => {
  const learningRate = params.learningRate;
  const batchSize = params.batchSize;

  loadData()
    .then(splitData)
    .then(([train, val]) => {
      const model = createModel();
      model.compile({
        loss: 'meanSquaredError',
        optimizer: tf.train.sgd(learningRate)
      });
      // TODO: implement our objective function
    });
};
```

最后，我们可以训练我们的模型并在验证集上对其进行评估。我们将计算验证集的均方误差并将其作为目标函数的值返回：

```javascript
const objective = (params, done) => {
  const learningRate = params.learningRate;
  const batchSize = params.batchSize;

  loadData()
    .then(splitData)
    .then(([train, val]) => {
      const model = createModel();
      model.compile({
        loss: 'meanSquaredError',
        optimizer: tf.train.sgd(learningRate)
      });

      model.fit(train, {
        epochs: 10,
        batchSize: batchSize,
        validationData: val,
        callbacks: {
          onEpochEnd: (epoch, logs) => {
            console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
          }
        }
      })
        .then(() => {
          const valLoss = model.evaluate(val);
          console.log(`Validation loss: ${valLoss}`);
          done(null, valLoss);
        });
    });
};
```

就是这样！我们现在已经使用 TensorFlow.js 和 Node.js 实现了一个简单的超参数调整实验。

## 结论

在本文中，我们学习了如何使用 TensorFlow.js 和 Node.js 进行超参数调整。我们已经使用贝叶斯优化实现了一个简单的超参数调整实验。

超参数调整的内容比我们在这篇文章中介绍的要多得多。如果您有兴趣了解更多信息，我建议您查看以下资源：

- [机器学习中的超参数优化](https://towardsdatascience.com/hyperparameter-optimization-in-machine-learning-part-1-of-4-cca2b1c265a2)
- [超参数调整的贝叶斯方法](https://towardsdatascience.com/a-bayesian-approach-to-hyperparameter-tuning-part-1-of-3-c8f8e527e97b)
- [使用 TensorFlow 进行超参数调整](https://medium.com/tensorflow/hyperparameter-tuning-with-tensorflow-part-1-fae4f2bae5e1)