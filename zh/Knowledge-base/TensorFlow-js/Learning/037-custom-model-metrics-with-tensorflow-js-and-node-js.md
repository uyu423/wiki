---
title: 037：使用 TensorFlow.js 和 Node.js 自定义模型指标
description: 
published: true
date: 2023-02-02T13:57:27.451Z
tags: 
editor: markdown
dateCreated: 2023-02-02T13:57:25.906Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [037: Custom Model Metrics with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/037-custom-model-metrics-with-tensorflow-js-and-node-js)
{.links-list}


# 037：使用 TensorFlow.js 和 Node.js 自定义模型指标

在本文中，我们将学习如何在 TensorFlow.js 和 Node.js 中定义自定义模型指标。

## 什么是自定义模型指标？

自定义模型指标是接受两个参数的函数：

- `yTrue`：基本事实值。
- `yPred`：预测值。

并返回表示指标的单个值。

例如，我们可能想要定义一个自定义指标来计算真实值和预测值之间的均方误差 (MSE)。我们可以通过定义以下函数来做到这一点：

```javascript
function mse(yTrue, yPred) {
  // ...
}
```

## 在 TensorFlow.js 中定义自定义模型指标

在 TensorFlow.js 中，我们可以通过创建“CustomCallback”并将其传递给“fit”方法来定义自定义模型指标。

```javascript
const model = tf.sequential();
// ...

model.compile({
  // ...
  metrics: ['mse']
});

model.fit(x, y, {
  epochs: 10,
  callbacks: tf.callbacks.customCallback(['mse'], (logs) => {
    console.log(logs.mse);
  })
});
```

在上面的代码中，我们定义了一个计算“mse”指标的“CustomCallback”。然后我们将此回调传递给“fit”方法，该方法告诉模型在训练期间计算“mse”指标。

## 在 Node.js 中定义自定义模型指标

在 Node.js 中，我们可以通过创建一个“tf.Metrics”实例并将其传递给“fit”方法来定义自定义模型指标。

```javascript
const model = tf.sequential();
// ...

model.compile({
  // ...
  metrics: ['mse']
});

const metrics = new tf.Metrics(['mse']);

model.fit(x, y, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      metrics.update(logs);
    }
  }
});

metrics.print();
```

在上面的代码中，我们创建了一个计算“mse”指标的“tf.Metrics”实例。然后我们将此实例传递给“fit”方法，该方法告诉模型在训练期间计算“mse”指标。

## 结论

在本文中，我们学习了如何在 TensorFlow.js 和 Node.js 中定义自定义模型指标。