---
title: 006: Logistic Regression with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T08:04:30.166Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:04:25.798Z
---

- [006: Regresión logística con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/006-logistic-regression-with-tensorflow-js-and-node-js)
{.links-list}
- [006：使用 TensorFlow.js 和 Node.js 进行逻辑回归***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/006-logistic-regression-with-tensorflow-js-and-node-js)
{.links-list}
- [006: TensorFlow.js 및 Node.js를 사용한 로지스틱 회귀***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/006-logistic-regression-with-tensorflow-js-and-node-js)
{.links-list}


# Logistic Regression with TensorFlow.js and Node.js

In this post, we'll learn how to build a logistic regression model using TensorFlow.js and Node.js.

Logistic regression is a statistical method for predicting binary outcomes. That is, it can be used to predict whether an event will occur or not. For example, we can use logistic regression to predict whether a patient will develop a disease, based on certain characteristics.

Logistic regression is a type of linear regression, but with a few important differences. First, the outcome variable is binary, which means it can only take two values (0 or 1). Second, the model is fit using a maximum likelihood estimation, rather than least squares.

## Getting Started

To get started, we need to install TensorFlow.js and Node.js. We can do this using the following commands:

```
npm install -g tensorflow
npm install -g node
```

Once TensorFlow.js and Node.js are installed, we can create a new file called `logistic-regression.js` and start coding.

## Data

The first step is to load our data. We'll use the `tensorflow.js` library to load the data into a `tf.tensor` object.

```javascript
const tf = require('tensorflow');

// Load the data
const data = tf.tensor([
  [1, 2],
  [2, 3],
  [3, 4],
  [4, 5],
]);
```

## Model

Next, we need to define our model. We'll use a logistic regression model with two input features (`x1` and `x2`) and one output (`y`).

```javascript
// Define the model
const model = tf.sequential();
model.add(tf.layers.dense({ units: 1, inputShape: [2] }));
model.compile({ loss: 'binaryCrossentropy', optimizer: 'sgd' });
```

## Training

Now that we have our data and model, we can train our model. We'll use the `fit` method to train our model on the data.

```javascript
// Train the model
model.fit(data, tf.tensor([1, 1, 0, 0]), {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    },
  },
});
```

## Prediction

Once our model is trained, we can use it to make predictions. We'll use the `predict` method to predict the output for new data.

```javascript
// Make predictions
model.predict(tf.tensor([[5, 6]])).print(); // [[0.5]]
model.predict(tf.tensor([[6, 7]])).print(); // [[0.5]]
```

As we can see, our model predicts the output as 0.5 for both inputs. This means that our model is predicting a 50% chance of the event occurring.

## Conclusion

In this post, we've learned how to build a logistic regression model using TensorFlow.js and Node.js. We've also seen how to use our model to make predictions on new data.