---
title: 005：使用 TensorFlow.js 和 Node.js 进行线性回归
description: 
published: true
date: 2023-02-02T07:43:33.535Z
tags: 
editor: markdown
dateCreated: 2023-02-02T07:43:31.955Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [005: Linear Regression with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/005-linear-regression-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 进行线性回归

在本文中，我们将学习如何使用 TensorFlow.js 和 Node.js 执行线性回归。我们将从简要回顾线性回归开始，然后我们将了解如何使用 TensorFlow.js 实现它。

## 什么是线性回归？

线性回归是一种统计技术，用于模拟因变量与一个或多个自变量之间的关系。因变量是被预测的变量，而自变量是用于预测因变量的变量。

在线性回归模型中，因变量是自变量的线性函数。也就是说，因变量是自变量的线性函数。

## 如何使用 TensorFlow.js 执行线性回归？

TensorFlow.js 是一个用于训练和部署机器学习模型的 JavaScript 库。它也用于数值计算。在本节中，我们将了解如何使用 TensorFlow.js 进行线性回归。

我们将使用以下数据作为线性回归示例：

| × |是 |
|---|---|
| 1 | 2 |
| 2 | 4 |
| 3 | 6 |

第一步是导入 TensorFlow.js 库。我们可以使用 require() 函数来做到这一点：

```javascript
const tf = require('@tensorflow/tfjs');
```

接下来，我们需要定义自变量和因变量。我们可以使用 tf.tensor() 函数来做到这一点：

```javascript
// Define the independent variable
const x = tf.tensor([1, 2, 3], [3, 1]);

// Define the dependent variable
const y = tf.tensor([2, 4, 6], [3, 1]);
```

现在我们已经定义了自变量和因变量，我们可以定义线性回归模型了。我们可以使用 tf.layers.dense() 函数来做到这一点：

```javascript
// Define the linear regression model
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));
```

下一步是编译线性回归模型。我们可以使用 tf.model.compile() 函数来做到这一点：

```javascript
// Compile the linear regression model
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});
```

最后，我们可以训练线性回归模型。我们可以使用 tf.model.fit() 函数来做到这一点：

```javascript
// Train the linear regression model
model.fit(x, y, {epochs: 100}).then(() => {
  // Use the model to predict the value of y for x = 4
  model.predict(tf.tensor([4], [1, 1])).print();
});
```

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 执行线性回归。我们还看到了如何使用线性回归模型来预测给定自变量的因变量值。