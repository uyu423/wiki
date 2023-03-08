---
title: 094: Building Recurrent Neural Networks (RNNs) in TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-03T05:05:07.459Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:05:02.681Z
---

- [094: Creación de redes neuronales recurrentes (RNN) en TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/094-building-recurrent-neural-networks-rnns-in-tensorflow-js-and-node-js)
{.links-list}
- [094：在 TensorFlow.js 和 Node.js 中构建递归神经网络 (RNN)***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/094-building-recurrent-neural-networks-rnns-in-tensorflow-js-and-node-js)
{.links-list}
- [094: TensorFlow.js 및 Node.js에서 순환 신경망(RNN) 구축***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/094-building-recurrent-neural-networks-rnns-in-tensorflow-js-and-node-js)
{.links-list}


# Introduction

Recurrent neural networks (RNNs) are a type of artificial neural network where connections between nodes form a directed graph along a temporal or spatial sequence. This allows it to exhibit temporal dynamic behavior for a time series or sequence of events.

In this post, we'll be building RNNs in TensorFlow.js and Node.js. TensorFlow.js is an open-source hardware-accelerated machine learning library for the web and JavaScript. Node.js is a cross-platform runtime environment that allows you to write server-side JavaScript code.

We'll be using a dataset of daily stock prices for Apple, Inc. (AAPL) from January 1st, 2013 to December 31st, 2016. The goal is to predict the opening stock price for January 1st, 2017.

# Prerequisites

Before getting started, there are a few things you'll need:

- Basic knowledge of artificial neural networks
- Familiarity with JavaScript
- A text editor
- A web browser

# Getting Started

## Installing TensorFlow.js

To install TensorFlow.js, you can use a package manager like npm or yarn.

```
npm install @tensorflow/tfjs
```

```
yarn add @tensorflow/tfjs
```

Alternatively, you can include the TensorFlow.js library in your HTML file with a script tag.

```html
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.3/dist/tf.min.js"></script>
```

## Installing Node.js

To install Node.js, you can download the installer from the [Node.js website](https://nodejs.org/en/).

## Downloading the Dataset

The dataset we'll be using is available [here](https://www.kaggle.com/camnugent/sandp500). Download the CSV file and save it in the same directory as your JavaScript file.

# Building the RNN

## Loading the Dataset

We'll start by loading the dataset into TensorFlow.js.

```javascript
const tf = require('@tensorflow/tfjs');

const data = tf.loadCSV('AAPL.csv');
```

## Preprocessing the Data

Next, we'll split the data into training and testing sets. We'll also scale the data so that it's between 0 and 1. This is a common preprocessing step for neural networks.

```javascript
const train_data = data.slice(0, data.length - 7);
const test_data = data.slice(data.length - 7);

const train_x = train_data.map(row => row.slice(1, row.length - 1));
const train_y = train_data.map(row => row[row.length - 1]);

const test_x = test_data.map(row => row.slice(1, row.length - 1));
const test_y = test_data.map(row => row[row.length - 1]);

const x_min = Math.min(...train_x.map(row => Math.min(...row)));
const x_max = Math.max(...train_x.map(row => Math.max(...row)));

const y_min = Math.min(...train_y);
const y_max = Math.max(...train_y);

const train_x_scaled = train_x.map(row => row.map(col => (col - x_min) / (x_max - x_min)));
const test_x_scaled = test_x.map(row => row.map(col => (col - x_min) / (x_max - x_min)));

const train_y_scaled = train_y.map(val => (val - y_min) / (y_max - y_min));
const test_y_scaled = test_y.map(val => (val - y_min) / (y_max - y_min));
```

## Building the Model

Now we can build the RNN. We'll start by creating a sequential model.

```javascript
const model = tf.sequential();
```

Next, we'll add a recurrent layer to the model. This layer will have 10 units and an input shape of 1.

```javascript
model.add(tf.layers.simpleRNN({units: 10, inputShape: [1]}));
```

Finally, we'll add a dense layer with a single unit and an output shape of 1. This is the layer that will output the predicted stock price.

```javascript
model.add(tf.layers.dense({units: 1, inputShape: [10]}));
```

## Compiling the Model

Now that we've built the model, we need to compile it before we can train it. We'll use the mean squared error (MSE) as our loss function and the Adam optimizer.

```javascript
model.compile({loss: 'meanSquaredError', optimizer: 'adam'});
```

## Training the Model

We're now ready to train the model. We'll train it for 10 epochs and use a batch size of 1.

```javascript
model.fit(tf.tensor2d(train_x_scaled, [train_x_scaled.length, 1]), tf.tensor2d(train_y_scaled, [train_y_scaled.length, 1]), {
  epochs: 10,
  batchSize: 1
});
```

## Predicting Stock Prices

Now that the model is trained, we can use it to make predictions on the test set.

```javascript
const test_predictions = model.predict(tf.tensor2d(test_x_scaled, [test_x_scaled.length, 1]));
```

## Evaluating the Model

Finally, we can evaluate the model's performance on the test set.

```javascript
const test_loss = tf.losses.meanSquaredError(test_predictions, tf.tensor2d(test_y_scaled, [test_y_scaled.length, 1]));

console.log(test_loss.dataSync());
```

# Conclusion

In this post, we've seen how to build a recurrent neural network in TensorFlow.js and Node.js. We've also seen how to preprocess the data and train the model.

While the model we've built is fairly simple, it can be extended to more complex models. For example, you could add more layers or units to the model, or you could use a different optimizer.

# Resources

- [TensorFlow.js Documentation](https://js.tensorflow.org/)
- [Node.js Documentation](https://nodejs.org/en/docs/)
- [Recurrent neural network](https://en.wikipedia.org/wiki/Recurrent_neural_network)
- [Stock market prediction using recurrent neural networks](https://t.co/GbU6XfjlbO?amp=1)