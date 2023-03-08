---
title: 083: Using TensorFlow.js with Other ML Frameworks in Node.js
description: 
published: true
date: 2023-02-03T02:17:30.499Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:17:25.700Z
---

- [083: Uso de TensorFlow.js con otros marcos de aprendizaje automático en Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/083-using-tensorflow-js-with-other-ml-frameworks-in-node-js)
{.links-list}
- [083：在 Node.js 中将 TensorFlow.js 与其他 ML 框架结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/083-using-tensorflow-js-with-other-ml-frameworks-in-node-js)
{.links-list}
- [083: TensorFlow.js를 Node.js의 다른 ML 프레임워크와 함께 사용***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/083-using-tensorflow-js-with-other-ml-frameworks-in-node-js)
{.links-list}


# Using TensorFlow.js with Other ML Frameworks in Node.js

TensorFlow.js is a powerful JavaScript library for training and deploying machine learning models. It can be used with other ML frameworks, such as TensorFlow Lite, to run inference on Node.js.

In this post, we'll show you how to use TensorFlow.js with other ML frameworks in Node.js. We'll also provide some tips on how to get the most out of TensorFlow.js.

## Using TensorFlow.js with TensorFlow Lite

TensorFlow.js can be used with TensorFlow Lite to run inference on Node.js. TensorFlow Lite is a lightweight framework for running machine learning models on mobile devices.

To use TensorFlow.js with TensorFlow Lite, you'll need to install the TensorFlow Lite Node.js bindings. You can do this with npm:

```
npm install @tensorflow/tfjs-node
```

Once the bindings are installed, you can use the `tensorflow.js` module to load a TensorFlow Lite model and run inference on it.

Here's an example of how to use TensorFlow.js with TensorFlow Lite:

```javascript
const tf = require('@tensorflow/tfjs-node');

// Load a TensorFlow Lite model.
const model = await tf.loadLiteModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_1.0_224/model.json');

// Run inference on a TensorFlow Lite model.
const output = model.predict(tf.zeros([1, 224, 224, 3]));

// Print the output of the model.
console.log(output);
```

## Using TensorFlow.js with Other ML Frameworks

TensorFlow.js can also be used with other ML frameworks, such as Keras, to run inference on Node.js.

To use TensorFlow.js with Keras, you'll need to install the TensorFlow.js Node.js bindings. You can do this with npm:

```
npm install @tensorflow/tfjs
```

Once the bindings are installed, you can use the `tf` module to load a Keras model and run inference on it.

Here's an example of how to use TensorFlow.js with Keras:

```javascript
const tf = require('@tensorflow/tfjs');

// Load a Keras model.
const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_1.0_224/model.json');

// Run inference on a Keras model.
const output = model.predict(tf.zeros([1, 224, 224, 3]));

// Print the output of the model.
console.log(output);
```

## Tips for Using TensorFlow.js

Here are some tips for using TensorFlow.js:

- If you're new to TensorFlow.js, we recommend starting with the [TensorFlow.js getting started guide](https://js.tensorflow.org/tutorials/getting-started.html).
- If you're using TensorFlow.js with other ML frameworks, we recommend using the [TensorFlow.js Node.js bindings](https://www.npmjs.com/package/@tensorflow/tfjs).
- If you're using TensorFlow.js with TensorFlow Lite, we recommend using the [TensorFlow Lite Node.js bindings](https://www.npmjs.com/package/@tensorflow/tfjs-node).
- If you're using TensorFlow.js with a web browser, we recommend using a [WebAssembly-based backend](https://js.tensorflow.org/api/0.12.0/#enabling-webassembly-support).