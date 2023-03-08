---
title: 023: Text Generation with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T12:17:23.667Z
tags: 
editor: markdown
dateCreated: 2023-02-02T12:17:19.212Z
---

- [023: Generación de Texto con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/023-text-generation-with-tensorflow-js-and-node-js)
{.links-list}
- [023：使用 TensorFlow.js 和 Node.js 生成文本***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/023-text-generation-with-tensorflow-js-and-node-js)
{.links-list}
- [023: TensorFlow.js 및 Node.js를 사용한 텍스트 생성***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/023-text-generation-with-tensorflow-js-and-node-js)
{.links-list}


# Text Generation with TensorFlow.js and Node.js

In this post, we'll learn how to generate text using TensorFlow.js and Node.js. We'll be using a char-rnn model, which is a type of recurrent neural network (RNN) that can learn to predict the next character in a sequence of text.

## What is a char-rnn?

A char-rnn is a type of RNN that can learn to predict the next character in a sequence of text. The char-rnn model we'll be using is based on the one described in the paper "Character-Aware Neural Language Models" (https://arxiv.org/abs/1508.06615).

## What is TensorFlow.js?

TensorFlow.js is a JavaScript library for training and deploying machine learning models in the browser and in Node.js.

## What is Node.js?

Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine.

## Getting Started

First, we need to install TensorFlow.js and Node.js. We'll be using the TensorFlow.js char-rnn model, which is a Node.js module.

```
npm install @tensorflow/tfjs-node
npm install @tensorflow/tfjs-node-charrnn
```

Next, we need to download the training data. For this example, we'll use a dataset of Shakespeare's works (https://www.kaggle.com/kinguistics/shakespeare-plays).

Once we have the training data, we can start training the char-rnn model. The training process can take a few minutes to complete.

```
const tf = require('@tensorflow/tfjs-node');
const charRNN = require('@tensorflow/tfjs-node-charrnn');

const model = charRNN.create(
  'https://storage.googleapis.com/tfjs-models/tfjs/charrnn/data/shakespeare_input.txt',
  {
    rnnType: 'lstm',
    embeddingSize: 128,
    rnnUnits: 128,
    batchSize: 64,
    seqLength: 128,
    temperature: 0.8,
    numEpochs: 20
  });

model.fit().then(() => {
  // The model is trained!
});
```

Once the model is trained, we can use it to generate text.

```
model.generate('The').then((text) => {
  console.log(text);
});
```

## Additional Information

- For more information on TensorFlow.js, see the TensorFlow.js documentation (https://js.tensorflow.org/).
- For more information on Node.js, see the Node.js documentation (https://nodejs.org/en/docs/).