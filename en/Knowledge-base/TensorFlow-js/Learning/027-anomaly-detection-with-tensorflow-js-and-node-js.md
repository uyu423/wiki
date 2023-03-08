---
title: 027: Anomaly Detection with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T13:17:51.909Z
tags: 
editor: markdown
dateCreated: 2023-02-02T13:17:47.458Z
---

- [027: Detección de anomalías con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/027-anomaly-detection-with-tensorflow-js-and-node-js)
{.links-list}
- [027：使用 TensorFlow.js 和 Node.js 进行异常检测***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/027-anomaly-detection-with-tensorflow-js-and-node-js)
{.links-list}
- [027: TensorFlow.js 및 Node.js를 사용한 이상 감지***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/027-anomaly-detection-with-tensorflow-js-and-node-js)
{.links-list}


# Anomaly Detection with TensorFlow.js and Node.js

In this post, we'll be looking at how to build anomaly detection models with TensorFlow.js and Node.js. We'll be using a dataset of daily temperature readings from the past 140 years, which we'll split into training and testing sets.

We'll be using the TensorFlow.js library to build and train our models. TensorFlow.js is a JavaScript library for training and deploying machine learning models. Node.js is a JavaScript runtime that allows us to run JavaScript code outside of the browser.

We'll be using the Sequential model API from TensorFlow.js. Sequential models are a type of neural network that are composed of a linear stack of layers.

## Prerequisites

Before we get started, there are a few things you'll need:

- A text editor. I recommend [Visual Studio Code](https://code.visualstudio.com/).
- [Node.js](https://nodejs.org/en/) installed on your computer.
- A basic understanding of JavaScript.

## Getting the Data

The first step is to get the data. We'll be using a dataset of daily temperature readings from the past 140 years. The dataset is available [here](https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data).

Download the dataset and unzip it. You should now have a folder called `GlobalLandTemperaturesByCountry`.

## Preparing the Data

The next step is to prepare the data. We'll need to split the dataset into training and testing sets. We'll also need to normalize the data, which means scaling the data so that it is between 0 and 1.

We'll be using the [`normalize-dataset`](https://www.npmjs.com/package/normalize-dataset) package to help us with this. Install it by running the following command:

```
npm install --save normalize-dataset
```

Create a new file called `prepare-data.js` and add the following code:

```javascript
const fs = require('fs');
const path = require('path');
const normalizeDataset = require('normalize-dataset');

const dataPath = path.join(__dirname, 'GlobalLandTemperaturesByCountry.csv');
const data = fs.readFileSync(dataPath, 'utf8');

// Split the data into training and testing sets
const [train, test] = normalizeDataset.splitDataset(data, 0.8);

// Save the training and testing sets to files
fs.writeFileSync(path.join(__dirname, 'train.csv'), train);
fs.writeFileSync(path.join(__dirname, 'test.csv'), test);
```

Run the code by running the following command:

```
node prepare-data.js
```

You should now have two new files in your project: `train.csv` and `test.csv`. These are the training and testing sets that we'll be using to train and test our models.

## Building the Model

Now that we have our data, we can start building our model. We'll be using the Sequential model API from TensorFlow.js. Sequential models are a type of neural network that are composed of a linear stack of layers.

Create a new file called `model.js` and add the following code:

```javascript
const tf = require('@tensorflow/tfjs');

// Create a sequential model
const model = tf.sequential();

// Add a single hidden layer
model.add(tf.layers.dense({ units: 1, inputShape: [1] }));

// Add an output layer
model.add(tf.layers.dense({ units: 1, activation: 'sigmoid' }));

// Compile the model
model.compile({
  loss: 'binaryCrossentropy',
  optimizer: 'adam'
});

module.exports = model;
```

In the code above, we've created a sequential model with one hidden layer and one output layer. We've also compiled the model using the `binaryCrossentropy` loss function and the `adam` optimizer.

## Training the Model

Now that we have our model, we need to train it. We'll do this by providing the model with the training set that we prepared earlier.

Create a new file called `train.js` and add the following code:

```javascript
const tf = require('@tensorflow/tfjs');
const fs = require('fs');
const path = require('path');

const model = require('./model');

// Read the training set from a file
const trainPath = path.join(__dirname, 'train.csv');
const trainData = tf.data.csv(trainPath, {
  columnConfigs: {
    label: {
      isLabel: true
    }
  }
});

// Train the model
model.fitDataset(trainData, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    }
  }
});
```

In the code above, we've read the training set from a file and passed it into the `fitDataset` function. This function will train the model for 10 epochs. An epoch is one iteration over the entire training set.

We've also configured the `onEpochEnd` callback to log the loss after each epoch. The loss is a measure of how well the model is performing. We want the loss to be as low as possible.

## Testing the Model

Now that we've trained our model, we need to test it. We'll do this by providing the model with the testing set that we prepared earlier.

Create a new file called `test.js` and add the following code:

```javascript
const tf = require('@tensorflow/tfjs');
const fs = require('fs');
const path = require('path');

const model = require('./model');

// Read the testing set from a file
const testPath = path.join(__dirname, 'test.csv');
const testData = tf.data.csv(testPath, {
  columnConfigs: {
    label: {
      isLabel: true
    }
  }
});

// Evaluate the model
model.evaluateDataset(testData).then(results => {
  console.log(`Loss: ${results.loss}`);
});
```

In the code above, we've read the testing set from a file and passed it into the `evaluateDataset` function. This function will evaluate the model and return the loss.

## Conclusion

In this post, we've seen how to build anomaly detection models with TensorFlow.js and Node.js. We've prepared the data, built the model, and trained and tested the model.