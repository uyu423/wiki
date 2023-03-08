---
title: 069: Scaling TensorFlow.js Applications with Node.js
description: 
published: true
date: 2023-02-02T23:04:26.275Z
tags: 
editor: markdown
dateCreated: 2023-02-02T23:04:21.732Z
---

- [069: Escalado de aplicaciones TensorFlow.js con Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/069-scaling-tensorflow-js-applications-with-node-js)
{.links-list}
- [069：使用 Node.js 扩展 TensorFlow.js 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/069-scaling-tensorflow-js-applications-with-node-js)
{.links-list}
- [069: Node.js로 TensorFlow.js 애플리케이션 확장***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/069-scaling-tensorflow-js-applications-with-node-js)
{.links-list}


# 069: Scaling TensorFlow.js Applications with Node.js

TensorFlow.js is a powerful tool for machine learning in JavaScript, but what do you do when your TensorFlow.js application outgrows the browser? In this post, we'll explore how to scale TensorFlow.js applications with Node.js.

## What is TensorFlow.js?

TensorFlow.js is an open-source library for machine learning in JavaScript. It's used by developers to create sophisticated machine learning models that run in the browser or in Node.js.

## Why use Node.js for TensorFlow.js?

Node.js is a great choice for scaling TensorFlow.js applications. It's fast, efficient, and has a large ecosystem of libraries and tools.

## How to scale TensorFlow.js with Node.js

There are two main ways to scale TensorFlow.js applications with Node.js:

1. Use the `tensorflow.js` Node.js module.
2. Use a TensorFlow.js-compatible library like `tfjs-node`.

We'll explore each of these methods in more detail below.

### Using the `tensorflow.js` Node.js module

The `tensorflow.js` Node.js module is the official way to run TensorFlow.js in Node.js. It's easy to install and use.

To install the `tensorflow.js` Node.js module, run the following command:

```
npm install @tensorflow/tfjs
```

To use the `tensorflow.js` Node.js module, require it in your code:

```javascript
const tf = require('@tensorflow/tfjs');
```

Now you can use all the TensorFlow.js APIs in your Node.js application.

### Using a TensorFlow.js-compatible library

If you want to use a TensorFlow.js-compatible library like `tfjs-node`, you'll need to install it first.

To install `tfjs-node`, run the following command:

```
npm install tfjs-node
```

To use `tfjs-node`, require it in your code:

```javascript
const tf = require('tfjs-node');
```

Now you can use all the TensorFlow.js APIs in your Node.js application.

## Resources for further reading

- [TensorFlow.js documentation](https://js.tensorflow.org/)
- [tfjs-node documentation](https://github.com/tensorflow/tfjs-node)
- [Node.js documentation](https://nodejs.org/en/docs/)