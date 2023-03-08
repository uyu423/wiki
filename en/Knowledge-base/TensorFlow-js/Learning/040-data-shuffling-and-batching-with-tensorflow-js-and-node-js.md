---
title: 040: Data Shuffling and Batching with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T16:17:37.635Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:17:33.111Z
---

- [040: Mezcla y agrupación de datos con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/040-data-shuffling-and-batching-with-tensorflow-js-and-node-js)
{.links-list}
- [040：使用 TensorFlow.js 和 Node.js 进行数据洗牌和批处理***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/040-data-shuffling-and-batching-with-tensorflow-js-and-node-js)
{.links-list}
- [040: TensorFlow.js 및 Node.js를 사용한 데이터 셔플링 및 일괄 처리***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/040-data-shuffling-and-batching-with-tensorflow-js-and-node-js)
{.links-list}


# Data Shuffling and Batching with TensorFlow.js and Node.js

TensorFlow.js is a JavaScript library for training and deploying machine learning models in the browser and on Node.js.

In this tutorial, we'll learn how to shuffle and batch data with TensorFlow.js. We'll cover the following topics:

* What is data shuffling and why is it important?
* How to shuffle data with TensorFlow.js?
* How to batch data with TensorFlow.js?
* How to shuffle and batch data together with TensorFlow.js?

## What is data shuffling and why is it important?

When training machine learning models, it's important to shuffle the data before each epoch. This is because, if the data is not shuffled, the model might overfit on the first few samples in the dataset.

Data shuffling is the process of randomly reordering the samples in a dataset. This can be done either before or after each epoch.

There are two main benefits of shuffling data:

* It helps prevent the model from overfitting on the first few samples in the dataset.
* It can help the model converge faster, since it sees different samples at each epoch.

## How to shuffle data with TensorFlow.js?

To shuffle data with TensorFlow.js, we first need to convert our data into a `tf.data.Dataset`.

We can do this by using the `tf.data.array()` or `tf.data.tensor()` methods:

```js
// Convert an array into a dataset
const dataset = tf.data.array([1, 2, 3, 4, 5]);

// Convert a tensor into a dataset
const dataset = tf.data.tensor([1, 2, 3, 4, 5]);
```

Once we have our dataset, we can use the `tf.data. shuffle()` method to shuffle the data:

```js
const shuffledDataset = dataset.shuffle();
```

## How to batch data with TensorFlow.js?

To batch data with TensorFlow.js, we first need to convert our data into a `tf.data.Dataset`.

We can do this by using the `tf.data.array()` or `tf.data.tensor()` methods:

```js
// Convert an array into a dataset
const dataset = tf.data.array([1, 2, 3, 4, 5]);

// Convert a tensor into a dataset
const dataset = tf.data.tensor([1, 2, 3, 4, 5]);
```

Once we have our dataset, we can use the `tf.data. batch()` method to batch the data:

```js
const batchedDataset = dataset.batch(2);
```

## How to shuffle and batch data together with TensorFlow.js?

To shuffle and batch data together with TensorFlow.js, we first need to convert our data into a `tf.data.Dataset`.

We can do this by using the `tf.data.array()` or `tf.data.tensor()` methods:

```js
// Convert an array into a dataset
const dataset = tf.data.array([1, 2, 3, 4, 5]);

// Convert a tensor into a dataset
const dataset = tf.data.tensor([1, 2, 3, 4, 5]);
```

Once we have our dataset, we can use the `tf.data. shuffle()` and `tf.data. batch()` methods to shuffle and batch the data:

```js
const shuffledAndBatchedDataset = dataset.shuffle().batch(2);
```