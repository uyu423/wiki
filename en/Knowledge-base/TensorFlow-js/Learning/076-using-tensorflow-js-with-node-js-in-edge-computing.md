---
title: 076: Using TensorFlow.js with Node.js in Edge Computing
description: 
published: true
date: 2023-02-03T00:38:00.744Z
tags: 
editor: markdown
dateCreated: 2023-02-03T00:37:55.802Z
---

- [076: Uso de TensorFlow.js con Node.js en Edge Computing***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/076-using-tensorflow-js-with-node-js-in-edge-computing)
{.links-list}
- [076：在边缘计算中使用 TensorFlow.js 和 Node.js***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/076-using-tensorflow-js-with-node-js-in-edge-computing)
{.links-list}
- [076: Edge Computing에서 TensorFlow.js를 Node.js와 함께 사용***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/076-using-tensorflow-js-with-node-js-in-edge-computing)
{.links-list}


# Using TensorFlow.js with Node.js in Edge Computing

TensorFlow.js is an open-source library for numerical computation using data flow graphs. It can be used in Node.js for training and deploying machine learning models on edge devices.

In this post, we'll go over how to use TensorFlow.js with Node.js for training and deploying machine learning models on edge devices.

## What is TensorFlow.js?

TensorFlow.js is an open-source library for numerical computation using data flow graphs. TensorFlow.js is a JavaScript library for training and deploying machine learning models in the browser and on Node.js.

TensorFlow.js was originally developed by the Google Brain team for use with the TensorFlow machine learning platform.

## What is Node.js?

Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js is an open-source, cross-platform runtime environment for developing server-side applications.

Node.js applications are written in JavaScript and can be run within the Node.js runtime on OS X, Microsoft Windows, Linux, and FreeBSD.

## Getting Started

In order to use TensorFlow.js with Node.js, you'll need to install the following:

- Node.js
- TensorFlow.js

You can install Node.js and TensorFlow.js using the following commands:

```
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
```

```
npm install @tensorflow/tfjs
```

## Hello World

Let's start by creating a simple "Hello World" program using TensorFlow.js and Node.js.

Create a file named "hello-world.js" and add the following code:

```javascript
const tf = require('@tensorflow/tfjs');

tf.tensor([1, 2, 3, 4]).print();
```

Run the program using the following command:

```
node hello-world.js
```

You should see the following output:

```
Tensor
    [[1],
     [2],
     [3],
     [4]]
```

## Training a Machine Learning Model

Now that we've seen how to use TensorFlow.js with Node.js, let's try training a simple machine learning model.

We'll be using the MNIST dataset, which consists of 70,000 grayscale images of handwritten digits. The images are 28x28 pixels in size.

The MNIST dataset is split into three parts: 60,000 images for training, 10,000 images for testing, and 10,000 images for validation.

We'll be using the TensorFlow.js layers API to build our machine learning model. The layers API is a high-level API that makes it easy to construct neural networks.

First, we'll need to load the MNIST dataset. We can do this using the tf.data API.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();
}

run();
```

Next, we'll define our machine learning model using the tf.sequential API.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });
}

run();
```

Now that we've defined our machine learning model, we need to train it. We can do this using the tf.fit API.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  return model.fit(images, labels, {
    batchSize,
    epochs
  });
}

run();
```

Once our machine learning model is trained, we can use it to make predictions on new data.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  model.fit(images, labels, {
    batchSize,
    epochs
  });

  const testImages = images.slice(0, 1000);
  const testLabels = labels.slice(0, 1000);

  const accuracy = model.evaluate(testImages, testLabels);

  console.log('Accuracy:', accuracy[1]);
}

run();
```

## Deploying a Machine Learning Model

Once we've trained our machine learning model, we can deploy it to an edge device for inference.

We'll be using the TensorFlow.js Node.js API to deploy our machine learning model to an edge device. The Node.js API is a low-level API that allows you to run TensorFlow.js programs on Node.js.

First, we'll need to convert our machine learning model to the TensorFlow.js Node.js format. We can do this using the tf.node.save API.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  model.fit(images, labels, {
    batchSize,
    epochs
  });

  tf.node.save(model, 'model.json');
}

run();
```

Once our machine learning model is converted to the TensorFlow.js Node.js format, we can deploy it to an edge device.

We'll need to install the TensorFlow.js Node.js API on our edge device. We can do this using the following command:

```
npm install @tensorflow/tfjs-node
```

Now that the TensorFlow.js Node.js API is installed, we can use the tf.node.load API to load our machine learning model.

```javascript
const tf = require('@tensorflow/tfjs-node');

async function run() {
  const model = await tf.node.load('model.json');
}

run();
```

Once our machine learning model is loaded, we can use it to make predictions on new data.

```javascript
const tf = require('@tensorflow/tfjs-node');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  model.fit(images, labels, {
    batchSize,
    epochs
  });

  tf.node.save(model, 'model.json');

  const testImages = images.slice(0, 1000);
  const testLabels = labels.slice(0, 1000);

  const accuracy = model.evaluate(testImages, testLabels);

  console.log('Accuracy:', accuracy[1]);
}

run();
```

## Conclusion

In this post, we've seen how to use TensorFlow.js with Node.js for training and deploying machine learning models on edge devices.

TensorFlow.js is a powerful library for numerical computation that can be used to train and deploy machine learning models on edge devices.

Node.js is a JavaScript runtime that can be used to run TensorFlow.js programs on edge devices.

The TensorFlow.js Node.js API is a low-level API that allows you to run TensorFlow.js programs on Node.js.

## Resources

- [TensorFlow.js](https://js.tensorflow.org/)
- [Node.js](https://nodejs.org/en/)
- [ MNIST Dataset](http://yann.lecun.com/exdb/mnist/)