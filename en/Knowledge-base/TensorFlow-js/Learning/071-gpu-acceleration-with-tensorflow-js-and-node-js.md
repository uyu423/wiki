---
title: 071: GPU Acceleration with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T20:24:36.696Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:24:31.995Z
---

- [071: aceleración de GPU con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/071-gpu-acceleration-with-tensorflow-js-and-node-js)
{.links-list}
- [071：使用 TensorFlow.js 和 Node.js 进行 GPU 加速***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/071-gpu-acceleration-with-tensorflow-js-and-node-js)
{.links-list}
- [071: TensorFlow.js 및 Node.js를 사용한 GPU 가속***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/071-gpu-acceleration-with-tensorflow-js-and-node-js)
{.links-list}


# GPU Acceleration with TensorFlow.js and Node.js

TensorFlow.js is a powerful and flexible JavaScript library for training and deploying machine learning models. Node.js is a JavaScript runtime that enables server-side scripting and fast network applications.

With TensorFlow.js and Node.js, you can train and deploy machine learning models on the web and on Node.js servers. TensorFlow.js provides a JavaScript API for training and deploying machine learning models on web browsers and Node.js servers. Node.js enables you to run JavaScript on a server.

In this post, we'll show you how to use TensorFlow.js and Node.js to train and deploy machine learning models on the web and on Node.js servers.

## Prerequisites

To follow along with this post, you'll need:

- A computer with a web browser and internet connection
- A text editor
- Node.js installed on your computer

## Installing TensorFlow.js

To install TensorFlow.js, you can use the Node.js package manager (npm):

```
npm install @tensorflow/tfjs
```

## Hello, TensorFlow.js

Let's start by training and deploying a simple machine learning model with TensorFlow.js. We'll use the MNIST dataset, which consists of images of handwritten digits.

First, we'll need to load the MNIST dataset. We can do this with the TensorFlow.js MNIST Dataset class:

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = new tf.MNISTDataset();
```

Next, we'll need to train a machine learning model on the MNIST dataset. We'll use a deep learning model called a convolutional neural network (CNN). A CNN is a type of neural network that is designed to work with images.

We can train a CNN with the TensorFlow.js layers API:

```javascript
const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});
```

Now that we have a machine learning model, we can train it on the MNIST dataset. We'll use the TensorFlow.js fit API to train the model:

```javascript
const trainXs = mnistData.getTrainImagesAsTensors();
const trainYs = mnistData.getTrainLabelsAsTensors();

model.fit(trainXs, trainYs, {
  epochs: 10,
  batchSize: 64
});
```

After the model has been trained, we can evaluate it on the MNIST test dataset. We'll use the TensorFlow.js evaluate API to evaluate the model:

```javascript
const testXs = mnistData.getTestImagesAsTensors();
const testYs = mnistData.getTestLabelsAsTensors();

model.evaluate(testXs, testYs);
```

The evaluate API will return the loss and accuracy of the model on the test dataset.

## Deploying a TensorFlow.js model

Once a machine learning model has been trained, you can deploy it to a web server or a Node.js server.

We'll start by deploying the model to a web server. We can do this with the TensorFlow.js model converter API:

```javascript
const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

const converter = tf.modelConverter.createConverter({
  from: 'tensorflowjs_layers_model'
});

const json = converter.toJSON(model);
```

The model converter API will return a JSON representation of the model. This JSON representation can be used to deploy the model to a web server.

To deploy the model to a web server, you'll need to create a HTML file and a JavaScript file. The HTML file will contain an element that the TensorFlow.js model will be loaded into. The JavaScript file will contain the code to load the model into the element.

Here's an example HTML file:

```html
<html>
  <head>
    <title>TensorFlow.js MNIST Example</title>
  </head>
  <body>
    <h1>TensorFlow.js MNIST Example</h1>
    <div id="container"></div>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs"></script>
    <script src="mnist.js"></script>
  </body>
</html>
```

And here's an example JavaScript file:

```javascript
const tf = require('@tensorflow/tfjs');

const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

const mnistData = new tf.MNISTDataset();

const testXs = mnistData.getTestImagesAsTensors();
const testYs = mnistData.getTestLabelsAsTensors();

model.evaluate(testXs, testYs);

const converter = tf.modelConverter.createConverter({
  from: 'tensorflowjs_layers_model'
});

const json = converter.toJSON(model);

tf.loadLayersModel('http://localhost:8080/model.json').then(function(model) {
  model.predict(testXs).then(function(predictions) {
    console.log(predictions);
  });
});
```

In the HTML file, we've included the TensorFlow.js script and the mnist.js script. The mnist.js script contains the code to load the model into the element with the id "container".

To run the HTML file, you'll need to start a web server. You can use the Node.js http-server module to start a web server:

```
npm install http-server -g

http-server
```

The http-server module will start a web server on port 8080. You can access the HTML file at http://localhost:8080.

## Running a TensorFlow.js model on a Node.js server

You can also run a TensorFlow.js model on a Node.js server. To do this, you'll need to use the TensorFlow.js Node.js API:

```javascript
const tf = require('@tensorflow/tfjs');

const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

const mnistData = new tf.MNISTDataset();

const testXs = mnistData.getTestImagesAsTensors();
const testYs = mnistData.getTestLabelsAsTensors();

model.evaluate(testXs, testYs);

const converter = tf.modelConverter.createConverter({
  from: 'tensorflowjs_layers_model'
});

const json = converter.toJSON(model);

tf.loadLayersModel('http://localhost:8080/model.json').then(function(model) {
  model.predict(testXs).then(function(predictions) {
    console.log(predictions);
  });
});
```

In the code above, we've loaded the MNIST dataset and trained a machine learning model on it. We've then converted the model to a JSON representation and loaded it into a Node.js server.

To run the code above, you'll need to start a Node.js server. You can use the Node.js Express module to start a Node.js server:

```
npm install express -g

express
```

The Express module will start a Node.js server on port 3000. You can access the server at http://localhost:3000.

## Conclusion

In this post, we've shown you how to use TensorFlow.js and Node.js to train and deploy machine learning models on the web and on Node.js servers.

TensorFlow.js is a powerful and flexible JavaScript library for training and deploying machine learning models. Node.js is a JavaScript runtime that enables server-side scripting and fast network applications.

With TensorFlow.js and Node.js, you can train and deploy machine learning models on the web and on Node.js servers. TensorFlow.js provides a JavaScript API for training and deploying machine learning models on web browsers and Node.js servers. Node.js enables you to run JavaScript on a server.