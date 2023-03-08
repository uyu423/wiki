---
title: 051: Using Callbacks with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T18:43:32.403Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:43:27.817Z
---

- [051: uso de devoluciones de llamada con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/051-using-callbacks-with-tensorflow-js-and-node-js)
{.links-list}
- [051：在 TensorFlow.js 和 Node.js 中使用回调***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/051-using-callbacks-with-tensorflow-js-and-node-js)
{.links-list}
- [051: TensorFlow.js 및 Node.js에서 콜백 사용***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/051-using-callbacks-with-tensorflow-js-and-node-js)
{.links-list}


# Using Callbacks with TensorFlow.js and Node.js

TensorFlow.js is a powerful tool for machine learning in JavaScript. Node.js is a JavaScript runtime that allows you to run JavaScript on the server. In this post, we'll show you how to use callbacks with TensorFlow.js and Node.js.

## What are callbacks?

A callback is a function that is passed as an argument to another function. The callback function is called when the other function is finished executing. Callbacks are commonly used in JavaScript to perform asynchronous operations.

## Using callbacks with TensorFlow.js

TensorFlow.js provides a callback API that allows you to perform asynchronous operations. The callback API is available in the `tf.tensor` class.

To use the callback API, you must first create a `tf.tensor` object. The `tf.tensor` class takes a data array and a shape array as arguments. The data array is a JavaScript array that contains the data for the tensor. The shape array is a JavaScript array that contains the dimensions of the tensor.

Once you have created a `tf.tensor` object, you can use the `.then()` method to register a callback function. The `.then()` method takes a callback function as an argument. The callback function is called when the `tf.tensor` object is ready.

The `.then()` method returns a `Promise` object. The `Promise` object represents the result of the `.then()` method. The `Promise` object has a `.then()` method that can be used to register another callback function.

Here is an example of using the `.then()` method to register a callback function:

```javascript
const tensor = tf.tensor([1, 2, 3, 4], [2, 2]);

tensor.then(t => {
  // The callback function is called when the tensor is ready.
  // The tensor is passed as an argument to the callback function.
  // The tensor can be used in the callback function.
  console.log(t);
});
```

## Using callbacks with Node.js

Node.js provides a callback API that allows you to perform asynchronous operations. The callback API is available in the `fs` module.

The `fs` module provides an API for interacting with the file system. The `fs` module has a `readFile()` method that can be used to read a file asynchronously. The `readFile()` method takes a file path and a callback function as arguments. The callback function is called when the file is read. The file data is passed as an argument to the callback function.

Here is an example of using the `readFile()` method to read a file asynchronously:

```javascript
const fs = require('fs');

fs.readFile('file.txt', (err, data) => {
  // The callback function is called when the file is read.
  // The file data is passed as an argument to the callback function.
  // The file data can be used in the callback function.
  console.log(data);
});
```

## Additional Information

- [Using Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
- [Node.js Callbacks](https://nodejs.org/api/fs.html#fs_fs_readfile_path_options_callback)