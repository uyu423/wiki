---
title: 077: Integrating TensorFlow.js with IoT Devices in Node.js
description: 
published: true
date: 2023-02-03T00:43:22.913Z
tags: 
editor: markdown
dateCreated: 2023-02-03T00:43:18.159Z
---

- [077: Integración de TensorFlow.js con dispositivos IoT en Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/077-integrating-tensorflow-js-with-iot-devices-in-node-js)
{.links-list}
- [077：在 Node.js 中将 TensorFlow.js 与物联网设备集成***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/077-integrating-tensorflow-js-with-iot-devices-in-node-js)
{.links-list}
- [077: TensorFlow.js를 Node.js에서 IoT 장치와 통합***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/077-integrating-tensorflow-js-with-iot-devices-in-node-js)
{.links-list}


# Integrating TensorFlow.js with IoT Devices in Node.js

TensorFlow.js is an open-source library that can be used to develop and train machine learning models in the browser. It can also be used to run these models on IoT devices. In this post, we will show how to use TensorFlow.js with Node.js to develop an application that can be used to control an IoT device.

## Prerequisites

Before we get started, there are a few things you'll need:

- A basic understanding of JavaScript
- Node.js installed on your computer
- A text editor ( we recommend [Visual Studio Code](https://code.visualstudio.com/))

## Getting Started

We will be using the [TensorFlow.js](https://js.tensorflow.org/) library to develop our application. The first thing we need to do is include the TensorFlow.js library in our project. We can do this by adding the following line of code to the head of our HTML file:

```
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.0"> </script>
```

Now that we have the TensorFlow.js library included in our project, we can start developing our application.

## Developing the Application

Our application will be a simple one that uses a pre-trained model to control an IoT device. The first thing we need to do is load the model. We can do this using the tf.loadModel() function:

```javascript
const model = await tf.loadModel('https://my-model-url');
```

Next, we need to define the inputs and outputs for our model. We can do this using the tf.layers.input() and tf.layers.dense() functions:

```javascript
const input = tf.layers.input({shape: [1]});
const output = tf.layers.dense({units: 1, activation: 'sigmoid'}).apply(input);
```

Now that we have our model loaded and the inputs and outputs defined, we can write the code that will actually control the IoT device. We'll do this by creating a function that takes an input and uses the model to predict the output:

```javascript
async function predict(input) {
  const output = model.predict(input);
  return output;
}
```

Finally, we need to write the code that will call the predict() function and use the output to control the IoT device. We'll do this by using the Node.js [serialport](https://serialport.io/) library:

```javascript
const SerialPort = require('serialport');
const Readline = require('@serialport/parser-readline');

const port = new SerialPort('/dev/ttyACM0', {
  baudRate: 9600
});

const parser = port.pipe(new Readline({ delimiter: '\r\n' }));

parser.on('data', async line => {
  const input = parseFloat(line);
  const output = await predict(input);
  port.write(output);
});
```

## Conclusion

In this post, we've shown how to use TensorFlow.js with Node.js to develop an application that can be used to control an IoT device. We've just scratched the surface of what's possible with TensorFlow.js and IoT, but we hope this has given you a taste of what's possible and inspired you to explore further.