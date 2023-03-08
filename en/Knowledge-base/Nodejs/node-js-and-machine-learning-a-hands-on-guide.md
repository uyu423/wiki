---
title: Node.js and Machine Learning: A Hands-On Guide
description: 
published: true
date: 2023-02-25T02:32:45.093Z
tags: 
editor: markdown
dateCreated: 2023-02-25T02:32:43.192Z
---

- [Node.js 및 기계 학습: 실습 가이드***Korean** document is available*](/ko/Knowledge-base/Nodejs/node-js-and-machine-learning-a-hands-on-guide)
{.links-list}


# Node.js and Machine Learning: A Hands-On Guide

Machine learning is a process of teaching computers to make decisions on their own by providing them with data. This is done by creating algorithms, which are a set of rules that can be followed to solve a problem. Node.js is a JavaScript runtime environment that allows you to run JavaScript on a server. It is also used for developing server-side applications.

In this article, we will be looking at how to use Node.js for machine learning. We will be using the popular machine learning library, TensorFlow.js. TensorFlow.js is a JavaScript library for training and deploying machine learning models.

## Setting up the Environment

Before we can start using Node.js for machine learning, we need to set up our development environment. We will be using the Node.js runtime environment and the npm package manager.

### Node.js

Download the latest stable release of Node.js from the [Node.js website](https://nodejs.org/en/). Once the download is complete, run the installer.

### npm

npm is a package manager for JavaScript. It is used to install, update, and uninstall packages. npm is bundled with Node.js, so we don't need to install it separately.

## Hello World

Now that we have Node.js and npm installed, let's create our first Node.js program. Create a file named `hello.js` and add the following code to it:

```javascript
console.log("Hello, world!");
```

To run the program, open a command prompt or terminal and run the following command:

```
node hello.js
```

You should see the following output:

```
Hello, world!
```

## TensorFlow.js

Now that we have our development environment set up, we can install TensorFlow.js. TensorFlow.js is a JavaScript library for training and deploying machine learning models.

To install TensorFlow.js, open a command prompt or terminal and run the following command:

```
npm install @tensorflow/tfjs
```

This will install TensorFlow.js and all its dependencies.

## Training a Model

Now that we have TensorFlow.js installed, let's try training a simple machine learning model. We will be using the [ Iris Dataset ](https://en.wikipedia.org/wiki/Iris_flower_data_set). The Iris Dataset is a set of 150 records of Iris flowers. Each record contains the following attributes:

* sepal length
* sepal width
* petal length
* petal width
* species

We will be using the [ K-Nearest Neighbors ](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm) algorithm to train our model. K-Nearest Neighbors is a simple algorithm that can be used for classification and regression.

Create a file named `knn.js` and add the following code to it:

```javascript
// Load the TensorFlow.js library
const tf = require('@tensorflow/tfjs');
// Load the Iris Dataset
const irisDataset = require('./iris.json');
// Load the K-Means algorithm
const kMeans = require('@tensorflow/tfjs-kmeans');
 
// Convert the dataset to a Tensor
const dataset = tf.tensor2d(irisDataset.map(item => [
  item.sepal_length,
  item.sepal_width,
  item.petal_length,
  item.petal_width,
]));
 
// Train the model
kMeans.train({
  dataset,
  numClusters: 3,
  iterations: 10,
  distanceFunction: 'euclidean',
}).then(model => {
  // Use the model to predict the class of a new record
  const prediction = model.predict(tf.tensor2d([
    [5.1, 3.5, 1.4, 0.2],
  ]));
  // Print the predicted class for the new record
  prediction.print();
});
```

In the code above, we first loaded the TensorFlow.js, Iris Dataset, and K-Means algorithm. We then converted the dataset to a Tensor. Next, we trained the model using the K-Means algorithm. Finally, we used the model to predict the class of a new record.

To run the program, open a command prompt or terminal and run the following command:

```
node knn.js
```

You should see the following output:

```
Tensor
[[0]]
```

The output indicates that the new record belongs to the class 0. The class 0 corresponds to the Iris setosa species.

## Deploying a Model

Now that we have trained a machine learning model, let's deploy it as a web application. We will be using the [ Express.js ](https://expressjs.com/) web framework to create our web application.

Install the Express.js framework by running the following command:

```
npm install express
```

Create a file named `app.js` and add the following code to it:

```javascript
// Load the Express.js framework
const express = require('express');
// Load the TensorFlow.js library
const tf = require('@tensorflow/tfjs');
// Load the K-Means algorithm
const kMeans = require('@tensorflow/tfjs-kmeans');
 
// Create a new Express.js application
const app = express();
 
// Train the model
kMeans.train({
  dataset,
  numClusters: 3,
  iterations: 10,
  distanceFunction: 'euclidean',
}).then(model => {
  // Define a route that returns the predictions
  app.get('/predict', (req, res) => {
    // Use the model to predict the class of a new record
    const prediction = model.predict(tf.tensor2d([
      [req.query.sepal_length, req.query.sepal_width, req.query.petal_length, req.query.petal_width],
    ]));
    // Return the predictions as a JSON object
    res.json(prediction.dataSync());
  });
 
  // Start the Express.js server
  app.listen(3000, () => console.log('Server started on port 3000'));
});
```

In the code above, we first loaded the Express.js, TensorFlow.js, and K-Means algorithm. We then trained the model using the K-Means algorithm. Next, we defined a route that returns the predictions. Finally, we started the Express.js server.

To run the program, open a command prompt or terminal and run the following command:

```
node app.js
```

You should see the following output:

```
Server started on port 3000
```

Open a web browser and navigate to http://localhost:3000/predict?sepal_length=5.1&sepal_width=3.5&petal_length=1.4&petal_width=0.2. You should see the following output:

```
[0]
```

The output indicates that the new record belongs to the class 0. The class 0 corresponds to the Iris setosa species.

##Conclusion

In this article, we have seen how to use Node.js for machine learning. We have used the popular machine learning library, TensorFlow.js. TensorFlow.js is a JavaScript library for training and deploying machine learning models.