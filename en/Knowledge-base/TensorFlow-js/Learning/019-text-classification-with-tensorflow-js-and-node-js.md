---
title: 019: Text Classification with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T11:19:08.523Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:19:04.021Z
---

- [019: Clasificación de texto con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/019-text-classification-with-tensorflow-js-and-node-js)
{.links-list}
- [019：使用 TensorFlow.js 和 Node.js 进行文本分类***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/019-text-classification-with-tensorflow-js-and-node-js)
{.links-list}
- [019: TensorFlow.js 및 Node.js를 사용한 텍스트 분류***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/019-text-classification-with-tensorflow-js-and-node-js)
{.links-list}


# Text Classification with TensorFlow.js and Node.js

In this post, we'll learn how to build a text classification model using TensorFlow.js and Node.js. Text classification is a common task in natural language processing, which is the process of analyzing and working with human language data.

We'll be using a dataset of movie reviews from the website Rotten Tomatoes. The dataset contains text for each review, as well as a label indicating whether the review is positive or negative. We'll use this dataset to train a model that can read new reviews and predict whether they're positive or negative.

## Prerequisites

Before we get started, there are a few things you'll need:

- Node.js and npm installed on your computer
- A text editor or IDE
- Basic knowledge of JavaScript

## Getting Started

First, we need to create a new Node.js project. Create a new directory for your project and initialize it with npm:

```
mkdir text-classification
cd text-classification
npm init -y
```

This will create a package.json file for your project. Next, we need to install the dependencies we'll be using. We'll be using TensorFlow.js, a library for working with machine learning in JavaScript, and the natural library, which provides some helpful functions for working with human language data.

```
npm install --save @tensorflow/tfjs natural
```

With the dependencies installed, we can now start coding. Create a new file called index.js in your project directory and add the following code:

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here
```

This imports the TensorFlow.js and natural libraries, which we'll be using in the next section.

## Preparing the Data

Before we can train our model, we need to prepare the data. The movie review dataset is in a file called reviews.csv, which you can [download here](https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv).

Add the following code to index.js to load and prepare the data:

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here

// Load the dataset
const csvUrl = 'https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv';
const { data, labels } = tf.data.csv(csvUrl);

// Shuffle the data
const shuffledData = data.shuffle();

// Split the data into training and test sets
const [trainData, testData] = shuffledData.split([0.8, 0.2]);

// Convert the labels to a one-hot encoding
const trainLabels = trainData.map((_, i) => labels[i]).oneHot(2);
const testLabels = testData.map((_, i) => labels[i]).oneHot(2);

// Normalize the data
const trainDataNormalized = trainData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

const testDataNormalized = testData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});
```

Let's take a look at what this code does:

- The first line loads the dataset from a URL. This dataset is in CSV format, so we use the tf.data.csv() function to load it.
- The second line shuffles the data. This is important because we don't want the model to learn the order of the reviews, just the reviews themselves.
- The third line splits the data into a training set and a test set. The training set is used to train the model, and the test set is used to evaluate the model.
- The fourth line converts the labels to a one-hot encoding. This is a common way of representing categorical data in machine learning.
- The fifth and sixth lines normalize the data. This step is important because it ensures that the model doesn't overfit to the training data.

## Building the Model

Now that we have the data prepared, we can build the model. We'll be using a Bidirectional Long Short-Term Memory (BiLSTM) model, which is a type of recurrent neural network (RNN).

Add the following code to index.js to build the model:

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here

// Load the dataset
const csvUrl = 'https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv';
const { data, labels } = tf.data.csv(csvUrl);

// Shuffle the data
const shuffledData = data.shuffle();

// Split the data into training and test sets
const [trainData, testData] = shuffledData.split([0.8, 0.2]);

// Convert the labels to a one-hot encoding
const trainLabels = trainData.map((_, i) => labels[i]).oneHot(2);
const testLabels = testData.map((_, i) => labels[i]).oneHot(2);

// Normalize the data
const trainDataNormalized = trainData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

const testDataNormalized = testData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

// Build the model
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 1000,
  outputDim: 32,
  inputLength: 100
}));
model.add(tf.layers.bidirectional({
  layer: tf.layers.lstm({
    units: 32
  })
}));
model.add(tf.layers.dense({
  units: 2,
  activation: 'softmax'
}));
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

// Train the model
model.fit(trainDataNormalized, trainLabels, {
  epochs: 5,
  validationData: [testDataNormalized, testLabels]
}).then(() => {
  // Evaluate the model
  const results = model.evaluate(testDataNormalized, testLabels);
  console.log(results);
});
```

This code does the following:

- The first line builds the model using a Sequential model. This is a type of model that consists of a linear stack of layers.
- The second line adds an Embedding layer. This layer is used to convert the input data into a vector representation.
- The third line adds a Bidirectional layer. This layer is used to process the data in both directions.
- The fourth line adds a Long Short-Term Memory (LSTM) layer. This layer is used to remember information for long periods of time.
- The fifth line adds a Dense layer. This layer is used to make predictions based on the data.
- The sixth line compiles the model. This step configures the model for training.
- The seventh line trains the model. This step will take a few minutes to complete.
- The eighth line evaluates the model. This step prints the accuracy of the model to the console.

## Making Predictions

Now that we have a trained model, we can use it to make predictions. Add the following code to index.js to make predictions:

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here

// Load the dataset
const csvUrl = 'https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv';
const { data, labels } = tf.data.csv(csvUrl);

// Shuffle the data
const shuffledData = data.shuffle();

// Split the data into training and test sets
const [trainData, testData] = shuffledData.split([0.8, 0.2]);

// Convert the labels to a one-hot encoding
const trainLabels = trainData.map((_, i) => labels[i]).oneHot(2);
const testLabels = testData.map((_, i) => labels[i]).oneHot(2);

// Normalize the data
const trainDataNormalized = trainData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

const testDataNormalized = testData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

// Build the model
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 1000,
  outputDim: 32,
  inputLength: 100
}));
model.add(tf.layers.bidirectional({
  layer: tf.layers.lstm({
    units: 32
  })
}));
model.add(tf.layers.dense({
  units: 2,
  activation: 'softmax'
}));
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

// Train the model
model.fit(trainDataNormalized, trainLabels, {
  epochs: 5,
  validationData: [testDataNormalized, testLabels]
}).then(() => {
  // Evaluate the model
  const results = model.evaluate(testDataNormalized, testLabels);
  console.log(results);
  
  // Make a prediction
  const prediction = model.predict(['this movie was great']);
  console.log(prediction);
});
```

This code does the following:

- The first line loads the dataset from a URL. This dataset is in CSV format, so we use the tf.data.csv() function to load it.
- The second line shuffles the data. This is important because we don't want the model to learn the order of the reviews, just the reviews themselves.
- The third line splits the data into a training set and a test set. The training set is used to train the model, and the test set is used to evaluate the model.
- The fourth line converts the labels to a one-hot encoding. This is a common way of representing categorical data in machine learning.
- The fifth and sixth lines normalize the data. This step is important because it ensures that the model doesn't overfit to the training data.
- The seventh line builds the model using a Sequential model. This is a type of model that consists of a linear stack of layers.
- The eighth line adds an Embedding layer. This layer is used to convert the input data into a vector representation.
- The ninth line adds a Bidirectional layer. This layer is used to process the data in both directions.
- The tenth line adds a Long Short-Term Memory (LSTM) layer. This layer is used to remember information for long periods of time.
- The eleventh line adds a Dense layer. This layer is used to make predictions based on the data.
- The twelfth line compiles the model. This step configures the model for training.
- The thirteenth line trains the model. This step will take a few minutes to complete.
- The fourteenth line evaluates the model. This step prints the accuracy of the model to the console.
- The fifteenth line makes a prediction. This step prints the prediction to the console.

## Conclusion

In this post, we learned how to build a text classification model using TensorFlow.js and Node.js. We started by loading and preparing the data, then we built and trained a model. Finally, we used the model to make predictions.

Text classification is a common task in natural language processing, and this post shows how to build a text classification model using TensorFlow.js and Node.js.