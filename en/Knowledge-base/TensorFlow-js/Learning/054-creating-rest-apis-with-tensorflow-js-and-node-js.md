---
title: 054: Creating REST APIs with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T19:36:30.146Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:36:25.590Z
---

- [054: Creación de API REST con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/054-creating-rest-apis-with-tensorflow-js-and-node-js)
{.links-list}
- [054：使用 TensorFlow.js 和 Node.js 创建 REST API***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/054-creating-rest-apis-with-tensorflow-js-and-node-js)
{.links-list}
- [054: TensorFlow.js 및 Node.js로 REST API 만들기***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/054-creating-rest-apis-with-tensorflow-js-and-node-js)
{.links-list}


# Creating REST APIs with TensorFlow.js and Node.js

## Introduction

In this post, we'll show you how to create REST APIs with TensorFlow.js and Node.js. We'll go over all the steps necessary to get your project up and running, including installing the required dependencies, setting up your project, and writing your code.

By the end of this post, you'll be able to create your own REST APIs with TensorFlow.js and Node.js.

## Prerequisites

Before we get started, there are a few things you'll need to have in order to follow along:

- A text editor. We recommend [Visual Studio Code](https://code.visualstudio.com/).
- [Node.js](https://nodejs.org/en/) installed on your machine.
- [npm](https://www.npmjs.com/) installed on your machine.
- [TensorFlow.js](https://js.tensorflow.org/) installed on your machine.

## Setting up your project

Once you have the prerequisites set up, you're ready to start setting up your project.

First, create a new directory for your project. We'll call ours `tfjs-rest-api`.

Next, initialize your project by running `npm init` in your project directory. This will create a `package.json` file for your project.

Now that you have a `package.json` file, you can install the dependencies for your project. Run the following command to install [Express](https://expressjs.com/), [ Body-Parser ](https://www.npmjs.com/package/body-parser), and [ TensorFlow.js ](https://www.npmjs.com/package/@tensorflow/tfjs):

```
npm install express body-parser @tensorflow/tfjs --save
```

This will install the dependencies and add them to your `package.json` file.

## Writing your code

Now that you have your project set up, you're ready to start writing your code.

Open your text editor and create a new file in your project directory. We'll call ours `index.js`.

In this file, we'll start by requiring the dependencies we installed earlier:

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const tf = require('@tensorflow/tfjs');
```

Next, we'll set up our Express server:

```javascript
const app = express();
const port = 3000;

app.use(bodyParser.json());

app.listen(port, () => {
  console.log(`Server listening on port ${port}`);
});
```

Now that our server is set up, we can start writing our API endpoints.

Our first endpoint will be a `GET` request to `/` that will return a simple message:

```javascript
app.get('/', (req, res) => {
  res.send('Hello, world!');
});
```

Our second endpoint will be a `POST` request to `/predict` that will take in an array of numbers and return a prediction based on those numbers:

```javascript
app.post('/predict', (req, res) => {
  const input = tf.tensor2d([req.body.numbers], [1, req.body.numbers.length]);
  const output = model.predict(input);
  res.send(output.dataSync());
});
```

In this endpoint, we're using a pre-trained [TensorFlow.js](https://js.tensorflow.org/) model to make our predictions. You can find this model [here](https://storage.googleapis.com/tfjs-models/tfjs/mnist_model/model.json).

## Testing your API

Now that you have your API endpoints set up, you're ready to test them.

To test your `GET` endpoint, you can use a tool like [Postman](https://www.getpostman.com/).

To test your `POST` endpoint, you can use the following command:

```
curl -X POST -H "Content-Type: application/json" -d '{"numbers": [1, 2, 3, 4, 5]}' http://localhost:3000/predict
```

This should return a prediction of `[6]`.

## Conclusion

In this post, we showed you how to create REST APIs with TensorFlow.js and Node.js. We covered all the steps necessary to get your project up and running, including installing the required dependencies, setting up your project, and writing your code.

By the end of this post, you should be able to create your own REST APIs with TensorFlow.js and Node.js.