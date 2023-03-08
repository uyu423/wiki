---
title: 032: Deploying TensorFlow.js Models with Node.js
description: 
published: true
date: 2023-02-02T14:36:49.469Z
tags: 
editor: markdown
dateCreated: 2023-02-02T14:36:44.827Z
---

- [032: Implementación de modelos de TensorFlow.js con Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/032-deploying-tensorflow-js-models-with-node-js)
{.links-list}
- [032：使用 Node.js 部署 TensorFlow.js 模型***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/032-deploying-tensorflow-js-models-with-node-js)
{.links-list}
- [032: Node.js로 TensorFlow.js 모델 배포***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/032-deploying-tensorflow-js-models-with-node-js)
{.links-list}


# 032: Deploying TensorFlow.js Models with Node.js

TensorFlow.js is an open-source JavaScript library for machine learning that enables developers to train and deploy ML models in the browser or in Node.js.

In this post, we'll learn how to use TensorFlow.js to deploy a pre-trained ML model in a Node.js application. We'll also learn how to use the Node.js API to run inference on the model.

## Prerequisites

Before getting started, you'll need the following:

* Node.js
* A text editor
* A web browser

## Getting Started

First, we need to install the TensorFlow.js library. We can do this using the Node Package Manager (NPM):

```
npm install @tensorflow/tfjs
```

Next, we need to download the pre-trained ML model. For this example, we'll use the [MobileNet](https://github.com/tensorflow/tfjs-models/tree/master/mobilenet) image classification model.

Once the model is downloaded, we can deploy it in our Node.js application.

## Deploying the Model

To deploy the model, we need to create a new file called `index.js`. In this file, we'll use the `tf.loadModel()` function to load the pre-trained model:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
  });
```

## Using the Model

Once the model is loaded, we can use it to run inference on an image. For this example, we'll use the [TensorFlow.js image classification example](https://github.com/tensorflow/tfjs-examples/tree/master/image-classification).

First, we need to load the image into a `tf.Tensor`:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
    const img = tf.tensor3d(imageData, [224, 224, 3]);
  });
```

Next, we need to pre-process the image using the `mobilenet.preprocessInput()` function:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
    const img = tf.tensor3d(imageData, [224, 224, 3]);

    // Pre-process the image.
    const preprocessedImg = tf.mobilenet.preprocessInput(img);
  });
```

Finally, we can use the `model.predict()` function to run inference on the image:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
    const img = tf.tensor3d(imageData, [224, 224, 3]);

    // Pre-process the image.
    const preprocessedImg = tf.mobilenet.preprocessInput(img);

    // Run inference.
    model.predict(preprocessedImg).then(predictions => {
      // Use the predictions.
    });
  });
```

The `predictions` variable contains the results of the inference.

## Conclusion

In this post, we learned how to use TensorFlow.js to deploy a pre-trained ML model in a Node.js application. We also learned how to use the Node.js API to run inference on the model.