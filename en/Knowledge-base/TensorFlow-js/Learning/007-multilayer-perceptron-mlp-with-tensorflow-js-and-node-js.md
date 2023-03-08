---
title: 007: Multilayer Perceptron (MLP) with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T08:17:35.383Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:17:30.981Z
---

- [007: Perceptrón multicapa (MLP) con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/007-multilayer-perceptron-mlp-with-tensorflow-js-and-node-js)
{.links-list}
- [007：使用 TensorFlow.js 和 Node.js 的多层感知器 (MLP)***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/007-multilayer-perceptron-mlp-with-tensorflow-js-and-node-js)
{.links-list}
- [007: TensorFlow.js 및 Node.js를 사용한 다층 퍼셉트론(MLP)***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/007-multilayer-perceptron-mlp-with-tensorflow-js-and-node-js)
{.links-list}


## Introduction

In this post, we'll be covering how to build a multilayer perceptron (MLP) with TensorFlow.js and Node.js. We'll go over the fundamental concepts behind neural networks and deep learning, and how to implement them using TensorFlow.js. By the end of this post, you'll be able to build your own neural networks and use them to solve real-world problems.

## What is a multilayer perceptron?

A multilayer perceptron (MLP) is a type of neural network. Neural networks are a type of machine learning algorithm that are used to model complex patterns in data. MLPs are a specific type of neural network that are composed of multiple layers of neurons.

The first layer of an MLP is the input layer, which takes in the input data. The second layer is the hidden layer, which transforms the input data into a new representation. The hidden layer is followed by the output layer, which produces the output of the MLP.

## Building an MLP with TensorFlow.js

TensorFlow.js is a JavaScript library for building neural networks and machine learning models. It can be used in both the browser and in Node.js.

In order to use TensorFlow.js, we first need to install it. We can do this using the Node Package Manager (NPM):

```
npm install @tensorflow/tfjs
```

Once TensorFlow.js is installed, we can import it into our project:

```javascript
const tf = require('@tensorflow/tfjs');
```

Now that we have TensorFlow.js installed and imported, we can start building our MLP.

The first step is to define the input layer. We can do this using the `input` function:

```javascript
const inputLayer = tf.input({shape: [2]});
```

The `input` function takes an object as an argument. The `shape` property of this object defines the shape of the input data. In this case, we're using a two-dimensional input, so the `shape` property is set to `[2]`.

Next, we need to define the hidden layer. We can do this using the `layers` function:

```javascript
const hiddenLayer = tf.layers.dense({
  units: 4,
  activation: 'sigmoid',
  inputShape: [2]
});
```

The `layers` function takes an object as an argument. The `units` property defines the number of neurons in the layer. The `activation` property defines the activation function of the layer. In this case, we're using the sigmoid activation function. The `inputShape` property defines the shape of the input data.

Finally, we need to define the output layer. We can do this using the `layers` function:

```javascript
const outputLayer = tf.layers.dense({
  units: 1,
  activation: 'sigmoid',
  inputShape: [4]
});
```

As with the hidden layer, the `units` property defines the number of neurons in the layer. The `activation` property defines the activation function of the layer. In this case, we're again using the sigmoid activation function. The `inputShape` property defines the shape of the input data.

Now that we've defined the layers of our MLP, we need to connect them. We can do this using the `sequential` function:

```javascript
const model = tf.sequential();
```

The `sequential` function takes an array of layers as an argument. In this case, we're passing in our input layer, hidden layer, and output layer.

Now that our model is defined, we need to compile it. We can do this using the `compile` function:

```javascript
model.compile({
  optimizer: 'sgd',
  loss: 'meanSquaredError'
});
```

The `compile` function takes an object as an argument. The `optimizer` property defines the optimizer that will be used to train the model. In this case, we're using the stochastic gradient descent (SGD) optimizer. The `loss` property defines the loss function that will be used to evaluate the model. In this case, we're using the mean squared error (MSE) loss function.

Now that our model is compiled, we can train it. We can do this using the `fit` function:

```javascript
model.fit(x, y, {
  epochs: 100,
  batchSize: 32
});
```

The `fit` function takes three arguments: the training data (`x`), the target data (`y`), and an object specifying the training parameters. The `epochs` property defines the number of training epochs. The `batchSize` property defines the number of samples in each training batch.

Once the model is trained, we can use it to make predictions. We can do this using the `predict` function:

```javascript
model.predict(x).print();
```

The `predict` function takes an array of input data (`x`) and returns an array of predictions. The `print` function prints the predictions to the console.

## Conclusion

In this post, we covered how to build a multilayer perceptron (MLP) with TensorFlow.js and Node.js. We went over the fundamental concepts behind neural networks and deep learning, and how to implement them using TensorFlow.js. By the end of this post, you should be able to build your own neural networks and use them to solve real-world problems.