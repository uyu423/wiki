---
title: 050: Adam Optimization with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T18:36:31.002Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:36:26.416Z
---

- [050: Optimización de Adam con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/050-adam-optimization-with-tensorflow-js-and-node-js)
{.links-list}
- [050：使用 TensorFlow.js 和 Node.js 进行 Adam 优化***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/050-adam-optimization-with-tensorflow-js-and-node-js)
{.links-list}
- [050: TensorFlow.js 및 Node.js를 사용한 Adam 최적화***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/050-adam-optimization-with-tensorflow-js-and-node-js)
{.links-list}


# Adam Optimization with TensorFlow.js and Node.js

In this post, we'll explore how to use the Adam optimization algorithm with TensorFlow.js and Node.js. Adam is an optimization algorithm that can be used to train neural networks. Adam is a combination of the AdaGrad and RMSProp optimization algorithms.

Adam optimization is a computationally efficient method of training neural networks. Adam is well suited for training deep neural networks. Adam can be used with any differentiable loss function.

## Getting Started

To get started, we'll need to install the TensorFlow.js and Node.js dependencies. We can install TensorFlow.js and Node.js using the following commands:

```
npm install @tensorflow/tfjs
npm install node
```

## Defining the Model

Next, we need to define the model that we want to train. We'll use a simple neural network with one hidden layer. The hidden layer will have 100 neurons. We can define the model using the following code:

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({units: 100, inputShape: [1], activation: 'relu'}));
model.add(tf.layers.dense({units: 1, activation: 'linear'}));
```

## Compiling the Model

After we have defined the model, we need to compile it. Compiling the model allows us to specify the optimizer and loss function that we want to use. We'll use the Adam optimizer and the mean squared error loss function. We can compile the model using the following code:

```javascript
model.compile({optimizer: 'adam', loss: 'meanSquaredError'});
```

## Training the Model

Now that we have compiled the model, we can train it. We'll train the model for 10 epochs. An epoch is one iteration over the entire training dataset. We can train the model using the following code:

```javascript
model.fit(x, y, {epochs: 10});
```

## Evaluating the Model

After the model has been trained, we can evaluate it. We'll evaluate the model on a test dataset. We can evaluate the model using the following code:

```javascript
model.evaluate(xTest, yTest);
```

## Making Predictions

Finally, we can use the trained model to make predictions. We'll make predictions on a new dataset. We can make predictions using the following code:

```javascript
model.predict(xPred);
```

## Conclusion

In this post, we've seen how to use the Adam optimization algorithm with TensorFlow.js and Node.js. Adam is an efficient optimization algorithm that can be used to train neural networks. Adam can be used with any differentiable loss function.