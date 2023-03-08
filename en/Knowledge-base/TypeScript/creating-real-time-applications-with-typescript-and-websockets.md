---
title: Creating Real-Time Applications with TypeScript and WebSockets
description: 
published: true
date: 2023-01-31T10:57:35.821Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:57:32.375Z
---

- [TypeScript 및 WebSocket으로 실시간 애플리케이션 만들기***Korean** version of this document is available*](/ko/Knowledge-base/TypeScript/creating-real-time-applications-with-typescript-and-websockets)
{.links-list}
- [TypeScript と WebSocket を使用したリアルタイム アプリケーションの作成***Japanese** version of this document is available*](/ja/Knowledge-base/TypeScript/creating-real-time-applications-with-typescript-and-websockets)
{.links-list}
- [使用 TypeScript 和 WebSockets 创建实时应用程序***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/TypeScript/creating-real-time-applications-with-typescript-and-websockets)
{.links-list}



# Creating Real-Time Applications with TypeScript and WebSockets

WebSockets are a powerful tool for creating real-time applications. Combined with TypeScript, they can provide a great development experience with static type checking, code completion, and more. In this article, we'll explore how to use TypeScript and WebSockets to create a simple chat application.

## What are WebSockets?

WebSockets are a technology for creating bi-directional, real-time communication channels over an existing TCP connection. They are supported by all major browsers and can be used to create a variety of applications, from simple chat clients to complex multiplayer games.

## Getting Started

To get started, we'll need to set up a server that can handle WebSocket connections. For this article, we'll be using the popular Node.js framework Express.

First, we'll create a new directory for our project and install the dependencies:

```
mkdir chat-app
cd chat-app
npm init -y
npm install --save express
npm install --save ws
```

Next, we'll create a file for our server code:

```
touch server.js
```

And paste in the following code:

```javascript
const express = require('express');
const WebSocket = require('ws');

const app = express();

const PORT = process.env.PORT || 8080;

const server = app.listen(PORT, () => {
  console.log(`Server listening on port ${PORT}`);
});

const wss = new WebSocket.Server({ server });

wss.on('connection', (ws) => {
  console.log('Client connected');

  ws.on('message', (message) => {
    console.log(`Received message: ${message}`);
  });

  ws.send('Hello!');
});
```

Let's break down what's happening here. First, we require the Express and WebSocket modules. Next, we create an Express server and configure it to listen on port 8080. Then, we create a new WebSocket server, passing in the Express server as the 'server' option.

Next, we set up an event handler for when a client connects to the WebSocket server. When a client connects, we log a message to the console. Then, we set up an event handler for when a client sends a message. When a message is received, we again log it to the console. Finally, we send a message to the client.

To run the server, we can use the node command:

```
node server.js
```

## Creating a Client

Now that we have a server up and running, let's create a client. For this article, we'll be using the popular React framework.

First, we'll need to install the dependencies:

```
npm install --save react
npm install --save react-dom
npm install --save @types/react
npm install --save @types/react-dom
npm install --save ws
npm install --save @types/ws
```

Then, we'll create a file for our client code:

```
touch client.js
```

And paste in the following code:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import * as ws from 'ws';

const socket = new ws('ws://localhost:8080');

socket.onopen = () => {
  console.log('Connected to server');
};

socket.onmessage = (event) => {
  console.log(event.data);
};

socket.send('Hello from the client!');

ReactDOM.render(
  <div>Hello, world!</div>,
  document.getElementById('root')
);
```

First, we import the React and ReactDOM modules. Then, we import the WebSocket module. Next, we create a new WebSocket instance, passing in the URL of our server.

Then, we set up event handlers for when the socket opens and when a message is received. When the socket opens, we log a message to the console. When a message is received, we again log it to the console. Finally, we send a message to the server.

## Conclusion

In this article, we've seen how to use TypeScript and WebSockets to create a simple chat application. While this example is simple, it demonstrates the power of WebSockets for creating real-time applications.