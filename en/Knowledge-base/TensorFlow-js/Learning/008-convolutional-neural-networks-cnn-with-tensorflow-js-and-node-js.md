---
title: 008: Convolutional Neural Networks (CNN) with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T08:37:01.005Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:36:59.310Z
---

- [008: Redes neuronales convolucionales (CNN) con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/008-convolutional-neural-networks-cnn-with-tensorflow-js-and-node-js)
{.links-list}
- [008：使用 TensorFlow.js 和 Node.js 的卷积神经网络 (CNN)***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/008-convolutional-neural-networks-cnn-with-tensorflow-js-and-node-js)
{.links-list}
- [008: TensorFlow.js 및 Node.js를 사용한 CNN(컨볼루션 신경망)***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/008-convolutional-neural-networks-cnn-with-tensorflow-js-and-node-js)
{.links-list}


# Introduction

In this post, we'll be looking at how to build convolutional neural networks (CNNs) in TensorFlow.js and Node.js. We'll be using a well-known dataset for image recognition, the MNIST dataset, to train our CNN.

Convolutional neural networks are a type of neural network that are particularly well-suited for image recognition tasks. This is because they are able to take advantage of the spatial structure of images.

# Building a CNN in TensorFlow.js

We'll start by looking at how to build a CNN in TensorFlow.js. If you're not familiar with TensorFlow.js, it's a JavaScript library for machine learning that runs in the browser.

First, we need to load the MNIST dataset. The MNIST dataset is a collection of images of handwritten digits, each of which is 28x28 pixels.

We can load the MNIST dataset using TensorFlow.js's `tf.data.mnist` function. This function returns a `Dataset` object, which we can then use to train our CNN.

```javascript
const mnistData = tf.data.mnist({
  train: true,
  testData: false
});
```

Next, we need to define the convolutional neural network. We'll be using a Sequential model, which is a type of neural network that is composed of a linear stack of layers.

We'll start by adding a `Flatten` layer, which takes our 28x28 images and flattens them into a single vector of 784 elements.

```javascript
const model = tf.sequential();

model.add(tf.layers.flatten({
  inputShape: [28, 28]
}));
```

Next, we'll add a `Dense` layer. This is a fully-connected layer, which means that each neuron in the layer is connected to every neuron in the previous layer.

We'll configure the `Dense` layer to have 128 neurons and to use the `relu` activation function. The `relu` activation function is a common choice for neural networks. It outputs 0 for any input less than 0 and outputs the input for any input greater than or equal to 0.

```javascript
model.add(tf.layers.dense({
  units: 128,
  activation: 'relu',
  inputShape: [784]
}));
```

Finally, we'll add a `Dense` layer with 10 neurons and the `softmax` activation function. The `softmax` activation function is a common choice for the output layer of a neural network. It outputs a probability distribution over the 10 possible digits.

```javascript
model.add(tf.layers.dense({
  units: 10,
  activation: 'softmax',
  inputShape: [128]
}));
```

Now that we've defined our model, we need to compile it. When we compile a model, we specify the loss function and the optimizer.

The loss function is a measure of how well the model is performing. We want to minimize the loss function, which means that we want the model to make predictions that are as close to the true labels as possible.

The optimizer is a algorithm that is used to update the model in order to minimize the loss function. There are many different optimizers available, but we'll be using the `sgd` optimizer.

```javascript
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'sgd'
});
```

Now that our model is compiled, we can train it. We'll train it for 10 epochs, which means that the model will see the entire MNIST dataset 10 times.

```javascript
model.fit(mnistData, {
  epochs: 10
});
```

# Building a CNN in Node.js

Now that we've seen how to build a CNN in TensorFlow.js, let's take a look at how to do it in Node.js.

First, we need to load the MNIST dataset. The MNIST dataset is a collection of images of handwritten digits, each of which is 28x28 pixels.

We can load the MNIST dataset using the `mnist` package. This package returns a `Dataset` object, which we can then use to train our CNN.

```javascript
const mnist = require('mnist');

const mnistData = mnist.training(0, 60000);
```

Next, we need to define the convolutional neural network. We'll be using a Sequential model, which is a type of neural network that is composed of a linear stack of layers.

We'll start by adding a `Flatten` layer, which takes our 28x28 images and flattens them into a single vector of 784 elements.

```javascript
const model = tf.sequential();

model.add(tf.layers.flatten({
  inputShape: [28, 28]
}));
```

Next, we'll add a `Dense` layer. This is a fully-connected layer, which means that each neuron in the layer is connected to every neuron in the previous layer.

We'll configure the `Dense` layer to have 128 neurons and to use the `relu` activation function. The `relu` activation function is a common choice for neural networks. It outputs 0 for any input less than 0 and outputs the input for any input greater than or equal to 0.

```javascript
model.add(tf.layers.dense({
  units: 128,
  activation: 'relu',
  inputShape: [784]
}));
```

Finally, we'll add a `Dense` layer with 10 neurons and the `softmax` activation function. The `softmax` activation function is a common choice for the output layer of a neural network. It outputs a probability distribution over the 10 possible digits.

```javascript
model.add(tf.layers.dense({
  units: 10,
  activation: 'softmax',
  inputShape: [128]
}));
```

Now that we've defined our model, we need to compile it. When we compile a model, we specify the loss function and the optimizer.

The loss function is a measure of how well the model is performing. We want to minimize the loss function, which means that we want the model to make predictions that are as close to the true labels as possible.

The optimizer is a algorithm that is used to update the model in order to minimize the loss function. There are many different optimizers available, but we'll be using the `sgd` optimizer.

```javascript
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'sgd'
});
```

Now that our model is compiled, we can train it. We'll train it for 10 epochs, which means that the model will see the entire MNIST dataset 10 times.

```javascript
model.fit(mnistData, {
  epochs: 10
});
```

# Conclusion

In this post, we've seen how to build convolutional neural networks in TensorFlow.js and Node.js. We've also seen how to train these networks on the MNIST dataset.