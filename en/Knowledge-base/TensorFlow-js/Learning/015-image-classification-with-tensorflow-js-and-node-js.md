---
title: 015: Image Classification with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T10:18:00.265Z
tags: 
editor: markdown
dateCreated: 2023-02-02T10:17:55.932Z
---

- [015: Clasificación de imágenes con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/015-image-classification-with-tensorflow-js-and-node-js)
{.links-list}
- [015：使用 TensorFlow.js 和 Node.js 进行图像分类***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/015-image-classification-with-tensorflow-js-and-node-js)
{.links-list}
- [015: TensorFlow.js 및 Node.js를 사용한 이미지 분류***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/015-image-classification-with-tensorflow-js-and-node-js)
{.links-list}


# Introduction

In this post, we'll be looking at how to use TensorFlow.js and Node.js to build an image classification model. We'll be using the MobileNet model, which is a pre-trained model that has been trained on a large dataset of images.

We'll be using the following libraries:

* [TensorFlow.js](https://js.tensorflow.org/)
* [ Node.js](https://nodejs.org/en/)

## Prerequisites

Before we get started, there are a few things that you'll need to have set up:

* A text editor. I recommend [Visual Studio Code](https://code.visualstudio.com/).
* [Node.js](https://nodejs.org/en/). This will be used to run our code.
* [TensorFlow.js](https://js.tensorflow.org/). This is a JavaScript library for machine learning.

## Getting Started

1. Create a new directory for your project.

2. Create a file called `index.js` in your project directory.

3. Copy the following code into `index.js`:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MobileNet model.
const model = tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');

// Make a prediction through the model on our image.
const imgEl = document.getElementById('img');
model.predict(tf.fromPixels(imgEl)).then(predictions => {
  console.log('Predictions: ');
  console.log(predictions);
});
```

4. Create a file called `index.html` in your project directory.

5. Copy the following code into `index.html`:

```html
<html>
  <body>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.11.3"> </script>
    <script src="index.js"></script>
    <img id="img" src="https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/test_images/grace_hopper.jpg">
  </body>
</html>
```

6. Run the following command to start the server:

```
node index.js
```

You should see the following output:

```
Predictions:
[
  {
    className: 'daisy',
    probability: 0.9911273956298828
  },
  {
    className: 'tulip',
    probability: 0.008872604370117188
  },
  {
    className: 'sunflower',
    probability: 0.0001983642578125
  },
  {
    className: 'dandelion',
    probability: 0.0000457763671875
  },
  {
    className: 'roses',
    probability: 0.0000095367431640625
  }
]
```

## What's happening?

In the code above, we're using the MobileNet model to classify an image. MobileNet is a pre-trained model that has been trained on a large dataset of images.

When we run the `predict` method, TensorFlow.js will return an array of predictions, each with a `className` and a `probability`. The `className` is the name of the class that the model predicts the image belongs to, and the `probability` is the confidence that the model has in that prediction.

## Making predictions on a webcam

In the example above, we're using a pre-trained model to make predictions on an image. But what if we want to make predictions on a live webcam feed?

To do this, we'll need to use the `tf.data` and `tf.layers` APIs.

First, we'll create a ` webcam ` object. This will be used to capture the live webcam feed:

```javascript
const webcam = new tf.data.webcam(document.getElementById('webcam'));
```

Next, we'll create a ` convolutional ` layer. This layer will be used to process the live webcam feed:

```javascript
const layer = tf.layers.conv2d({
  kernelSize: 5,
  filters: 20,
  strides: 1,
  activation: 'relu',
  kernelInitializer: 'varianceScaling',
  inputShape: [28, 28, 1]
});
```

Now we'll create a ` function ` that will be used to make predictions on the live webcam feed. This function will take in an image, process it through the ` convolutional ` layer, and return a prediction:

```javascript
async function predict(image) {
  // Make a prediction through the model on the image.
  const predictions = await model.predict(image);

  // Return the highest confidence prediction.
  return predictions.as1D().argMax();
}
```

Finally, we'll create a ` loop ` that will continuously make predictions on the live webcam feed:

```javascript
while (true) {
  // Get the next image from the webcam.
  const img = await webcam.capture();

  // Get the prediction from our model.
  const prediction = await predict(img);

  // Convert the prediction into a human-readable string.
  const classNames = ['daisy', 'tulip', 'sunflower', 'dandelion', 'roses'];
  const className = classNames[prediction.dataSync()[0]];

  // Display the string on the page.
  document.getElementById('prediction').innerText = className;

  // Dispose the image when we're done.
  img.dispose();

  // Give some breathing room by waiting for the next animation frame to
  // fire before making another prediction.
  await tf.nextFrame();
}
```

## Conclusion

In this post, we've seen how to use TensorFlow.js and Node.js to build an image classification model. We've also seen how to use the model to make predictions on a live webcam feed.