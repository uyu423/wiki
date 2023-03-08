---
title: 009: Recurrent Neural Networks (RNN) with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T08:44:00.133Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:43:58.506Z
---

- [009: Redes neuronales recurrentes (RNN) con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/009-recurrent-neural-networks-rnn-with-tensorflow-js-and-node-js)
{.links-list}
- [009：使用 TensorFlow.js 和 Node.js 的递归神经网络 (RNN)***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/009-recurrent-neural-networks-rnn-with-tensorflow-js-and-node-js)
{.links-list}
- [009: TensorFlow.js 및 Node.js를 사용한 순환 신경망(RNN)***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/009-recurrent-neural-networks-rnn-with-tensorflow-js-and-node-js)
{.links-list}


# Introduction

Recurrent Neural Networks (RNN) are a type of neural network that are well-suited for processing sequential data, such as text, audio, and video. In this post, we'll be using TensorFlow.js and Node.js to build an RNN that can generate new text, character-by-character.

# Setting up the project

Before we get started, we need to set up our project. We'll be using the Express web framework for Node.js, so first we need to install it.

```
$ npm install express --save
```

Next, we need to install TensorFlow.js. We'll be using the Node.js API, so we need to install the `@tensorflow/tfjs-node` package.

```
$ npm install @tensorflow/tfjs-node --save
```

Now that we have all the dependencies we need, we can create a file called `index.js` in our project's root directory and start coding.

# Building the RNN

The first thing we need to do is load the data we'll be using to train our RNN. We'll be using a corpus of Shakespearean text, which you can download [here](https://storage.googleapis.com/tfjs-examples/shakespeare.txt).

Once you have the text file downloaded, we can load it into our Node.js program using the `fs` module.

```javascript
const fs = require('fs');

const text = fs.readFileSync('shakespeare.txt', 'utf8');
```

Now that we have the text loaded, we need to preprocess it so that it's suitable for training our RNN. We'll start by converting all the characters to lowercase and removing all non-alphanumeric characters.

```javascript
const text = text.toLowerCase();
const text = text.replace(/[^a-zA-Z0-9]/g, '');
```

Next, we need to split the text into an array of individual characters.

```javascript
const chars = Array.from(text);
```

Now that we have our text preprocessed, we can start building our RNN. We'll be using a Long Short-Term Memory (LSTM) cell, which is a type of RNN cell that's well-suited for processing sequential data.

We can create an LSTM cell in TensorFlow.js with the following code:

```javascript
const lstmCell = tf.layers.lstmCell({
  units: 512,
  recurrentInputSize: 512,
  inputShape: [1, chars.length],
  kernelInitializer: 'glorotNormal',
  recurrentInitializer: 'orthogonal',
  biasInitializer: 'zeros',
  unitForgetBias: true,
  activation: 'tanh',
  recurrentActivation: 'sigmoid',
  useBias: true,
  kernelRegularizer: null,
  recurrentRegularizer: null,
  biasRegularizer: null,
  activityRegularizer: null,
  kernelConstraint: null,
  recurrentConstraint: null,
  biasConstraint: null,
  dropout: 0.0,
  recurrentDropout: 0.0
});
```

Next, we need to create the RNN itself. We can do this with the following code:

```javascript
const rnn = tf.layers.rnn({
  cell: lstmCell,
  inputShape: [1, chars.length],
  returnSequences: true,
  goBackwards: false,
  stateful: false,
  unroll: false
});
```

Now that we have our RNN created, we need to compile it. We'll be using the Adam optimizer and categorical cross entropy as our loss function.

```javascript
rnn.compile({
  optimizer: 'adam',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});
```

# Training the RNN

Now that our RNN is compiled, we can start training it. We'll first need to create some training data. We'll create an array of one-hot encoded characters, where each character is represented by a vector of zeros with a one in the index corresponding to the character.

```javascript
const chars = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'];

const oneHotChars = [];

for (let i = 0; i < chars.length; i++) {
  const char = chars[i];
  const oneHotChar = [];

  for (let j = 0; j < chars.length; j++) {
    if (j === i) {
      oneHotChar.push(1.0);
    } else {
      oneHotChar.push(0.0);
    }
  }

  oneHotChars.push(oneHotChar);
}
```

Now that we have our one-hot encoded characters, we need to create our training data. We'll create an array of training examples, where each training example is a pair of one-hot encoded characters. The first character in the pair will be the input character and the second character will be the output character.

```javascript
const trainingData = [];

for (let i = 0; i < text.length - 1; i++) {
  const inputChar = oneHotChars[chars.indexOf(text[i])];
  const outputChar = oneHotChars[chars.indexOf(text[i + 1])];

  trainingData.push([inputChar, outputChar]);
}
```

Now that we have our training data, we can train our RNN. We'll train it for 10 epochs and use a batch size of 32.

```javascript
rnn.fit(trainingData, {
  epochs: 10,
  batchSize: 32
});
```

# Generating text

Now that our RNN is trained, we can use it to generate new text. We'll start by creating a function that takes in a character and returns the next character.

```javascript
function nextChar(char) {
  const oneHotChar = oneHotChars[chars.indexOf(char)];
  const output = rnn.predict(tf.tensor2d([oneHotChar], [1, oneHotChar.length]));
  const index = output.argMax(1).dataSync()[0];
  const nextChar = chars[index];

  return nextChar;
}
```

Now we can use our `nextChar` function to generate new text. We'll start with the character 'a' and generate 1000 characters.

```javascript
let text = 'a';

for (let i = 0; i < 1000; i++) {
  text += nextChar(text[text.length - 1]);
}

console.log(text);
```

And that's it! You now have a working RNN that can generate new text, character-by-character.

# Additional Information

If you're interested in learning more about RNNs, I recommend the following resources:

- [Recurrent Neural Networks in TensorFlow](https://www.tensorflow.org/tutorials/sequences/recurrent)
- [Understanding LSTM Networks](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [Building a Recurrent Neural Network with TensorFlow](https://www.oreilly.com/learning/building-a-recurrent-neural-network-with-tensorflow)