---
title: 037: Custom Model Metrics with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T13:57:30.431Z
tags: 
editor: markdown
dateCreated: 2023-02-02T13:57:25.913Z
---

- [037: Métricas de modelos personalizados con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/037-custom-model-metrics-with-tensorflow-js-and-node-js)
{.links-list}
- [037：使用 TensorFlow.js 和 Node.js 自定义模型指标***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/037-custom-model-metrics-with-tensorflow-js-and-node-js)
{.links-list}
- [037: TensorFlow.js 및 Node.js를 사용한 사용자 정의 모델 측정항목***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/037-custom-model-metrics-with-tensorflow-js-and-node-js)
{.links-list}


# 037: Custom Model Metrics with TensorFlow.js and Node.js

In this post, we'll learn how to define custom model metrics in TensorFlow.js and Node.js.

## What are custom model metrics?

Custom model metrics are functions that take in two arguments:

- `yTrue`: The ground truth values.
- `yPred`: The predicted values.

And return a single value that represents the metric.

For example, we might want to define a custom metric that calculates the mean squared error (MSE) between the ground truth values and the predicted values. We can do this by defining the following function:

```javascript
function mse(yTrue, yPred) {
  // ...
}
```

## Defining custom model metrics in TensorFlow.js

In TensorFlow.js, we can define custom model metrics by creating a `CustomCallback` and passing it to the `fit` method.

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

In the code above, we've defined a `CustomCallback` that calculates the `mse` metric. We've then passed this callback to the `fit` method, which tells the model to calculate the `mse` metric during training.

## Defining custom model metrics in Node.js

In Node.js, we can define custom model metrics by creating a `tf.Metrics` instance and passing it to the `fit` method.

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

In the code above, we've created a `tf.Metrics` instance that calculates the `mse` metric. We've then passed this instance to the `fit` method, which tells the model to calculate the `mse` metric during training.

## Conclusion

In this post, we've learned how to define custom model metrics in TensorFlow.js and Node.js.