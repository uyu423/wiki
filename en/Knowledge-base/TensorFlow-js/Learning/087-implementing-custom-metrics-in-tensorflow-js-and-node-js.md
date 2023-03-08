---
title: 087: Implementing Custom Metrics in TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-03T03:17:29.830Z
tags: 
editor: markdown
dateCreated: 2023-02-03T03:17:25.104Z
---

- [087: Implementación de métricas personalizadas en TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/087-implementing-custom-metrics-in-tensorflow-js-and-node-js)
{.links-list}
- [087：在 TensorFlow.js 和 Node.js 中实现自定义指标***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/087-implementing-custom-metrics-in-tensorflow-js-and-node-js)
{.links-list}
- [087: TensorFlow.js 및 Node.js에서 맞춤 측정항목 구현***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/087-implementing-custom-metrics-in-tensorflow-js-and-node-js)
{.links-list}


# Implementing Custom Metrics in TensorFlow.js and Node.js

In this post, we'll learn how to implement custom metrics in TensorFlow.js and Node.js.

## What are custom metrics?

Custom metrics are user-defined metrics that can be used to track the performance of a machine learning model. They can be used to track anything from the model's accuracy to the number of training iterations.

## Why use custom metrics?

Custom metrics can be used to track the performance of a machine learning model in a more granular way than the built-in metrics. They can also be used to track the performance of a model over multiple training runs.

## How to implement custom metrics in TensorFlow.js?

TensorFlow.js provides a CustomCallback class that can be used to implement custom metrics. The CustomCallback class takes a function as an argument. This function takes two arguments:

- The first argument is the current batch of data.
- The second argument is the current epoch.

The function should return an object with the metric name and metric value.

Here's an example of how to use the CustomCallback class to track the accuracy of a machine learning model:

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

In this example, we've defined a custom metric to track the accuracy of the model. The CustomCallback class will call the function we've defined at the end of each epoch. The function will evaluate the model on the current batch of data and return the accuracy.

## How to implement custom metrics in Node.js?

Node.js provides a similar functionality to TensorFlow.js with the use of the async/await keywords.

Here's an example of how to use async/await to track the accuracy of a machine learning model:

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

In this example, we've defined a custom metric to track the accuracy of the model. The async/await keywords will call the function we've defined at the end of each epoch. The function will evaluate the model on the current batch of data and return the accuracy.