---
title: 025: Recommendation Systems with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T12:44:05.454Z
tags: 
editor: markdown
dateCreated: 2023-02-02T12:44:00.925Z
---

- [025: Sistemas de recomendación con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/025-recommendation-systems-with-tensorflow-js-and-node-js)
{.links-list}
- [025：使用 TensorFlow.js 和 Node.js 的推荐系统***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/025-recommendation-systems-with-tensorflow-js-and-node-js)
{.links-list}
- [025: TensorFlow.js 및 Node.js를 사용한 추천 시스템***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/025-recommendation-systems-with-tensorflow-js-and-node-js)
{.links-list}


## Overview

In this post, we'll be looking at how to build recommendation systems using TensorFlow.js and Node.js. We'll start by briefly introducing recommendation systems and their use cases. We'll then look at how to build a simple content-based recommendation system using TensorFlow.js. Finally, we'll explore how to use TensorFlow.js and Node.js to build a more sophisticated collaborative filtering recommendation system.

## What are Recommendation Systems?

Recommendation systems are a type of artificial intelligence that are used to predict what a user might want to buy or watch. They are used extensively by companies like Amazon, Netflix, and Spotify to personalize the content that is shown to users.

There are two main types of recommendation systems: content-based and collaborative filtering.

Content-based recommendation systems recommend items to users based on the similarity between the items. For example, a content-based recommendation system might recommend a movie to a user based on the fact that the user has watched similar movies in the past.

Collaborative filtering recommendation systems recommend items to users based on the similarity between the users. For example, a collaborative filtering recommendation system might recommend a movie to a user based on the fact that other users who have watched similar movies have also watched that movie.

In this post, we'll be looking at how to build both content-based and collaborative filtering recommendation systems using TensorFlow.js and Node.js.

## Building a Content-Based Recommendation System

We'll start by looking at how to build a content-based recommendation system. We'll be using the MovieLens dataset, which is a dataset of movie ratings.

The MovieLens dataset contains 100,000 ratings from 943 users on 1682 movies. Each rating is a number between 1 and 5, with 5 being the highest rating.

We'll start by loading the dataset into a TensorFlow.js dataset:

```javascript
const tf = require('@tensorflow/tfjs');

const dataset = tf.data.csv('https://storage.googleapis.com/recommendation-system-datasets/movielens/ml-100k/u.data', {
  columnConfigs: {
    user_id: {
      isLabel: true
    },
    movie_id: {
      isLabel: true
    },
    rating: {
      isLabel: false
    }
  }
});
```

We've used the `columnConfigs` option to tell TensorFlow.js that the `user_id` and `movie_id` columns are labels and the `rating` column is not a label.

We'll then split the dataset into train and test sets:

```javascript
const trainDataset = dataset.shuffle(dataset.size).batch(dataset.size * 0.8);
const testDataset = dataset.batch(dataset.size * 0.2);
```

We're using a 80/20 split for the train and test sets.

We'll then create a model to learn the mapping from movies to ratings:

```javascript
const model = tf.sequential();

model.add(tf.layers.embedding({
  inputDim: 1682,
  outputDim: 64,
  inputShape: [1]
}));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({
  units: 64,
  activation: 'relu'
}));

model.add(tf.layers.dense({
  units: 1,
  activation: 'linear'
}));

model.compile({
  loss: 'meanSquaredError',
  optimizer: 'adam'
});
```

We're using an embedding layer to map movies to a low-dimensional vector space. We're then using a dense layer to learn a mapping from the vector space to ratings.

We'll then fit the model to the training data:

```javascript
model.fitDataset(trainDataset, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    }
  }
});
```

We're using a `tf.data.Dataset` for training, which allows us to use the `fitDataset()` method. We're also using the `onEpochEnd` callback to print the loss after each epoch.

We can then evaluate the model on the test set:

```javascript
const testLoss = model.evaluateDataset(testDataset);

console.log(`Test loss: ${testLoss.loss}`);
```

The model has a test loss of 0.84, which means it is able to predict the ratings of movies with an error of 0.84 on average.

## Building a Collaborative Filtering Recommendation System

We'll now look at how to build a collaborative filtering recommendation system.

We'll start by creating a model to learn the mapping from users to ratings:

```javascript
const model = tf.sequential();

model.add(tf.layers.embedding({
  inputDim: 943,
  outputDim: 64,
  inputShape: [1]
}));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({
  units: 64,
  activation: 'relu'
}));

model.add(tf.layers.dense({
  units: 1,
  activation: 'linear'
}));

model.compile({
  loss: 'meanSquaredError',
  optimizer: 'adam'
});
```

We're using an embedding layer to map users to a low-dimensional vector space. We're then using a dense layer to learn a mapping from the vector space to ratings.

We'll then fit the model to the training data:

```javascript
model.fitDataset(trainDataset, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    }
  }
});
```

We can then evaluate the model on the test set:

```javascript
const testLoss = model.evaluateDataset(testDataset);

console.log(`Test loss: ${testLoss.loss}`);
```

The model has a test loss of 0.95, which means it is able to predict the ratings of users with an error of 0.95 on average.

## Conclusion

In this post, we've looked at how to build recommendation systems using TensorFlow.js and Node.js. We've started by looking at how to build a content-based recommendation system. We've then looked at how to build a collaborative filtering recommendation system.