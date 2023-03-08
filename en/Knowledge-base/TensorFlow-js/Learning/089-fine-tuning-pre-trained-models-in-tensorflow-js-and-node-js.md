---
title: 089: Fine-Tuning Pre-Trained Models in TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-03T03:44:01.054Z
tags: 
editor: markdown
dateCreated: 2023-02-03T03:43:59.396Z
---

- [089: Ajuste fino de modelos preentrenados en TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/089-fine-tuning-pre-trained-models-in-tensorflow-js-and-node-js)
{.links-list}
- [089：在 TensorFlow.js 和 Node.js 中微调预训练模型***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/089-fine-tuning-pre-trained-models-in-tensorflow-js-and-node-js)
{.links-list}
- [089: TensorFlow.js 및 Node.js에서 사전 학습된 모델 미세 조정***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/089-fine-tuning-pre-trained-models-in-tensorflow-js-and-node-js)
{.links-list}


# 089: Fine-Tuning Pre-Trained Models in TensorFlow.js and Node.js

TensorFlow.js is a powerful tool that allows us to train and deploy machine learning models in the browser. In this post, we will learn how to fine-tune pre-trained models in TensorFlow.js and Node.js.

## What are pre-trained models?

Pre-trained models are machine learning models that have been trained on a large dataset. These models can be used to perform tasks such as image classification, object detection, and text classification.

## Why fine-tune pre-trained models?

Fine-tuning pre-trained models is a common technique in machine learning. It allows us to adapt pre-trained models to our own dataset. This can be useful when our dataset is small or when we want to improve the performance of a pre-trained model on our dataset.

## How to fine-tune pre-trained models?

There are two common ways to fine-tune pre-trained models:

1. **Transfer learning**: We can use a pre-trained model as a starting point and then train it on our own dataset. This is a common technique when our dataset is small.

2. **Fine-tuning**: We can use a pre-trained model and then fine-tune it on our own dataset. This is a common technique when we want to improve the performance of a pre-trained model on our dataset.

In this post, we will focus on fine-tuning pre-trained models.

## Fine-tuning pre-trained models in TensorFlow.js

TensorFlow.js provides a high-level API for fine-tuning pre-trained models. We will use the `tf.fineTuneModel()` function to fine-tune a pre-trained model.

First, we need to load a pre-trained model. We will use the `tf.loadLayersModel()` function to load a pre-trained model from a URL.

Next, we need to define the inputs and outputs of the model. We will use the `tf.input()` and `tf.output()` functions to define the inputs and outputs of the model.

Finally, we need to call the `tf.fineTuneModel()` function to fine-tune the pre-trained model. We will need to specify the optimizer, loss, and metrics.

Here is an example of how to fine-tune a pre-trained model in TensorFlow.js:

```javascript
// Load a pre-trained model
const model = tf.loadLayersModel('https://model-url');

// Define the inputs and outputs of the model
const input = tf.input({shape: [28, 28, 1]});
const output = model.outputs[0];

// Fine-tune the model
const model = tf.fineTuneModel(
    model,
    {
      optimizer: tf.train.adam(0.001),
      loss: tf.losses.softmaxCrossEntropy,
      metrics: ['accuracy']
    },
    {
      // We will use a validation split of 0.1
      validationSplit: 0.1
    }
);
```

## Fine-tuning pre-trained models in Node.js

TensorFlow.js provides a Node.js API for fine-tuning pre-trained models. We will use the `tf.node.fineTuneModel()` function to fine-tune a pre-trained model.

First, we need to load a pre-trained model. We will use the `tf.node.loadLayersModel()` function to load a pre-trained model from a URL.

Next, we need to define the inputs and outputs of the model. We will use the `tf.node.input()` and `tf.node.output()` functions to define the inputs and outputs of the model.

Finally, we need to call the `tf.node.fineTuneModel()` function to fine-tune the pre-trained model. We will need to specify the optimizer, loss, and metrics.

Here is an example of how to fine-tune a pre-trained model in Node.js:

```javascript
// Load a pre-trained model
const model = tf.node.loadLayersModel('https://model-url');

// Define the inputs and outputs of the model
const input = tf.node.input({shape: [28, 28, 1]});
const output = model.outputs[0];

// Fine-tune the model
const model = tf.node.fineTuneModel(
    model,
    {
      optimizer: tf.train.adam(0.001),
      loss: tf.losses.softmaxCrossEntropy,
      metrics: ['accuracy']
    },
    {
      // We will use a validation split of 0.1
      validationSplit: 0.1
    }
);
```

## Conclusion

In this post, we learned how to fine-tune pre-trained models in TensorFlow.js and Node.js. We saw that TensorFlow.js provides a high-level API for fine-tuning pre-trained models. We also saw that TensorFlow.js provides a Node.js API for fine-tuning pre-trained models.