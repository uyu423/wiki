---
title: 067: Creating Desktop Applications with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T22:36:31.360Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:36:26.668Z
---

- [067: Creación de aplicaciones de escritorio con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/067-creating-desktop-applications-with-tensorflow-js-and-node-js)
{.links-list}
- [067：使用 TensorFlow.js 和 Node.js 创建桌面应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/067-creating-desktop-applications-with-tensorflow-js-and-node-js)
{.links-list}
- [067: TensorFlow.js 및 Node.js로 데스크톱 애플리케이션 만들기***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/067-creating-desktop-applications-with-tensorflow-js-and-node-js)
{.links-list}


# 067: Creating Desktop Applications with TensorFlow.js and Node.js

In this post, we'll be looking at how to create desktop applications with TensorFlow.js and Node.js.

TensorFlow.js is a powerful tool for machine learning in JavaScript. Node.js is a JavaScript runtime that allows you to run JavaScript code outside of the browser.

Together, these two technologies can be used to create desktop applications that use machine learning.

## Getting Started

To get started, you'll need to install Node.js and TensorFlow.js.

Node.js can be downloaded from the [Node.js website](https://nodejs.org/en/). TensorFlow.js can be installed using the [Node.js package manager](https://www.npmjs.com/):

```
npm install @tensorflow/tfjs
```

Once you have Node.js and TensorFlow.js installed, you're ready to start creating your desktop application.

## Creating a Desktop Application

To create a desktop application with TensorFlow.js and Node.js, you'll need to create a Node.js file and a HTML file.

The Node.js file will be used to run your machine learning code. The HTML file will be used to display the results of your machine learning code.

We'll start by creating a Node.js file called `main.js`. In this file, we'll require the TensorFlow.js library and load a pre-trained model.

```javascript
const tf = require('@tensorflow/tfjs');

// Load a pre-trained model.
const model = tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

Next, we'll create an HTML file called `index.html`. In this file, we'll include the following code:

```html
<html>
  <head>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs"></script>
    <script src="main.js"></script>
  </head>
  <body>
    <h1>Hello, TensorFlow.js!</h1>
  </body>
</html>
```

This code includes the TensorFlow.js library and the `main.js` file. It also contains a simple `<h1>` tag.

Finally, we'll need to run the `index.html` file using Node.js. We can do this by running the following command:

```
node index.html
```

This will start a local server and open the `index.html` file in your default web browser.

## Conclusion

In this post, we've seen how to create desktop applications with TensorFlow.js and Node.js. We've also seen how to load a pre-trained model and run it in a Node.js file.

If you're interested in learning more about TensorFlow.js and Node.js, I recommend checking out the following resources:

- [Getting Started with TensorFlow.js](https://js.tensorflow.org/tutorials/getting-started.html)
- [TensorFlow.js for Beginners](https://www.youtube.com/watch?v=HEQDRWMK6yY)
- [Node.js for Beginners](https://www.youtube.com/watch?v=U8XF6AFGqlc)