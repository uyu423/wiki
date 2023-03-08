---
title: 095: Building Long Short-Term Memory (LSTM) Networks in TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-03T05:17:58.781Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:17:53.924Z
---

- [095: Creación de redes de memoria a corto plazo (LSTM) en TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/095-building-long-short-term-memory-lstm-networks-in-tensorflow-js-and-node-js)
{.links-list}
- [095：在 TensorFlow.js 和 Node.js 中构建长短期记忆 (LSTM) 网络***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/095-building-long-short-term-memory-lstm-networks-in-tensorflow-js-and-node-js)
{.links-list}
- [095: TensorFlow.js 및 Node.js에서 장단기 기억(LSTM) 네트워크 구축***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/095-building-long-short-term-memory-lstm-networks-in-tensorflow-js-and-node-js)
{.links-list}


# 095: Building Long Short-Term Memory (LSTM) Networks in TensorFlow.js and Node.js

In this post, we'll be looking at how to build Long Short-Term Memory (LSTM) networks in TensorFlow.js and Node.js.

LSTMs are a type of recurrent neural network that are well-suited for working with sequential data. Sequential data is data where each element is dependent on the previous element, such as time series data.

LSTMs are able to learn long-term dependencies by using a "memory" cell that can remember information for long periods of time. LSTMs are also able to handle input elements that are not in the same order as the output elements, which is important for working with time series data.

## Building an LSTM network in TensorFlow.js

We'll start by looking at how to build an LSTM network in TensorFlow.js.

First, we need to install TensorFlow.js. We can do this using the Node.js package manager, npm:

```
npm install @tensorflow/tfjs
```

Next, we need to create a new file called `lstm.js` and import TensorFlow.js:

```javascript
const tf = require('@tensorflow/tfjs');
```

Now we're ready to start building our LSTM network.

We'll start by defining the model:

```javascript
const model = tf.sequential();
```

Next, we'll add an LSTM layer to the model. The first argument to the `tf.layers.lstm` function is the number of units, which is the number of memory cells in the LSTM layer. We'll use 16 units:

```javascript
model.add(tf.layers.lstm({units: 16, inputShape: [1, 1]}));
```

The `inputShape` argument is the shape of the input data. The first element is the number of time steps, and the second element is the number of features. In our case, we have one time step and one feature.

Next, we'll add a dense layer to the model. This is a standard fully-connected layer that will output a single value:

```javascript
model.add(tf.layers.dense({units: 1}));
```

Now we need to compile the model. We need to specify the loss function and the optimizer. We'll use the mean squared error loss function and the Adam optimizer:

```javascript
model.compile({loss: 'meanSquaredError', optimizer: 'adam'});
```

We're now ready to train the model. We'll use a `tf.tensor2d` to specify the training data. The first argument is the data, and the second argument is the shape of the data. In our case, we have two training examples, each with one time step and one feature:

```javascript
const xs = tf.tensor2d([[1], [2]]);
const ys = tf.tensor2d([[1], [2]]);
```

We'll train the model for 10 epochs, which is the number of times the model will see the training data:

```javascript
model.fit(xs, ys, {epochs: 10});
```

Once the model has been trained, we can use it to make predictions. We'll use a `tf.tensor2d` to specify the input data. In our case, we have one time step and one feature:

```javascript
const xs = tf.tensor2d([[3]]);
```

We can then call the `model.predict` method to make a prediction:

```javascript
model.predict(xs).print();
```

This will output the prediction, which is a single value.

## Building an LSTM network in Node.js

We'll now look at how to build an LSTM network in Node.js.

First, we need to install TensorFlow.js. We can do this using the Node.js package manager, npm:

```
npm install @tensorflow/tfjs
```

Next, we need to create a new file called `lstm.js` and import TensorFlow.js:

```javascript
const tf = require('@tensorflow/tfjs');
```

Now we're ready to start building our LSTM network.

We'll start by defining the model:

```javascript
const model = tf.sequential();
```

Next, we'll add an LSTM layer to the model. The first argument to the `tf.layers.lstmLayer` function is the number of units, which is the number of memory cells in the LSTM layer. We'll use 16 units:

```javascript
model.add(tf.layers.lstmLayer({units: 16, inputShape: [1, 1]}));
```

The `inputShape` argument is the shape of the input data. The first element is the number of time steps, and the second element is the number of features. In our case, we have one time step and one feature.

Next, we'll add a dense layer to the model. This is a standard fully-connected layer that will output a single value:

```javascript
model.add(tf.layers.denseLayer({units: 1}));
```

Now we need to compile the model. We need to specify the loss function and the optimizer. We'll use the mean squared error loss function and the Adam optimizer:

```javascript
model.compile({loss: 'meanSquaredError', optimizer: 'adam'});
```

We're now ready to train the model. We'll use a `tf.tensor2d` to specify the training data. The first argument is the data, and the second argument is the shape of the data. In our case, we have two training examples, each with one time step and one feature:

```javascript
const xs = tf.tensor2d([[1], [2]]);
const ys = tf.tensor2d([[1], [2]]);
```

We'll train the model for 10 epochs, which is the number of times the model will see the training data:

```javascript
model.fit(xs, ys, {epochs: 10});
```

Once the model has been trained, we can use it to make predictions. We'll use a `tf.tensor2d` to specify the input data. In our case, we have one time step and one feature:

```javascript
const xs = tf.tensor2d([[3]]);
```

We can then call the `model.predict` method to make a prediction:

```javascript
model.predict(xs).print();
```

This will output the prediction, which is a single value.

## Conclusion

In this post, we've seen how to build Long Short-Term Memory (LSTM) networks in TensorFlow.js and Node.js. LSTMs are a type of recurrent neural network that are well-suited for working with sequential data.

If you're interested in learning more about LSTMs, I recommend the following resources:

- [The Unreasonable Effectiveness of Recurrent Neural Networks](https://karpathy.github.io/2015/05/21/rnn-effectiveness/)
- [Understanding LSTM Networks](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [Long Short-Term Memory](https://en.wikipedia.org/wiki/Long_short-term_memory)