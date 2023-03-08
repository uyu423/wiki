---
title: 004: Tensors and Operations in TensorFlow.js
description: 
published: true
date: 2023-02-02T07:36:29.759Z
tags: 
editor: markdown
dateCreated: 2023-02-02T07:36:25.431Z
---

- [004: Tensores y Operaciones en TensorFlow.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/004-tensors-and-operations-in-tensorflow-js)
{.links-list}
- [004：TensorFlow.js 中的张量和运算***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/004-tensors-and-operations-in-tensorflow-js)
{.links-list}
- [004: TensorFlow.js의 텐서 및 작업***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/004-tensors-and-operations-in-tensorflow-js)
{.links-list}


# Introduction

TensorFlow.js is a powerful JavaScript library for machine learning, and one of its key features is the ability to work with tensors. In this post, we'll take a look at what tensors are and how to work with them in TensorFlow.js.

# What is a Tensor?

A tensor is a generalization of a vector. Vectors are often thought of as one-dimensional arrays of numbers, but tensors can be thought of as arrays of any dimension. Just as vectors can be added and multiplied by scalars, so can tensors.

Tensors are often used in machine learning because they can be used to represent data in a variety of ways. For example, an image can be represented as a three-dimensional tensor, with the height, width, and depth of the image being the three dimensions.

# TensorFlow.js

TensorFlow.js is a JavaScript library for machine learning that allows you to work with tensors in a variety of ways. In this post, we'll take a look at a few of the ways that you can work with tensors in TensorFlow.js.

# Creating Tensors

Tensors can be created from JavaScript arrays using the tf.tensor function. For example, the following code creates a two-dimensional tensor with the values 1, 2, 3, and 4:

```javascript
const t = tf.tensor([[1, 2], [3, 4]]);
```

You can also create tensors with specific values using the tf.ones, tf.zeros, and tf.fill functions. For example, the following code creates a two-dimensional tensor with the values 1, 0, 1, and 0:

```javascript
const t = tf.ones([2, 2]);
```

# Manipulating Tensors

Tensors can be manipulated in a variety of ways. The most common way to manipulate a tensor is to use the tf.transpose function. This function permutes the dimensions of a tensor. For example, the following code creates a two-dimensional tensor with the values 1, 2, 3, and 4 and then permutes the dimensions to create a new tensor with the values 1, 3, 2, and 4:

```javascript
const t = tf.tensor([[1, 2], [3, 4]]);
const t2 = t.transpose();
```

Tensors can also be reshaped using the tf.reshape function. This function returns a new tensor with the same values as the original tensor but with a different shape. For example, the following code creates a two-dimensional tensor with the values 1, 2, 3, and 4 and then reshapes it to a one-dimensional tensor with the values 1, 2, 3, 4:

```javascript
const t = tf.tensor([[1, 2], [3, 4]]);
const t2 = t.reshape([4]);
```

# Working with Tensors in TensorFlow.js

TensorFlow.js provides a variety of functions for working with tensors. In this section, we'll take a look at a few of the most commonly used functions.

The tf.tensor function can be used to create a tensor from a JavaScript array. The tf.ones and tf.zeros functions can be used to create tensors with all ones or all zeros, respectively. The tf.fill function can be used to create a tensor with a given value.

The tf.transpose function can be used to permute the dimensions of a tensor. The tf.reshape function can be used to reshape a tensor.

The tf.concat function can be used to concatenate two or more tensors along a given dimension. The tf.split function can be used to split a tensor along a given dimension.

The tf.add, tf.sub, tf.mul, and tf.div functions can be used to perform element-wise addition, subtraction, multiplication, and division on two tensors, respectively.

The tf.matMul function can be used to perform a matrix multiplication on two two-dimensional tensors.

The tf.sum function can be used to compute the sum of all the elements in a tensor. The tf.mean function can be used to compute the mean of all the elements in a tensor.

# Conclusion

In this post, we've taken a look at what tensors are and how to work with them in TensorFlow.js. We've seen how to create tensors and how to manipulate them. We've also seen how to work with tensors in TensorFlow.js using a variety of functions.