---
title: 084: Using TensorFlow.js with Other JavaScript Libraries in Node.js
description: 
published: true
date: 2023-02-03T02:37:12.925Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:37:08.087Z
---

- [084: uso de TensorFlow.js con otras bibliotecas de JavaScript en Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/084-using-tensorflow-js-with-other-javascript-libraries-in-node-js)
{.links-list}
- [084：在 Node.js 中使用 TensorFlow.js 和其他 JavaScript 库***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/084-using-tensorflow-js-with-other-javascript-libraries-in-node-js)
{.links-list}
- [084: Node.js에서 다른 JavaScript 라이브러리와 함께 TensorFlow.js 사용***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/084-using-tensorflow-js-with-other-javascript-libraries-in-node-js)
{.links-list}


# Using TensorFlow.js with Other JavaScript Libraries in Node.js

TensorFlow.js is a powerful tool for machine learning in JavaScript, and it works great with other JavaScript libraries. In this post, we'll show you how to use TensorFlow.js with Node.js and Express.

## Prerequisites

To follow along with this post, you'll need a few things:

- Node.js and npm installed
- A text editor - we recommend Visual Studio Code
- Basic knowledge of JavaScript

## Getting Started

First, let's create a new directory for our project:

```
mkdir tensorflowjs-node
cd tensorflowjs-node
```

Next, we'll initialize our project with npm:

```
npm init -y
```

Now that our project is set up, we can install the dependencies we'll need. We'll be using the following libraries:

- [TensorFlow.js](https://www.tensorflow.org/js)
- [Express](https://expressjs.com/)
- [body-parser](https://www.npmjs.com/package/body-parser)

We can install these dependencies with the following command:

```
npm install --save @tensorflow/tfjs express body-parser
```

## Hello, TensorFlow.js!

Now that we have our dependencies installed, we can start writing some code. Let's begin by creating a file called `index.js`. In this file, we'll write a simple script to print "Hello, TensorFlow.js!" to the console:

```javascript
// index.js

const tf = require('@tensorflow/tfjs');

console.log('Hello, TensorFlow.js!');
```

If we run this script with Node.js, we should see the following output:

```
$ node index.js
Hello, TensorFlow.js!
```

## Using TensorFlow.js with Express

Now that we've seen how to use TensorFlow.js in a Node.js script, let's take a look at how we can use it with Express. For this example, we'll create a simple server that responds to `GET` requests with a list of numbers.

First, let's require the dependencies we'll need:

```javascript
// index.js

const tf = require('@tensorflow/tfjs');
const express = require('express');
const bodyParser = require('body-parser');
```

Next, we'll create an ` Express` instance and configure `body-parser` to parse JSON bodies:

```javascript
// index.js

const app = express();
app.use(bodyParser.json());
```

Now, let's define a route that will respond to `GET` requests with a list of numbers:

```javascript
// index.js

app.get('/numbers', (req, res) => {
  const numbers = [1, 2, 3, 4, 5];
  res.json(numbers);
});
```

Finally, we'll start the server on port `3000`:

```javascript
// index.js

app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

If we run this script with Node.js, we should see the following output:

```
$ node index.js
Server is listening on port 3000
```

We can now send `GET` requests to `http://localhost:3000/numbers` and we'll receive a JSON response with a list of numbers.

## Using TensorFlow.js with Express and body-parser

In the previous section, we saw how to use TensorFlow.js with Express. In this section, we'll extend our example to show how we can use `body-parser` to parse JSON bodies.

First, let's require the dependencies we'll need:

```javascript
// index.js

const tf = require('@tensorflow/tfjs');
const express = require('express');
const bodyParser = require('body-parser');
```

Next, we'll create an ` Express` instance and configure `body-parser` to parse JSON bodies:

```javascript
// index.js

const app = express();
app.use(bodyParser.json());
```

Now, let's define a route that will respond to `POST` requests with the body of the request:

```javascript
// index.js

app.post('/body', (req, res) => {
  res.json(req.body);
});
```

Finally, we'll start the server on port `3000`:

```javascript
// index.js

app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

If we run this script with Node.js, we should see the following output:

```
$ node index.js
Server is listening on port 3000
```

We can now send `POST` requests to `http://localhost:3000/body` with a JSON body and we'll receive a JSON response with the body of the request.

## Using TensorFlow.js with Express and body-parser

In the previous section, we saw how to use TensorFlow.js with Express and body-parser. In this section, we'll extend our example to show how we can use TensorFlow.js to perform inference on the body of the request.

First, let's require the dependencies we'll need:

```javascript
// index.js

const tf = require('@tensorflow/tfjs');
const express = require('express');
const bodyParser = require('body-parser');
```

Next, we'll create an ` Express` instance and configure `body-parser` to parse JSON bodies:

```javascript
// index.js

const app = express();
app.use(bodyParser.json());
```

Now, let's define a route that will respond to `POST` requests with the body of the request:

```javascript
// index.js

app.post('/inference', (req, res) => {
  const input = tf.tensor(req.body);
  const output = tf.add(input, 1);
  res.json(output.dataSync());
});
```

Finally, we'll start the server on port `3000`:

```javascript
// index.js

app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

If we run this script with Node.js, we should see the following output:

```
$ node index.js
Server is listening on port 3000
```

We can now send `POST` requests to `http://localhost:3000/inference` with a JSON body and we'll receive a JSON response with the result of the inference.

## Wrapping Up

In this post, we've seen how to use TensorFlow.js with Node.js and Express. We've also seen how to use TensorFlow.js with body-parser to parse JSON bodies.

## Resources

- [TensorFlow.js](https://www.tensorflow.org/js)
- [Express](https://expressjs.com/)
- [body-parser](https://www.npmjs.com/package/body-parser)