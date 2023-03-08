---
title: 048: Adadelta Optimization with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T18:17:49.406Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:17:47.725Z
---

- [048: Optimización Adadelta con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/048-adadelta-optimization-with-tensorflow-js-and-node-js)
{.links-list}
- [048：使用 TensorFlow.js 和 Node.js 优化 Adadelta***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/048-adadelta-optimization-with-tensorflow-js-and-node-js)
{.links-list}
- [048: TensorFlow.js 및 Node.js를 사용한 Adadelta 최적화***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/048-adadelta-optimization-with-tensorflow-js-and-node-js)
{.links-list}


# Adadelta Optimization with TensorFlow.js and Node.js

Adadelta is an optimization algorithm that can be used instead of traditional stochastic gradient descent (SGD) to train deep neural networks. It is a more robust and efficient method of training neural networks, and can be used with TensorFlow.js and Node.js.

## What is Adadelta?

Adadelta is an adaptive learning rate optimization algorithm that is well suited for training deep neural networks. It was proposed in 2012 by Matthew D. Zeiler and Rob Fergus in the paper "[ADADELTA: An Adaptive Learning Rate Method](https://arxiv.org/abs/1212.5701)," which won the Best Paper Award at the International Conference on Learning Representations (ICLR) in 2013.

Adadelta is an extension of Adagrad, another adaptive learning rate optimization algorithm that was proposed in 2011 by Duchi et al. in the paper "[Adaptive Subgradient Methods for Online Learning and Stochastic Optimization](https://www.jmlr.org/papers/volume12/duchi11a/duchi11a.pdf)."

Both Adagrad and Adadelta are based on the concept of per-parameter learning rates, which are adapted based on the gradient of the loss function with respect to the parameters.

## How Does Adadelta Work?

The Adadelta optimization algorithm works by calculating the per-parameter learning rate for each parameter in the neural network. The learning rate is adapted based on the gradient of the loss function with respect to the parameters.

The algorithm has two parameters:

-   `rho`: A parameter that controls the decay rate of the learning rate. A value of `0.95` is typically used.
-   `epsilon`: A small parameter that is used for numerical stability. A value of `1e-6` is typically used.

The Adadelta optimization algorithm can be summarized as follows:

1.  Initialize the per-parameter learning rates `Delta_p` to `0`.
2.  For each training example `x` and corresponding target `y`:
    1.  Calculate the gradient of the loss function with respect to the parameters `Delta_p = gradient(loss(x, y), p)`.
    2.  Update the per-parameter learning rates: `Delta_p = rho * Delta_p + (1 - rho) * Delta_p^2`.
    3.  Update the parameters: `p = p - learning_rate * Delta_p / sqrt(epsilon + accumulated_gradients)`.

## Adadelta vs. SGD

Adadelta is a more robust and efficient method of training neural networks than traditional stochastic gradient descent (SGD).

SGD is a popular optimization algorithm for training neural networks, but it can be difficult to tune the learning rate. If the learning rate is too low, the training process will be slow. If the learning rate is too high, the training process may diverge.

Adadelta does not require a learning rate to be specified. The learning rate is automatically adapted based on the gradient of the loss function. This makes it more robust and efficient than SGD.

## Adadelta with TensorFlow.js and Node.js

Adadelta can be used with TensorFlow.js and Node.js.

TensorFlow.js is a JavaScript library for training and deploying machine learning models. Node.js is a JavaScript runtime that can be used to run TensorFlow.js applications.

To use Adadelta with TensorFlow.js and Node.js, you need to install the `tensorflow` and `@tensorflow/tfjs-node` modules.

```
$ npm install --save tensorflow
$ npm install --save @tensorflow/tfjs-node
```

Then, you can use the `tf.train.adadelta` function to train a neural network using the Adadelta optimization algorithm.

```javascript
const tf = require('tensorflow');

// Define the neural network.
const model = tf.sequential();
model.add(tf.layers.dense({ units: 10, inputShape: [5], activation: 'relu' }));
model.add(tf.layers.dense({ units: 1, activation: 'sigmoid' }));

// Compile the model.
model.compile({
  loss: 'binaryCrossentropy',
  optimizer: tf.train.adadelta(),
  metrics: ['accuracy']
});

// Train the model.
model.fit({ x: tf.ones([100, 5]), y: tf.zeros([100]) }, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    }
  }
});
```

## Conclusion

In this post, we have seen how to use the Adadelta optimization algorithm with TensorFlow.js and Node.js. Adadelta is a more robust and efficient method of training neural networks than traditional stochastic gradient descent (SGD).