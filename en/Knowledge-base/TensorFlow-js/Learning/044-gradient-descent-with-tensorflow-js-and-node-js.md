---
title: 044: Gradient Descent with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T17:18:36.824Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:18:32.062Z
---

- [044: Descenso de gradiente con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/044-gradient-descent-with-tensorflow-js-and-node-js)
{.links-list}
- [044：使用 TensorFlow.js 和 Node.js 进行梯度下降***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/044-gradient-descent-with-tensorflow-js-and-node-js)
{.links-list}
- [044: TensorFlow.js 및 Node.js를 사용한 경사 하강법***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/044-gradient-descent-with-tensorflow-js-and-node-js)
{.links-list}


# 044: Gradient Descent with TensorFlow.js and Node.js

Gradient descent is a optimization algorithm used to find the values of parameters (such as weights and biases) that minimize a cost function. It is a popular algorithm for training neural networks.

TensorFlow.js is a JavaScript library for training and deploying machine learning models. Node.js is a JavaScript runtime that allows you to run JavaScript code on a server.

In this tutorial, we will use TensorFlow.js and Node.js to train a simple neural network to perform linear regression. We will use gradient descent to find the optimal values for the weights and biases of the network.

## What is Linear Regression?

Linear regression is a machine learning algorithm used to predict a continuous value. For example, we could use linear regression to predict the price of a house based on its size, number of bedrooms, and number of bathrooms.

Linear regression is a type of supervised learning, which means we need to provide the algorithm with training data. The training data consists of a set of input values (x) and the corresponding output values (y). For our house price example, the input values could be the size, number of bedrooms, and number of bathrooms, and the output value would be the price.

## How Does Linear Regression Work?

Linear regression works by finding a set of weights (w) and biases (b) that minimize the error between the predicted values (ŷ) and the actual values (y).

![Linear Regression](https://cdn-images-1.medium.com/max/1600/1*d7Cg5UC5tM7GtLjTvW0MzA.png)

The predicted values are calculated by taking the input values (x) and multiplying them by the weights (w), and then adding the biases (b).

![Predicted Values](https://cdn-images-1.medium.com/max/1600/1*j_q-F1lrVxKbV-_d7JKV2w.png)

The error is calculated by taking the difference between the predicted values (ŷ) and the actual values (y).

![Error](https://cdn-images-1.medium.com/max/1600/1*7VtEOzAj_sXXuTzXrT7yYQ.png)

We can then use gradient descent to find the weights and biases that minimize the error.

## What is Gradient Descent?

Gradient descent is an optimization algorithm used to find the values of parameters (such as weights and biases) that minimize a cost function.

![Cost Function](https://cdn-images-1.medium.com/max/1600/1*Xu7B5y9gp0iL5ooBj7LtWw.png)

The cost function is a measure of how far the predicted values (ŷ) are from the actual values (y). We want to find the weights and biases that minimize the cost function.

![Weights and Biases](https://cdn-images-1.medium.com/max/1600/1*n6sVxWAz7VUgX6Sj7K1vUw.png)

Gradient descent works by iteratively updating the weights and biases in the direction that minimizes the cost function. The size of the update is determined by the learning rate.

![Gradient Descent](https://cdn-images-1.medium.com/max/1600/1*jw7UwKLnA0sCgq_QPV-_lA.png)

## Implementing Gradient Descent in TensorFlow.js

Now that we've seen how gradient descent works, let's see how to implement it in TensorFlow.js.

First, we need to define the input values (x), the output values (y), and the initial values for the weights (w) and biases (b).

```javascript
// Define the input values
const x = tf.tensor([
  [1, 2, 3, 4],
  [2, 3, 4, 5],
  [3, 4, 5, 6],
  [4, 5, 6, 7]
]);

// Define the output values
const y = tf.tensor([
  [2],
  [4],
  [6],
  [8]
]);

// Define the initial values for the weights and biases
const w = tf.variable(tf.zeros([4, 1]));
const b = tf.variable(tf.zeros([1]));
```

Next, we need to define the cost function. We will use the mean squared error cost function.

```javascript
// Define the cost function
function cost(pred, labels) {
  const diff = pred.sub(labels);
  const sqrDiff = diff.square();
  const meanSqrDiff = sqrDiff.mean();
  return meanSqrDiff;
}
```

Now, we can define the gradient descent algorithm. We will iteratively update the weights and biases in the direction that minimizes the cost function.

```javascript
// Define the gradient descent algorithm
async function train(x, y, w, b, epochs, learningRate) {
  for (let i = 0; i < epochs; i++) {
    // Calculate the predicted values
    const pred = x.matMul(w).add(b);

    // Calculate the cost
    const c = cost(pred, y);

    // Print the cost
    console.log("Epoch: " + i + " Cost: " + c.dataSync()[0]);

    // Calculate the gradients
    const grads = tf.grads(c, [w, b]);
    const dw = grads[0];
    const db = grads[1];

    // Update the weights and biases
    w.sub(dw.mul(learningRate));
    b.sub(db.mul(learningRate));
  }
}
```

Finally, we can call the `train` function to train the model. We will train the model for 100 epochs with a learning rate of 0.1.

```javascript
// Train the model
train(x, y, w, b, 100, 0.1);
```

## Training the Model

Now that we've seen how to implement gradient descent in TensorFlow.js, let's see how to use it to train a neural network to perform linear regression.

First, we need to define the input values (x), the output values (y), and the initial values for the weights (w) and biases (b).

```javascript
// Define the input values
const x = tf.tensor([
  [1, 2, 3, 4],
  [2, 3, 4, 5],
  [3, 4, 5, 6],
  [4, 5, 6, 7]
]);

// Define the output values
const y = tf.tensor([
  [2],
  [4],
  [6],
  [8]
]);

// Define the initial values for the weights and biases
const w = tf.variable(tf.zeros([4, 1]));
const b = tf.variable(tf.zeros([1]));
```

Next, we need to define the cost function. We will use the mean squared error cost function.

```javascript
// Define the cost function
function cost(pred, labels) {
  const diff = pred.sub(labels);
  const sqrDiff = diff.square();
  const meanSqrDiff = sqrDiff.mean();
  return meanSqrDiff;
}
```

Now, we can define the gradient descent algorithm. We will iteratively update the weights and biases in the direction that minimizes the cost function.

```javascript
// Define the gradient descent algorithm
async function train(x, y, w, b, epochs, learningRate) {
  for (let i = 0; i < epochs; i++) {
    // Calculate the predicted values
    const pred = x.matMul(w).add(b);

    // Calculate the cost
    const c = cost(pred, y);

    // Print the cost
    console.log("Epoch: " + i + " Cost: " + c.dataSync()[0]);

    // Calculate the gradients
    const grads = tf.grads(c, [w, b]);
    const dw = grads[0];
    const db = grads[1];

    // Update the weights and biases
    w.sub(dw.mul(learningRate));
    b.sub(db.mul(learningRate));
  }
}
```

Finally, we can call the `train` function to train the model. We will train the model for 100 epochs with a learning rate of 0.1.

```javascript
// Train the model
train(x, y, w, b, 100, 0.1);
```

## Testing the Model

Now that we've trained the model, let's see how it performs on some test data.

First, we need to define the test data.

```javascript
// Define the test data
const xTest = tf.tensor([
  [5, 6, 7, 8],
  [6, 7, 8, 9],
  [7, 8, 9, 10],
  [8, 9, 10, 11]
]);

// Define the expected output values
const yTest = tf.tensor([
  [10],
  [12],
  [14],
  [16]
]);
```

Next, we need to calculate the predicted values.

```javascript
// Calculate the predicted values
const pred = xTest.matMul(w).add(b);
```

Finally, we can compare the predicted values to the expected output values.

```javascript
// Compare the predicted values to the expected output values
pred.print();
yTest.print();
```

## Conclusion

In this tutorial, we've seen how to use gradient descent to train a neural network to perform linear regression. We've also seen how to implement gradient descent in TensorFlow.js and how to use it to train a neural network.