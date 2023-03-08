---
title: 003: Understanding TensorFlow.js Core API
description: 
published: true
date: 2023-02-02T07:23:30.993Z
tags: 
editor: markdown
dateCreated: 2023-02-02T07:23:26.580Z
---

- [003: comprensión de la API principal de TensorFlow.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/003-understanding-tensorflow-js-core-api)
{.links-list}
- [003：了解 TensorFlow.js 核心 API***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/003-understanding-tensorflow-js-core-api)
{.links-list}
- [003: TensorFlow.js 핵심 API 이해하기***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/003-understanding-tensorflow-js-core-api)
{.links-list}


# Understanding TensorFlow.js Core API

TensorFlow.js is an open-source web framework that allows developers to train and deploy machine learning models in the browser. The TensorFlow.js Core API is a low-level API that allows developers to create, manipulate, and optimize numerical computations in JavaScript.

## What is a Tensor?

A tensor is a data structure that represents a linear transformation. In simple terms, a tensor is an array of numbers. In TensorFlow.js, a tensor has a shape and a data type. The shape of a tensor is the size and dimensionality of the array, and the data type is the type of data that the tensor contains (e.g. `float32`, `int32`, `string`).

## Creating Tensors

There are a few ways to create tensors in TensorFlow.js. The simplest way is to create a tensor from a JavaScript array using the `tf.tensor` function:

```javascript
const a = tf.tensor([1, 2, 3, 4]);
```

The `tf.tensor` function also allows you to specify the shape and data type of the tensor:

```javascript
const b = tf.tensor([1, 2, 3, 4], [2, 2], 'int32');
```

You can also create a tensor from a scalar (a single number):

```javascript
const c = tf.scalar(5);
```

## Manipulating Tensors

Tensors can be manipulated using a variety of functions in the TensorFlow.js API. For example, you can add two tensors using the `tf.add` function:

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = tf.tensor([5, 6, 7, 8]);
const c = tf.add(a, b);
```

You can also perform element-wise operations on tensors. Element-wise operations are operations that are applied to each element in the tensor independently. For example, you can multiply two tensors element-wise using the `tf.mul` function:

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = tf.tensor([5, 6, 7, 8]);
const c = tf.mul(a, b);
```

## Converting Tensors

Tensors can be converted to other data structures using the `.toXXX` methods. For example, you can convert a tensor to a JavaScript array using the `.toArray` method:

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = a.toArray(); // [1, 2, 3, 4]
```

You can also convert a tensor to a string using the `.toString` method:

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = a.toString(); // "1 2 3 4"
```

## Optimizing Computations

TensorFlow.js provides a variety of optimization functions that can be used to optimize numerical computations. For example, you can use the `tf.clipByValue` function to clip tensor values to a specified range:

```javascript
const a = tf.tensor([-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5]);
const b = tf.clipByValue(a, -2, 2);
```

You can also use the `tf.addN` function to perform element-wise addition on a list of tensors:

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = tf.tensor([5, 6, 7, 8]);
const c = tf.tensor([9, 10, 11, 12]);
const d = tf.addN([a, b, c]);
```

## Learning More

TensorFlow.js is a powerful tool that allows developers to create, manipulate, and optimize numerical computations in JavaScript. The TensorFlow.js Core API is a low-level API that provides the building blocks for creating, manipulating, and optimizing numerical computations in JavaScript.

If you want to learn more about TensorFlow.js, we recommend checking out the following resources:

- The TensorFlow.js documentation: https://js.tensorflow.org/
- The TensorFlow.js GitHub repository: https://github.com/tensorflow/tfjs
- The TensorFlow.js Core API reference: https://js.tensorflow.org/api/core.html