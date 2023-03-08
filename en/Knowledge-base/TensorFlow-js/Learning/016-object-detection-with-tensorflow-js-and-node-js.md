---
title: 016: Object Detection with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T10:36:36.831Z
tags: 
editor: markdown
dateCreated: 2023-02-02T10:36:32.426Z
---

- [016: Detección de objetos con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/016-object-detection-with-tensorflow-js-and-node-js)
{.links-list}
- [016：使用 TensorFlow.js 和 Node.js 进行对象检测***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/016-object-detection-with-tensorflow-js-and-node-js)
{.links-list}
- [016: TensorFlow.js 및 Node.js를 사용한 객체 감지***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/016-object-detection-with-tensorflow-js-and-node-js)
{.links-list}


# Object Detection with TensorFlow.js and Node.js

In this post, we'll learn how to use TensorFlow.js and Node.js to perform real-time object detection on images.

We'll start by setting up a development environment, then we'll install TensorFlow.js and its dependencies. Next, we'll write a Node.js script to load an image, run object detection on it, and draw the results to the screen. Finally, we'll take a look at some of the resources available for further learning.

## Setting up the development environment

Before we get started, we need to set up a development environment. For this post, we'll be using Node.js.

If you don't already have Node.js installed, you can download it from the [Node.js website](https://nodejs.org/en/). Once you have Node.js installed, you can create a new project directory and initialize it with the following commands:

```
mkdir object-detection
cd object-detection
npm init -y
```

## Installing TensorFlow.js and its dependencies

Now that we have a project directory set up, we can install TensorFlow.js and its dependencies. We'll be using the [tfjs-node](https://www.npmjs.com/package/@tensorflow/tfjs-node) package, which provides an implementation of TensorFlow.js that can be used on Node.js.

To install tfjs-node and its dependencies, run the following command:

```
npm install @tensorflow/tfjs-node
```

## Writing the object detection script

With TensorFlow.js installed, we can now write a script to perform object detection on images. We'll start by loading an image, then we'll use the [tf.data.detectObjects](https://js.tensorflow.org/api/latest/#tf.data.detectObjects) method to run object detection on the image. Finally, we'll draw the results to the screen.

The full script is available [here](https://github.com/tensorflow/tfjs-models/blob/master/tfjs-models/src/object_detection/index.js), but we'll walk through the key parts below.

First, we need to load the tfjs-node package:

```javascript
const tf = require('@tensorflow/tfjs-node');
```

Next, we'll load the [ coco-ssd model ](https://github.com/tensorflow/tfjs-models/tree/master/tfjs-models/detection), which we'll use for object detection. The coco-ssd model is a single-shot detection model that is trained on the [Common Objects in Context (COCO) dataset](http://cocodataset.org/#home).

```javascript
const cocoSSD = require('@tensorflow-models/coco-ssd');
```

With the model loaded, we can now write the code to load an image and run object detection on it. We'll start by loading the image using the [tf.node.decodeImage](https://js.tensorflow.org/api/latest/#tf.node.decodeImage) method. This method returns a promise that resolves to a tensor containing the image data.

```javascript
const image = tf.node.decodeImage(
  fs.readFileSync('./test-image.jpg')
);
```

Once the image is loaded, we can use the [tf.data.detectObjects](https://js.tensorflow.org/api/latest/#tf.data.detectObjects) method to run object detection on it. This method returns a promise that resolves to an array of objects, each of which contains information about a detected object, including the class of the object and its location within the image.

```javascript
const predictions = await cocoSSD.detectObjects(image);
```

Finally, we'll draw the results to the screen. We'll use the [tf.node.drawBoxes](https://js.tensorflow.org/api/latest/#tf.node.drawBoxes) method to draw boxes around the detected objects, and the [tf.node.writeFile](https://js.tensorflow.org/api/latest/#tf.node.writeFile) method to write the results to a new image file.

```javascript
const drawnImage = tf.node.drawBoxes(
  image,
  predictions.map(prediction => prediction.bbox)
);
tf.node.writeFile('./test-image-output.jpg', drawnImage.toBuffer());
```

## Running the object detection script

With the script written, we can now run it to perform object detection on an image. To run the script, use the following command:

```
node index.js
```

This will run the object detection script on the image `test-image.jpg` and write the results to `test-image-output.jpg`.

## Resources for further learning

- [TensorFlow.js Object Detection](https://js.tensorflow.org/tutorials/object-detection.html)
- [Real-time Object Detection with TensorFlow.js and Node.js](https://www.twilio.com/blog/real-time-object-detection-tensorflow-js-node-js)
- [Detect Objects Using Your Webcam](https://codelabs.developers.google.com/codelabs/tensorflowjs-object-detection/index.html)