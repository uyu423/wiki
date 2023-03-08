---
title: 063: Real-Time Sentiment Analysis with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T21:43:50.094Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:43:45.476Z
---

- [063: Análisis de sentimiento en tiempo real con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/063-real-time-sentiment-analysis-with-tensorflow-js-and-node-js)
{.links-list}
- [063：使用 TensorFlow.js 和 Node.js 进行实时情感分析***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/063-real-time-sentiment-analysis-with-tensorflow-js-and-node-js)
{.links-list}
- [063: TensorFlow.js 및 Node.js를 사용한 실시간 감정 분석***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/063-real-time-sentiment-analysis-with-tensorflow-js-and-node-js)
{.links-list}


# Real-Time Sentiment Analysis with TensorFlow.js and Node.js

In this post, we'll be looking at how to build a real-time sentiment analysis application using TensorFlow.js and Node.js.

## What is Sentiment Analysis?

Sentiment analysis is the process of extracting opinion-based information from text. This can be useful for a variety of applications, such as understanding customer feedback or gauging the public's reaction to a news event.

## Building the Application

We'll be using the following tools to build our application:

- [TensorFlow.js](https://js.tensorflow.org/)
- [Node.js](https://nodejs.org/en/)
- [Socket.io](https://socket.io/)

### Setting up the Environment

First, we need to set up our development environment. We'll be using [Node.js](https://nodejs.org/en/) for this project, so make sure you have it installed.

Once Node.js is installed, we can create a new project directory and initialize it with [npm](https://www.npmjs.com/):

```
mkdir sentiment-analysis
cd sentiment-analysis
npm init -y
```

This will create a new directory called `sentiment-analysis` and initialize it with a `package.json` file.

Next, we need to install the dependencies for our project. We'll be using [TensorFlow.js](https://js.tensorflow.org/) and [Socket.io](https://socket.io/):

```
npm install @tensorflow/tfjs socket.io
```

This will install the `@tensorflow/tfjs` and `socket.io` packages in our project.

### Creating the Model

Now that we have our environment set up, we can start building the sentiment analysis model. We'll be using a [pre-trained model](https://tfhub.dev/google/tfjs-models/tfjs-sentiment/2) from TensorFlow Hub.

To use this model, we first need to load it into TensorFlow.js:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
const model = await tf.loadModel('https://tfhub.dev/google/tfjs-models/tfjs-sentiment/2/default/1');
```

Next, we need to create a function that takes a string of text and returns a score between 0 and 1, where 0 is negative and 1 is positive. We can do this by feeding the text into the model and taking the argmax of the output:

```javascript
function getSentiment(text) {
  // Convert the text to a tensor.
  const input = tf.tensor1d([text]);

  // Get the model's predictions.
  const predictions = model.predict(input);

  // Get the highest scoring prediction.
  const argMax = predictions.argMax(-1);

  // We only need the highest scoring prediction's index.
  const index = argMax.dataSync()[0];

  // Get the predicted label.
  const label = (index === 0) ? 'negative' : 'positive';

  // Get the predicted probability.
  const probability = predictions.dataSync()[index];

  return { label, probability };
}
```

Now that we have our model set up, we can move on to creating the server.

### Creating the Server

We'll be using [Node.js](https://nodejs.org/) and [Socket.io](https://socket.io/) to create the server for our application.

First, we need to require the dependencies:

```javascript
const tf = require('@tensorflow/tfjs');
const io = require('socket.io')();
```

Next, we need to create a function that handles incoming text from a socket:

```javascript
function handleText(socket, text) {
  // Get the sentiment of the text.
  const { label, probability } = getSentiment(text);

  // Emit the results to the socket.
  socket.emit('results', { label, probability });
}
```

Finally, we need to start the server and listen for incoming connections:

```javascript
// Start the server.
io.listen(3000);

// Listen for incoming connections.
io.on('connection', (socket) => {
  // Listen for text from the socket.
  socket.on('text', (text) => handleText(socket, text));
});
```

Now that we have our server set up, we can move on to creating the client.

### Creating the Client

We'll be using [Socket.io](https://socket.io/) to create the client for our application.

First, we need to load the Socket.io client library:

```html
<script src="/socket.io/socket.io.js"></script>
```

Next, we need to create a socket and connect it to the server:

```javascript
// Connect to the server.
const socket = io.connect('http://localhost:3000');
```

Now that we have our socket set up, we can start sending text to the server. We'll do this by listening for user input and emitting it to the socket:

```javascript
// Listen for user input.
document.querySelector('#text-input').addEventListener('input', (event) => {
  // Get the input text.
  const text = event.target.value;

  // Emit the text to the socket.
  socket.emit('text', text);
});
```

Finally, we need to listen for results from the server and display them to the user:

```javascript
// Listen for results from the server.
socket.on('results', (results) => {
  // Get the results element.
  const element = document.querySelector('#results');

  // Clear the element.
  element.innerHTML = '';

  // Create a new paragraph for each result.
  results.forEach((result) => {
    const { label, probability } = result;
    const paragraph = document.createElement('p');
    paragraph.innerHTML = `${label}: ${probability}`;
    element.appendChild(paragraph);
  });
});
```

Now that we have our client set up, we can test the application.

## Testing the Application

To test the application, open `index.html` in a browser. Then, enter some text into the text input and press enter. You should see the results appear in the results element.

## Conclusion

In this post, we've seen how to build a real-time sentiment analysis application using TensorFlow.js and Node.js. We've also seen how to use a pre-trained model from TensorFlow Hub.

If you're interested in learning more about sentiment analysis, here are some resources for further reading:

- [Sentiment Analysis with TensorFlow.js](https://medium.com/tensorflow/sentiment-analysis-with-tensorflow-js-bccd4d9d4a30)
- [Real-Time Sentiment Analysis with TensorFlow.js](https://www.tensorflow.org/js/tutorials/sentiment/index)