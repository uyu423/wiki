---
title: 061: Real-Time Object Detection with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T21:17:48.286Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:17:43.580Z
---

- [061: Detección de objetos en tiempo real con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/061-real-time-object-detection-with-tensorflow-js-and-node-js)
{.links-list}
- [061：使用 TensorFlow.js 和 Node.js 进行实时对象检测***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/061-real-time-object-detection-with-tensorflow-js-and-node-js)
{.links-list}
- [061: TensorFlow.js 및 Node.js를 사용한 실시간 개체 감지***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/061-real-time-object-detection-with-tensorflow-js-and-node-js)
{.links-list}


# 061: Real-Time Object Detection with TensorFlow.js and Node.js

In this post, we'll learn how to use TensorFlow.js and Node.js to perform real-time object detection.

## What is TensorFlow.js?

TensorFlow.js is an open-source library for machine learning in JavaScript. It allows you to train and run machine learning models in the browser or in a Node.js environment.

## What is Node.js?

Node.js is a JavaScript runtime environment that allows you to run JavaScript code outside of the browser.

## How can we use TensorFlow.js and Node.js to perform real-time object detection?

We can use TensorFlow.js and Node.js to perform real-time object detection by:

1. Training a machine learning model to detect objects in images.
2. Deploying the model to a Node.js server.
3. Using the server to process incoming images and detect objects in real-time.

## 1. Training a machine learning model to detect objects in images

We'll start by training a machine learning model to detect objects in images. For this, we'll use the MobileNet model. MobileNet is a pre-trained model that has been trained on a large dataset of images.

We can use MobileNet to perform object detection by:

1. Loading the MobileNet model.
2. Passing an image to the model.
3. Getting the model's predictions.

Let's see how we can do this in code:

```javascript
// Load the MobileNet model.
const model = await mobilenet.load();

// Classify the image.
const predictions = await model.classify(image);

// Get the model's predictions.
console.log(predictions);
```

## 2. Deploying the model to a Node.js server

Once we have trained our model, we can deploy it to a Node.js server. This will allow us to process incoming images and detect objects in real-time.

To do this, we'll need to:

1. Install the TensorFlow.js library.
2. Install the Node.js library.
3. Create a Node.js server.
4. Deploy the model to the server.

Let's see how we can do this in code:

```javascript
// Install the TensorFlow.js library.
npm install @tensorflow/tfjs

// Install the Node.js library.
npm install node

// Create a Node.js server.
const tf = require('@tensorflow/tfjs');
const express = require('express');
const app = express();

//Deploy the model to the server.
app.use(express.static(__dirname + '/model'));

// Process incoming images and detect objects in real-time.
app.post('/api/detect', async (req, res) => {
  // Classify the image.
  const predictions = await model.classify(req.body.image);

  // Send the predictions to the client.
  res.json(predictions);
});

// Start the server.
app.listen(3000, () => console.log('Server is running on port 3000'));
```

## 3. Using the server to process incoming images and detect objects in real-time

Once our server is up and running, we can use it to process incoming images and detect objects in real-time.

To do this, we'll need to:

1. Send an image to the server.
2. The server will process the image and return the predictions.
3. We can use the predictions to detect objects in the image.

Let's see how we can do this in code:

```javascript
// Send an image to the server.
const image = 'some-image.jpg';

fetch('/api/detect', {
  method: 'POST',
  body: JSON.stringify({ image }),
})
  .then(res => res.json())
  .then(predictions => {
    // Use the predictions to detect objects in the image.
    console.log(predictions);
  });
```

## Conclusion

In this post, we've learned how to use TensorFlow.js and Node.js to perform real-time object detection.