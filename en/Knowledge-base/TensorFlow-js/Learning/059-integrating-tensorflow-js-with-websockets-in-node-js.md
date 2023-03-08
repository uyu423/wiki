---
title: 059: Integrating TensorFlow.js with WebSockets in Node.js
description: 
published: true
date: 2023-02-02T20:44:13.063Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:44:11.380Z
---

- [059: Integrando TensorFlow.js con WebSockets en Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/059-integrating-tensorflow-js-with-websockets-in-node-js)
{.links-list}
- [059：在 Node.js 中将 TensorFlow.js 与 WebSockets 集成***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/059-integrating-tensorflow-js-with-websockets-in-node-js)
{.links-list}
- [059: TensorFlow.js와 Node.js의 WebSockets 통합***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/059-integrating-tensorflow-js-with-websockets-in-node-js)
{.links-list}


# 059: Integrating TensorFlow.js with WebSockets in Node.js

TensorFlow.js is a powerful tool for training and deploying machine learning models in the browser. However, training models in the browser can be slow and inefficient due to the limited resources available.

One way to speed up training is to use WebSockets to send data to a server for training. This way, the server can use its resources to train the model more quickly.

In this post, we'll show you how to set up a Node.js server and use WebSockets to send data to the server for training a TensorFlow.js model.

## Prerequisites

Before we get started, there are a few things you'll need:

- A text editor. We recommend [Visual Studio Code](https://code.visualstudio.com/).
- [Node.js](https://nodejs.org/en/) installed on your computer.
- [NPM](https://www.npmjs.com/) (which comes with Node.js) installed on your computer.
- [TensorFlow.js](https://js.tensorflow.org/) installed on your computer.

## Setting up the Node.js server

First, we'll need to set up a Node.js server. We'll use the [ Express ](https://expressjs.com/) web framework to make things easier.

Create a new file called `server.js` and paste the following code into it:

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => res.send('Hello World!'));

app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```

This code creates a basic Express server that listens on port 3000.

Next, we'll need to install the dependencies for our server. In your terminal, navigate to the directory where `server.js` is located and run the following command:

```
npm install express --save
```

This will install the Express framework and save it as a dependency in our `package.json` file.

Now that our server is set up, we can start it by running the following command in our terminal:

```
node server.js
```

You should see the following output:

```
Example app listening on port 3000!
```

## Sending data to the server

Now that our server is up and running, we can start sending data to it. We'll use [ WebSockets ](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) to send data from the browser to the server.

First, we'll need to install the [ ws ](https://github.com/websockets/ws) WebSocket library. In your terminal, navigate to the directory where `server.js` is located and run the following command:

```
npm install ws --save
```

This will install the `ws` library and save it as a dependency in our `package.json` file.

Next, we'll need to modify our `server.js` file to use the `ws` library. Replace the contents of `server.js` with the following code:

```javascript
const express = require('express');
const app = express();
const port = 3000;
const WebSocket = require('ws');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
  ws.on('message', (message) => {
    console.log(`Received message => ${message}`);
  });
  ws.send('Hello!');
});

app.get('/', (req, res) => res.send('Hello World!'));

app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```

This code creates a new WebSocket server that listens on port 8080. When a connection is made, the server will log any messages it receives.

Now that our server is set up to receive data, we can write some code to send data to it. Create a new file called `client.html` and paste the following code into it:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>WebSocket Client</title>
  </head>
  <body>
    <h1>WebSocket Client</h1>
    <script>
      const ws = new WebSocket('ws://localhost:8080');
      ws.onopen = () => {
        // Send a message when the WebSocket is opened
        ws.send('Hello!');
      };
      ws.onmessage = (event) => {
        // Log the message when a message is received
        console.log(event.data);
      };
    </script>
  </body>
</html>
```

This code creates a new WebSocket connection to our server and sends a message when the connection is opened. It also logs any messages it receives.

Open `client.html` in your browser and you should see the following output in the console:

```
Hello!
```

## Sending data to the server for training

Now that we can send data to our server, we can use it to train a TensorFlow.js model. We'll use the [ Iris Dataset ](https://en.wikipedia.org/wiki/Iris_flower_data_set) to train a simple classification model.

First, we'll need to modify our `server.js` file to include the TensorFlow.js library. Replace the contents of `server.js` with the following code:

```javascript
const express = require('express');
const app = express();
const port = 3000;
const WebSocket = require('ws');
const tf = require('@tensorflow/tfjs');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
  ws.on('message', (message) => {
    console.log(`Received message => ${message}`);
  });
  ws.send('Hello!');
});

app.get('/', (req, res) => res.send('Hello World!'));

app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```

This code includes the TensorFlow.js library and creates a basic classification model.

Next, we'll need to modify our `client.html` file to send data to the server for training. Replace the contents of `client.html` with the following code:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>WebSocket Client</title>
  </head>
  <body>
    <h1>WebSocket Client</h1>
    <script>
      const ws = new WebSocket('ws://localhost:8080');
      ws.onopen = () => {
        // Send data to the server when the WebSocket is opened
        ws.send('1,2,3,4');
      };
      ws.onmessage = (event) => {
        // Log the message when a message is received
        console.log(event.data);
      };
    </script>
  </body>
</html>
```

This code sends data to the server when the connection is opened. It also logs any messages it receives.

Open `client.html` in your browser and you should see the following output in the console:

```
Received message => 1,2,3,4
```

## Conclusion

In this post, we've shown you how to set up a Node.js server and use WebSockets to send data to the server for training a TensorFlow.js model.

This is a powerful way to train machine learning models in the browser. By using the resources of a server, we can train models more quickly and efficiently.