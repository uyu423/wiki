---
title: 039: Data Augmentation with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T16:04:34.620Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:04:29.960Z
---

- [039: Aumento de datos con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/039-data-augmentation-with-tensorflow-js-and-node-js)
{.links-list}
- [039：使用 TensorFlow.js 和 Node.js 进行数据扩充***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/039-data-augmentation-with-tensorflow-js-and-node-js)
{.links-list}
- [039: TensorFlow.js 및 Node.js를 사용한 데이터 증대***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/039-data-augmentation-with-tensorflow-js-and-node-js)
{.links-list}


# Data Augmentation with TensorFlow.js and Node.js

## Introduction

Data augmentation is a technique used to artificially increase the size of a dataset by generating new data samples from existing ones. This is especially useful when the original dataset is small and you want to train a machine learning model with as much data as possible.

TensorFlow.js is a JavaScript library for training and deploying machine learning models. Node.js is a JavaScript runtime environment that allows you to run JavaScript code outside of a web browser.

In this post, we'll learn how to use TensorFlow.js and Node.js to perform data augmentation. We'll start by looking at what data augmentation is and why it's useful. We'll then see how to implement data augmentation in TensorFlow.js. Finally, we'll learn how to use Node.js to run our data augmentation code.

## What is Data Augmentation?

Data augmentation is a technique used to artificially increase the size of a dataset by generating new data samples from existing ones. This is especially useful when the original dataset is small and you want to train a machine learning model with as much data as possible.

Data augmentation works by applying a set of transformations to the existing data samples. The transformed samples are then used as new data samples. For example, if we have a dataset of images, we can perform data augmentation by applying transformations such as rotation, cropping, and flipping to the images. This will generate new images that can be used as part of the dataset.

The benefit of data augmentation is that it can help to improve the performance of machine learning models. This is because the augmented dataset is larger and contains more variety than the original dataset. This can help the model to learn more generalizable patterns.

## Data Augmentation in TensorFlow.js

TensorFlow.js is a JavaScript library for training and deploying machine learning models. It can be used in the browser or in a Node.js environment.

Data augmentation can be performed in TensorFlow.js using the `tf.data.Dataset` API. This API allows you to apply transformations to a dataset. The `tf.image` module contains a set of functions that can be used to perform image augmentation.

To use data augmentation in TensorFlow.js, we first need to create a `tf.data.Dataset` object. We can then apply transformations to this dataset using the `tf.image` module. Finally, we can use the `.forEachAsync()` method to run the augmentation code on each data sample.

## Node.js

Node.js is a JavaScript runtime environment that allows you to run JavaScript code outside of a web browser. It can be used to create server-side applications.

Node.js comes with a set of built-in modules that can be used to perform various tasks. For data augmentation, we'll be using the `fs` module, which allows us to read and write files.

## Example

In this example, we'll be using the MNIST dataset. This dataset contains images of handwritten digits. We'll be using the `tf.image` module to perform data augmentation on this dataset.

First, we'll need to load the MNIST dataset. We can do this using the `fs` module.


```javascript
var fs = require('fs');

var mnistData = fs.readFileSync('mnist.csv', {encoding: 'utf-8'});
```

Next, we'll need to parse the MNIST data. We can do this using the `tf.data.csv` module.


```javascript
var csv = require('@tensorflow/tfjs-data/src/data/csv');

var mnistDataset = csv.parse(mnistData, {
  columnConfigs: {
    label: {
      isLabel: true
    }
  }
});
```

Now that we have our dataset, we can start applying data augmentation. We'll start by creating a `tf.data.Dataset` object.


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: sample.xs,
    ys: sample.ys
  };
});
```

Next, we'll apply the `tf.image.resizeBilinear()` transformation to the dataset. This transformation will resize the images.


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: tf.image.resizeBilinear(sample.xs, [28, 28]),
    ys: sample.ys
  };
});
```

We can also apply the `tf.image.rotate()` transformation to the dataset. This transformation will rotate the images.


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: tf.image.rotate(sample.xs, tf.scalar(Math.random() * 2.0 * Math.PI)),
    ys: sample.ys
  };
});
```

Finally, we'll apply the `tf.image.flipLeftRight()` transformation to the dataset. This transformation will flip the images horizontally.


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: tf.image.flipLeftRight(sample.xs),
    ys: sample.ys
  };
});
```

Now that we've applied our transformations, we can use the `.forEachAsync()` method to run the data augmentation code on each data sample.


```javascript
mnistDataset.forEachAsync(function(sample) {
  // augment data here
});
```

## Conclusion

In this post, we've learned how to use TensorFlow.js and Node.js to perform data augmentation. We've seen how to use the `tf.data.Dataset` API to apply transformations to a dataset. We've also seen how to use the `.forEachAsync()` method to run the data augmentation code on each data sample.