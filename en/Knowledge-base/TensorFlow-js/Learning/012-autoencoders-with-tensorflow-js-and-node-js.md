---
title: 012: Autoencoders with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T09:36:43.204Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:36:38.733Z
---

- [012: Codificadores automáticos con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/012-autoencoders-with-tensorflow-js-and-node-js)
{.links-list}
- [012：使用 TensorFlow.js 和 Node.js 的自动编码器***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/012-autoencoders-with-tensorflow-js-and-node-js)
{.links-list}
- [012: TensorFlow.js 및 Node.js를 사용한 자동 인코더***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/012-autoencoders-with-tensorflow-js-and-node-js)
{.links-list}


# Autoencoders with TensorFlow.js and Node.js

Deep learning is a powerful tool for learning complex representations of data. An autoencoder is a type of neural network that can be used to learn these representations in an unsupervised manner.

In this post, we'll be using TensorFlow.js and Node.js to build a simple autoencoder. We'll be using the MNIST dataset, which consists of images of handwritten digits.

## Getting Started

First, we need to install the dependencies. We'll be using the following libraries:

* [TensorFlow.js](https://www.tensorflow.org/js)
* [mnist](https://www.npmjs.com/package/mnist)

You can install them using npm:

```
npm install tensorflowjs mnist
```

Next, we need to load the MNIST dataset. We'll be using the mnist library to do this:

```javascript
const mnist = require('mnist');

// Load the dataset
const dataset = mnist.set(0.7, 0.3);

// Get the training and test sets
const [train, test] = dataset.getTrainingAndTestSets();
```

The MNIST dataset consists of images of handwritten digits, each of which is 28x28 pixels. We'll need to flatten these images into vectors of size 784 before we can use them as input to our autoencoder.

```javascript
// Flatten the images into vectors
const trainX = train.map(example => example.input);
const testX = test.map(example => example.input);
```

## Building the Autoencoder

Now that we have the dataset, we can start building the autoencoder. We'll be using a fully-connected neural network with one hidden layer. The hidden layer will have a smaller number of units than the input layer, which will force the network to learn a compressed representation of the data.

```javascript
// Create the model
const model = tf.sequential();

// Add the input layer
model.add(tf.layers.dense({
  inputShape: [784],
  units: 64
}));

// Add the hidden layer
model.add(tf.layers.dense({
  units: 32
}));

// Add the output layer
model.add(tf.layers.dense({
  units: 784
}));
```

We need to specify an optimizer and a loss function for the model. We'll be using the Adam optimizer and the Mean Squared Error (MSE) loss function.

```javascript
// Compile the model
model.compile({
  optimizer: 'adam',
  loss: 'meanSquaredError'
});
```

## Training the Autoencoder

Now that we have the model, we can train it on the training set. We'll train the model for 20 epochs.

```javascript
// Train the model
model.fit(tf.tensor2d(trainX), tf.tensor2d(trainX), {
  epochs: 20
}).then(() => {
  // Evaluate the model on the test set
  model.evaluate(tf.tensor2d(testX), tf.tensor2d(testX));
});
```

## Visualizing the Results

To visualize the results of the training, we can use the `tensorflow-vis` library to plot the reconstructed images.

```javascript
// Install the library
npm install @tensorflow/tfjs-vis

// Load the library
const tfvis = require('@tensorflow/tfjs-vis');

// Plot the results
tfvis.show.image3d(
  model.predict(tf.tensor2d(testX)),
  {
    width: 28,
    height: 28
  }
);
```

## Conclusion

In this post, we've seen how to use TensorFlow.js and Node.js to build a simple autoencoder. We've also seen how to train the autoencoder and visualize the results.

Autoencoders can be used for a variety of tasks, such as dimensionality reduction, denoising, and generative modeling. If you're interested in learning more about autoencoders, I recommend the following resources:

* [Deep Learning 101 – Introduction to Autoencoders](https://towardsdatascience.com/deep-learning-101-introduction-to-autoencoders-3e44bffe2b7d)
* [Autoencoders](http://cs.stanford.edu/people/karpathy/convnetjs/demo/autoencoder.html)
* [Variational Autoencoders](https://jmetzen.github.io/2015-11-27/vae.html)