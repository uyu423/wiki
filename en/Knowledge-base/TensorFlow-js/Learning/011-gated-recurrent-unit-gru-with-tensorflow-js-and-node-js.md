---
title: 011: Gated Recurrent Unit (GRU) with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T09:17:25.284Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:17:20.887Z
---

- [011: Unidad recurrente cerrada (GRU) con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/011-gated-recurrent-unit-gru-with-tensorflow-js-and-node-js)
{.links-list}
- [011：使用 TensorFlow.js 和 Node.js 的门控循环单元 (GRU)***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/011-gated-recurrent-unit-gru-with-tensorflow-js-and-node-js)
{.links-list}
- [011: TensorFlow.js 및 Node.js를 사용하는 GRU(Gated Recurrent Unit)***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/011-gated-recurrent-unit-gru-with-tensorflow-js-and-node-js)
{.links-list}


# Gated Recurrent Unit (GRU) with TensorFlow.js and Node.js

In this post, we'll learn about Gated Recurrent Units (GRUs) and how to implement them with TensorFlow.js and Node.js.

## What are Gated Recurrent Units?

GRUs are a type of recurrent neural network (RNN). RNNs are neural networks that can process sequences of data, such as text, audio, or time series data.

GRUs are a type of RNN that uses gates to control the flow of information in the network. The gates help the network to better learn long-term dependencies.

## Implementing a GRU with TensorFlow.js

We'll use TensorFlow.js to implement a GRU. TensorFlow.js is a JavaScript library for training and deploying machine learning models in the browser and in Node.js.

First, we'll need to install TensorFlow.js. We can do this with the following command:

```
npm install @tensorflow/tfjs
```

Next, we'll need to load the data that we'll be using to train the model. We'll use the MNIST dataset, which is a dataset of handwritten digits.

We can load the MNIST dataset with the following code:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MNIST dataset.
const mnistData = require('mnist-data');

// Convert the MNIST data to a TensorFlow.js tensor.
const mnistTensor = tf.tensor3d(mnistData.images, [mnistData.images.length, 28, 28]);
```

Now that we have the data loaded, we can define the model. We'll use a GRU with 64 units.

```javascript
// Define the model.
const model = tf.sequential();
model.add(tf.layers.gru({units: 64, inputShape: [28, 28]}));
model.add(tf.layers.dense({units: 10, activation: 'softmax'}));
```

Next, we'll need to compile the model. We'll use the Adam optimizer and the categorical crossentropy loss function.

```javascript
// Compile the model.
model.compile({optimizer: 'adam', loss: 'categoricalCrossentropy', metrics: ['accuracy']});
```

Now, we can train the model. We'll train it for 10 epochs.

```javascript
// Train the model.
model.fit(mnistTensor, mnistData.labels, {epochs: 10}).then(() => {
  // The model is trained!
});
```

That's it! We've now trained a GRU to classify handwritten digits.

## Implementing a GRU with Node.js

We can also use Node.js to train a GRU. Node.js is a JavaScript runtime that allows you to run JavaScript code outside of the browser.

First, we'll need to install TensorFlow.js. We can do this with the following command:

```
npm install @tensorflow/tfjs
```

Next, we'll need to load the data that we'll be using to train the model. We'll use the MNIST dataset, which is a dataset of handwritten digits.

We can load the MNIST dataset with the following code:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MNIST dataset.
const mnistData = require('mnist-data');

// Convert the MNIST data to a TensorFlow.js tensor.
const mnistTensor = tf.tensor3d(mnistData.images, [mnistData.images.length, 28, 28]);
```

Now that we have the data loaded, we can define the model. We'll use a GRU with 64 units.

```javascript
// Define the model.
const model = tf.sequential();
model.add(tf.layers.gru({units: 64, inputShape: [28, 28]}));
model.add(tf.layers.dense({units: 10, activation: 'softmax'}));
```

Next, we'll need to compile the model. We'll use the Adam optimizer and the categorical crossentropy loss function.

```javascript
// Compile the model.
model.compile({optimizer: 'adam', loss: 'categoricalCrossentropy', metrics: ['accuracy']});
```

Now, we can train the model. We'll train it for 10 epochs.

```javascript
// Train the model.
model.fit(mnistTensor, mnistData.labels, {epochs: 10}).then(() => {
  // The model is trained!
});
```

That's it! We've now trained a GRU to classify handwritten digits.