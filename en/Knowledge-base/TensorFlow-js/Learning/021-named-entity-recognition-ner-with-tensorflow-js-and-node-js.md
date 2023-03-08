---
title: 021: Named Entity Recognition (NER) with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T11:43:43.604Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:43:39.130Z
---

- [021: Reconocimiento de entidad con nombre (NER) con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/021-named-entity-recognition-ner-with-tensorflow-js-and-node-js)
{.links-list}
- [021：使用 TensorFlow.js 和 Node.js 的命名实体识别 (NER)***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/021-named-entity-recognition-ner-with-tensorflow-js-and-node-js)
{.links-list}
- [021: TensorFlow.js 및 Node.js를 사용한 NER(Named Entity Recognition)***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/021-named-entity-recognition-ner-with-tensorflow-js-and-node-js)
{.links-list}


# Named Entity Recognition (NER) with TensorFlow.js and Node.js

In this post, we'll be looking at how to perform named entity recognition (NER) in JavaScript using TensorFlow.js and Node.js. NER is a task in natural language processing (NLP) that involves identifying and classifying named entities in text, such as people, places, organizations, and so on.

We'll be using a pre-trained model that was trained on the CoNLL 2003 NER dataset. The model is a Bidirectional Long Short-Term Memory (BiLSTM) model with a Conditional Random Field (CRF) layer on top.

## Prerequisites

In order to follow along with this post, you'll need the following:

- Node.js (version 8 or higher)
- A text editor or IDE

## Getting Started

First, let's create a new Node.js project. We'll be using the Express web framework, so we'll need to install that as well:

```
npm init
npm install --save express
```

Next, we'll need to install the TensorFlow.js NER model. We can do that with the following command:

```
npm install @tensorflow-models/ner
```

With that, we're now ready to start coding!

## Loading the Model

The first thing we need to do is load the model. We can do that with the following code:

```javascript
const tf = require('@tensorflow/tfjs-node');
const model = require('@tensorflow-models/ner');

async function main() {
  const ner = await model.load();
}

main();
```

In the code above, we first imported TensorFlow.js and the NER model. We then created an async function that will load the model and store it in a variable.

## Predicting Named Entities

Now that we've loaded the model, we can use it to predict named entities in text. We can do that with the following code:

```javascript
const tf = require('@tensorflow/tfjs-node');
const model = require('@tensorflow-models/ner');

async function main() {
  const ner = await model.load();

  const text = 'John Smith is a software engineer at Google.';

  const results = await ner.predict(text);

  console.log(results);
}

main();
```

In the code above, we've added a string of text that we want to predict the named entities for. We've then used the model's `predict` method to get the results.

The results will be an array of objects, each of which represents a named entity. Each object will have a `start` and `end` property that represents the start and end indices of the named entity in the input text, as well as a `score` property that represents the model's confidence in the prediction.

## Visualizing the Results

It can be helpful to visualize the results of the prediction. We can do that with the following code:

```javascript
const tf = require('@tensorflow/tfjs-node');
const model = require('@tensorflow-models/ner');

async function main() {
  const ner = await model.load();

  const text = 'John Smith is a software engineer at Google.';

  const results = await ner.predict(text);

  for (const result of results) {
    console.log(
        `${text.substring(result.start, result.end)} (${result.score})`);
  }
}

main();
```

In the code above, we've added a loop that will print out each of the named entities, as well as the model's confidence score for that prediction.

## Conclusion

In this post, we've seen how to perform named entity recognition in JavaScript using TensorFlow.js and Node.js. We've also seen how to visualize the results of the prediction.

If you're interested in learning more about NER or TensorFlow.js, here are some resources that you might find helpful:

- [Named Entity Recognition with TensorFlow (blog post)](https://blog.tensorflow.org/2018/12/named-entity-recognition-ner-tensorflow.html)
- [TensorFlow.js NER model](https://js.tensorflow.org/tutorials/tensorflow-for-js- nerds.html)
- [CoNLL 2003 NER dataset](https://www.clips.uantwerpen.be/conll2003/ner/)