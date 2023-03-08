---
title: 050：使用 TensorFlow.js 和 Node.js 进行 Adam 优化
description: 
published: true
date: 2023-02-02T18:36:28.002Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:36:26.411Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [050: Adam Optimization with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/050-adam-optimization-with-tensorflow-js-and-node-js)
{.links-list}


# Adam 使用 TensorFlow.js 和 Node.js 进行优化

在本文中，我们将探讨如何将 Adam 优化算法与 TensorFlow.js 和 Node.js 结合使用。 Adam 是一种可用于训练神经网络的优化算法。 Adam 是 AdaGrad 和 RMSProp 优化算法的组合。

Adam 优化是一种计算效率高的神经网络训练方法。 Adam 非常适合训练深度神经网络。 Adam 可以与任何可微损失函数一起使用。

## 入门

首先，我们需要安装 TensorFlow.js 和 Node.js 依赖项。我们可以使用以下命令安装 TensorFlow.js 和 Node.js：

```
npm install @tensorflow/tfjs
npm install node
```

## 定义模型

接下来，我们需要定义要训练的模型。我们将使用一个带有一个隐藏层的简单神经网络。隐藏层将有 100 个神经元。我们可以使用以下代码定义模型：

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({units: 100, inputShape: [1], activation: 'relu'}));
model.add(tf.layers.dense({units: 1, activation: 'linear'}));
```

## 编译模型

定义模型后，我们需要编译它。编译模型允许我们指定我们想要使用的优化器和损失函数。我们将使用 Adam 优化器和均方误差损失函数。我们可以使用以下代码编译模型：

```javascript
model.compile({optimizer: 'adam', loss: 'meanSquaredError'});
```

## 训练模型

现在我们已经编译了模型，我们可以训练它了。我们将训练模型 10 个时期。一个时期是对整个训练数据集的一次迭代。我们可以使用以下代码训练模型：

```javascript
model.fit(x, y, {epochs: 10});
```

## 评估模型

模型训练好后，我们可以对其进行评估。我们将在测试数据集上评估模型。我们可以使用以下代码评估模型：

```javascript
model.evaluate(xTest, yTest);
```

## 做出预测

最后，我们可以使用训练好的模型进行预测。我们将对新数据集进行预测。我们可以使用以下代码进行预测：

```javascript
model.predict(xPred);
```

## 结论

在本文中，我们了解了如何将 Adam 优化算法与 TensorFlow.js 和 Node.js 结合使用。 Adam 是一种高效的优化算法，可用于训练神经网络。 Adam 可以与任何可微损失函数一起使用。