---
title: 087：在 TensorFlow.js 和 Node.js 中实现自定义指标
description: 
published: true
date: 2023-02-03T03:17:26.714Z
tags: 
editor: markdown
dateCreated: 2023-02-03T03:17:25.102Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [087: Implementing Custom Metrics in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/087-implementing-custom-metrics-in-tensorflow-js-and-node-js)
{.links-list}


# 在 TensorFlow.js 和 Node.js 中实现自定义指标

在本文中，我们将学习如何在 TensorFlow.js 和 Node.js 中实现自定义指标。

## 什么是自定义指标？

自定义指标是用户定义的指标，可用于跟踪机器学习模型的性能。它们可用于跟踪从模型的准确性到训练迭代次数的任何事情。

## 为什么要使用自定义指标？

自定义指标可用于以比内置指标更精细的方式跟踪机器学习模型的性能。它们还可用于跟踪模型在多次训练运行中的性能。

## 如何在 TensorFlow.js 中实现自定义指标？

TensorFlow.js 提供了一个 CustomCallback 类，可用于实现自定义指标。 CustomCallback 类将一个函数作为参数。这个函数有两个参数：

- 第一个参数是当前批次的数据。
- 第二个参数是当前纪元。

该函数应返回一个具有度量名称和度量值的对象。

下面是一个示例，说明如何使用 CustomCallback 类来跟踪机器学习模型的准确性：

```javascript
const model = tf.sequential();

model.add(tf.layers.dense({units: 100, activation: 'relu', inputShape: [784]}));
model.add(tf.layers.dense({units: 10, activation: 'softmax'}));

model.compile({
  optimizer: 'sgd',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});

const callback = tf.callbacks.CustomCallback((batch, epoch) => {
  const acc = model.evaluate(batch.x, batch.y)[1].dataSync()[0];
  console.log('Accuracy: ', acc);
  return {'accuracy': acc};
});

model.fit(x, y, {
  epochs: 10,
  callbacks: [callback]
});
```

在此示例中，我们定义了一个自定义指标来跟踪模型的准确性。 CustomCallback 类将调用我们在每个纪元结束时定义的函数。该函数将评估当前批次数据的模型并返回准确性。

## 如何在 Node.js 中实现自定义指标？

Node.js 通过使用 async/await 关键字提供与 TensorFlow.js 类似的功能。

下面是一个如何使用 async/await 来跟踪机器学习模型准确性的示例：

```javascript
const model = tf.sequential();

model.add(tf.layers.dense({units: 100, activation: 'relu', inputShape: [784]}));
model.add(tf.layers.dense({units: 10, activation: 'softmax'}));

model.compile({
  optimizer: 'sgd',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});

async function run() {
  for (let i = 0; i < 10; i++) {
    const res = await model.fit(x, y);
    console.log('Accuracy: ', res.history.acc);
  }
}

run();
```

在此示例中，我们定义了一个自定义指标来跟踪模型的准确性。 async/await 关键字将调用我们在每个 epoch 结束时定义的函数。该函数将评估当前批次数据的模型并返回准确性。