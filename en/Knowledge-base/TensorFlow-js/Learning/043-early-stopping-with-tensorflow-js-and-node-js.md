---
title: 043: Early Stopping with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T17:04:38.644Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:04:37.006Z
---

- [043: Detención anticipada con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/043-early-stopping-with-tensorflow-js-and-node-js)
{.links-list}
- [043：使用 TensorFlow.js 和 Node.js 提前停止***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/043-early-stopping-with-tensorflow-js-and-node-js)
{.links-list}
- [043: TensorFlow.js 및 Node.js로 조기 중지***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/043-early-stopping-with-tensorflow-js-and-node-js)
{.links-list}


# Early Stopping with TensorFlow.js and Node.js

Deep learning is a neural network technique that has revolutionized many fields, including computer vision, natural language processing, and predictive modeling. TensorFlow.js is a powerful open-source library for training and deploying deep learning models in JavaScript.

In this post, we'll learn how to use TensorFlow.js and Node.js to implement early stopping, a technique for training neural networks that can help prevent overfitting.

## What is early stopping?

Early stopping is a technique for training neural networks that can help prevent overfitting. Overfitting occurs when a model is trained on a dataset that is too small or too simple, and the model begins to learn patterns that are specific to that dataset. This can cause the model to perform poorly on new data.

Early stopping is a way to combat overfitting by stopping the training process before the model has a chance to learn these patterns. We can do this by monitoring the performance of the model on a validation set, and stopping the training process when the performance on the validation set begins to decline.

## Implementing early stopping with TensorFlow.js

We'll start by creating a simple neural network using TensorFlow.js. This network will take two input values and predict a third, continuous output value. We'll train it on a dataset of 100 points.

```javascript
const tf = require('@tensorflow/tfjs');

// Create a neural network with two input nodes,
// one hidden layer with two nodes, and one output node
const model = tf.sequential();
model.add(tf.layers.dense({units: 2, inputShape: [2]}));
model.add(tf.layers.dense({units: 1}));

// Compile the model
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

// Generate some synthetic data for training
const xs = tf.tensor2d([[0, 0], [0, 1], [1, 0], [1, 1]]);
const ys = tf.tensor2d([[0], [1], [1], [0]]);

// Train the model
model.fit(xs, ys, {
  epochs: 100,
  validationData: [xs, ys],
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    }
  }
});
```

Next, we'll add a callback that will stop the training process when the loss on the validation set begins to increase. We'll do this by keeping track of the loss at each epoch, and comparing the loss at the current epoch to the loss at the previous epoch. If the loss has increased, we'll stop the training process.

```javascript
let previousLoss;

model.fit(xs, ys, {
  epochs: 100,
  validationData: [xs, ys],
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);

      if (previousLoss && log.loss > previousLoss) {
        model.stopTraining = true;
      }
      previousLoss = log.loss;
    }
  }
});
```

## Try it out

You can [try out this code for yourself](https://jsfiddle.net/jimmykim/9h5b7eLp/).

## Additional information

- [TensorFlow.js](https://js.tensorflow.org/)
- [Node.js](https://nodejs.org/en/)

## Resources for further reading

- [Overfitting and Underfitting with TensorFlow.js](https://js.tensorflow.org/tutorials/overfitting_and_underfitting.html)
- [Early Stopping](https://machinelearningmastery.com/how-to-avoid-overfitting-with-early-stopping/)