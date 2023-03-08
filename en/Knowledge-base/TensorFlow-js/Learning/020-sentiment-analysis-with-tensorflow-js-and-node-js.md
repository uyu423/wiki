---
title: 020: Sentiment Analysis with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T11:36:33.947Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:36:29.276Z
---

- [020: Análisis de sentimiento con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/020-sentiment-analysis-with-tensorflow-js-and-node-js)
{.links-list}
- [020：使用 TensorFlow.js 和 Node.js 进行情感分析***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/020-sentiment-analysis-with-tensorflow-js-and-node-js)
{.links-list}
- [020: TensorFlow.js 및 Node.js를 사용한 감정 분석***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/020-sentiment-analysis-with-tensorflow-js-and-node-js)
{.links-list}


#020: Sentiment Analysis with TensorFlow.js and Node.js

##Introduction

In this post, we'll be covering how to do sentiment analysis with TensorFlow.js and Node.js. Sentiment analysis is a process of computationally determining whether a piece of writing is positive, negative, or neutral. It's often used to gauge public opinion on social media, and has a wide range of other applications.

We'll be using the TensorFlow.js library, which is a JavaScript library for training and deploying machine learning models. TensorFlow.js can be used in a Node.js environment, which we'll be using for our sentiment analysis.

##Getting Started

Before we get started, there are a few things you'll need to set up. Firstly, you'll need to have Node.js installed on your machine. You can download it from the [Node.js website](https://nodejs.org/en/).

Once you have Node.js installed, you'll need to install the TensorFlow.js library. You can do this with the following command:

```
npm install @tensorflow/tfjs
```

Next, you'll need to create a new file for our sentiment analysis program. We'll call it `sentiment.js`. You can do this with your favorite text editor.

##Initializing the TensorFlow.js Environment

The first thing we need to do in our `sentiment.js` file is to initialize the TensorFlow.js environment. We can do this with the following code:

```javascript
const tf = require('@tensorflow/tfjs');
```

This will load the TensorFlow.js library into our program so that we can use it.

##Loading the Dataset

Now that we have the TensorFlow.js environment set up, we need to load the dataset that we'll be using for training our sentiment analysis model. We'll be using the [IMDB movie review dataset](https://ai.stanford.edu/~amaas/data/sentiment/). This dataset contains 50,000 movie reviews, each with a label of 0 (negative) or 1 (positive).

We can load this dataset into our program with the following code:

```javascript
const dataset = tf.data.csv('https://storage.googleapis.com/tfjs-datasets/imdb_reviews.csv');
```

This will load the dataset into a `dataset` variable.

##Preprocessing the Dataset

Before we can use the dataset for training, we need to preprocess it. This involves splitting the dataset into training and testing sets, and converting the text data into numerical vectors.

We can do this with the following code:

```javascript
const [train, test] = dataset.split(0.8);

const vectorizer = new tf.layers.Embedding(10000, 16);

const trainX = train.map(example => vectorizer.apply(example.text));
const testX = test.map(example => vectorizer.apply(example.text));
const trainY = train.map(example => example.label);
const testY = test.map(example => example.label);
```

This code will split the dataset into training and testing sets, and then vectorize the text data. The vectorized data will be stored in the `trainX` and `testX` variables for the training and testing sets, respectively. The labels for the training and testing sets will be stored in the `trainY` and `testY` variables, respectively.

##Building the Model

Now that we have our dataset preprocessed, we can build the model that we'll be using for sentiment analysis. We'll be using a simple neural network with one hidden layer.

We can build the model with the following code:

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({ units: 16, activation: 'relu', inputShape: [16] }));
model.add(tf.layers.dense({ units: 1, activation: 'sigmoid' }));
model.compile({ loss: 'binaryCrossentropy', optimizer: 'adam' });
```

This code will create a new `sequential` model, and then add a hidden layer and an output layer to the model. The hidden layer will have 16 units, and the output layer will have one unit. The model will be compiled with the `binaryCrossentropy` loss function and the `adam` optimizer.

##Training the Model

Now that we have our model built, we can train it on our dataset. We'll train it for 10 epochs, which means that the model will see the training data 10 times.

We can train the model with the following code:

```javascript
model.fit(trainX, trainY, { epochs: 10 })
  .then(() => {
    // evaluate the model on the test set
  });
```

This code will train the model on the training set, and then evaluate it on the test set.

##Evaluating the Model

Once the model has been trained, we can evaluate its performance on the test set. We'll use the `model.evaluate()` method to do this.

We can evaluate the model with the following code:

```javascript
model.evaluate(testX, testY)
  .then(results => {
    // log the results
  });
```

This code will evaluate the model on the test set and print the results.

##Making Predictions

Now that we have a trained model, we can use it to make predictions on new data. To do this, we'll use the `model.predict()` method.

We can make predictions with the following code:

```javascript
const prediction = model.predict(tf.tensor2d([[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16]]));
prediction.print();
```

This code will make a prediction on the data `[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16]`. The `print()` method will print the prediction to the console.

##Conclusion

In this post, we covered how to do sentiment analysis with TensorFlow.js and Node.js. We covered how to load and preprocess the dataset, build the model, train the model, and make predictions with the model.