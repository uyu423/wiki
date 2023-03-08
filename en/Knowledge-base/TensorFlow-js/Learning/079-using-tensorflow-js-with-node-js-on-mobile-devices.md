---
title: 079: Using TensorFlow.js with Node.js on Mobile Devices
description: 
published: true
date: 2023-02-03T01:17:44.955Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:17:40.287Z
---

- [079: Uso de TensorFlow.js con Node.js en dispositivos móviles***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/079-using-tensorflow-js-with-node-js-on-mobile-devices)
{.links-list}
- [079：在移动设备上使用 TensorFlow.js 和 Node.js***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/079-using-tensorflow-js-with-node-js-on-mobile-devices)
{.links-list}
- [079: 모바일 장치에서 Node.js와 함께 TensorFlow.js 사용***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/079-using-tensorflow-js-with-node-js-on-mobile-devices)
{.links-list}


## Introduction

TensorFlow.js is an open-source library that can be used to develop and train machine learning models in the browser or on a Node.js server. In this post, we'll focus on using TensorFlow.js with Node.js on mobile devices.

TensorFlow.js offers many benefits over traditional server-side machine learning frameworks, such as increased flexibility and portability. Mobile devices are often resource-constrained, so being able to run machine learning models on-device is a huge advantage.

## Setting up the environment

Before we get started, we need to set up our development environment. We'll need to install Node.js and the TensorFlow.js library.

Node.js can be downloaded and installed from the official website (https://nodejs.org/en/). Once Node.js is installed, we can use the Node Package Manager (npm) to install TensorFlow.js.

```
npm install @tensorflow/tfjs
```

## Hello, TensorFlow.js!

Now that we have our environment set up, let's write our first TensorFlow.js program!

```javascript
// Load the TensorFlow.js library
const tf = require('@tensorflow/tfjs');

// Define a TensorFlow.js model
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));

// Compile the model
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

// Fit the model to the data
const xs = tf.tensor2d([-1.0, 0.0, 1.0, 2.0, 3.0, 4.0], [6, 1]);
const ys = tf.tensor2d([-3.0, -1.0, 1.0, 3.0, 5.0, 7.0], [6, 1]);

model.fit(xs, ys, {epochs: 500}).then(() => {
  // Use the model to predict the output of a new Tensor
  model.predict(tf.tensor2d([5], [1, 1])).print();
});
```

In this program, we first load the TensorFlow.js library using the require() function. We then define a sequential model using the tf.sequential() function.

Next, we add a dense layer to the model using the tf.layers.dense() function. This layer has one unit and expects an input of size one.

After adding the layer, we compile the model using the tf.compile() function. We specify that we want to use the mean squared error loss function and the stochastic gradient descent optimizer.

Finally, we fit the model to the data using the tf.fit() function. We specify that we want to run 500 training epochs.

Once the model is trained, we use the tf.predict() function to predict the output of a new Tensor. In this case, we predict the output for the Tensor [5].

## Running TensorFlow.js on a mobile device

Now that we've seen how to write a TensorFlow.js program, let's see how we can run it on a mobile device.

There are two ways to run TensorFlow.js on a mobile device: using the web browser or using a native app.

If we want to use the web browser, we need to make sure that our TensorFlow.js program is running on a web server. We can use any web server, but for this example, we'll use Node.js.

First, we need to install the http-server npm package.

```
npm install http-server
```

Once the http-server package is installed, we can use it to start a web server from the command line.

```
http-server
```

This will start a web server on port 8080. We can now access our TensorFlow.js program by going to http://localhost:8080 in our web browser.

If we want to use a native app, we need to use a platform-specific TensorFlow.js library. For iOS, we can use the TensorFlow Lite Swift library (https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/swift). For Android, we can use the TensorFlow Lite Android library (https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/android).

## Conclusion

In this post, we've seen how to use TensorFlow.js with Node.js on mobile devices. TensorFlow.js offers many benefits over traditional server-side machine learning frameworks, such as increased flexibility and portability. Mobile devices are often resource-constrained, so being able to run machine learning models on-device is a huge advantage.