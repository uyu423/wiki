---
title: 045: Stochastic Gradient Descent (SGD) with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T17:36:43.491Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:36:41.307Z
---

- [045: descenso de gradiente estocástico (SGD) con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/045-stochastic-gradient-descent-sgd-with-tensorflow-js-and-node-js)
{.links-list}
- [045：使用 TensorFlow.js 和 Node.js 的随机梯度下降 (SGD)***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/045-stochastic-gradient-descent-sgd-with-tensorflow-js-and-node-js)
{.links-list}
- [045: TensorFlow.js 및 Node.js를 사용한 Stochastic Gradient Descent(SGD)***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/045-stochastic-gradient-descent-sgd-with-tensorflow-js-and-node-js)
{.links-list}


# Stochastic Gradient Descent (SGD) with TensorFlow.js and Node.js

Stochastic gradient descent (SGD) is a widely used optimization method for training deep learning models. SGD works by iteratively updating the weights of a model in the direction that minimizes the cost function.

TensorFlow.js is a JavaScript library for training and deploying machine learning models in the browser or on Node.js. In this tutorial, we'll show how to use TensorFlow.js and SGD to train a simple linear regression model.

## Getting Started

First, let's install TensorFlow.js and its dependencies. We'll need Node.js and npm installed to do this.

    $ npm install @tensorflow/tfjs @tensorflow/tfjs-node

Next, we'll need to create a file for our code. We'll call it `sgd.js`.

## The Data

We'll be using a very simple dataset for this tutorial. It consists of just two columns: `x` and `y`. `x` is a list of numbers from 1 to 100, and `y` is a list of the squares of those numbers.

We can generate this dataset easily with TensorFlow.js:

```javascript
const xs = tf.range(1, 100, 1);
const ys = xs.square();
```

## The Model

Our model will be a very simple linear regression model. Linear regression models are used to predict a continuous value, like a price or a quantity.

Our model will have just one weight and one bias:

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({ units: 1, inputShape: [1] }));
```

## The Cost Function

The cost function is a measure of how well our model is doing. We want to minimize the cost function, which means we want to find the set of weights and biases that make our model's predictions as close to the actual values as possible.

There are many different cost functions that can be used for linear regression. For this tutorial, we'll use the mean squared error cost function:

```javascript
function meanSquaredError(labels, predictions) {
  const error = labels.sub(predictions).square().mean();
  return error;
}
```

## The Optimizer

The optimizer is the algorithm that we use to update the weights and biases of our model. SGD is a popular choice for optimizers, but there are many others to choose from.

For this tutorial, we'll use the SGD optimizer with a learning rate of 0.1:

```javascript
const optimizer = tf.train.sgd(0.1);
```

## Training the Model

Now that we have our data, our model, our cost function, and our optimizer, we're ready to train our model.

Training a model in TensorFlow.js is easy. We just need to call the `fit` method on our model, passing in our data and the number of epochs (iterations) that we want to train for:

```javascript
model.fit(xs, ys, {
  epochs: 100,
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    }
  }
});
```

## Evaluating the Model

Once the model is trained, we can evaluate it on new data. For this tutorial, we'll generate a new dataset with `x` values from 1 to 10 and `y` values from 1 to 100.

```javascript
const xs = tf.range(1, 10, 1);
const ys = tf.range(1, 100, 1);
```

We can use the `predict` method to make predictions on this new data:

```javascript
const predictions = model.predict(xs);
```

Finally, we can compare the predictions to the actual values to see how well our model did:

```javascript
predictions.print();
ys.print();
```

## Additional Information

- [TensorFlow.js Documentation](https://js.tensorflow.org/)
- [Linear Regression Tutorial](https://machinelearningmastery.com/linear-regression-tutorial-machine-learning/)
- [SGD Optimizer Documentation](https://www.tensorflow.org/api_docs/python/tf/train/GradientDescentOptimizer)