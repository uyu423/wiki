---
title: Working with Node.js and WebSockets for Real-Time Communication
description: 
published: true
date: 2023-02-17T01:55:33.412Z
tags: 
editor: markdown
dateCreated: 2023-02-17T01:55:30.796Z
---

- [Trabajar con Node.js y WebSockets para comunicación en tiempo real***Spanish** document is available*](/es/Knowledge-base/Nodejs/working-with-node-js-and-websockets-for-real-time-communication)
{.links-list}
- [使用 Node.js 和 WebSockets 进行实时通信***Chinese Simplified** document is available*](/zh/Knowledge-base/Nodejs/working-with-node-js-and-websockets-for-real-time-communication)
{.links-list}
- [실시간 통신을 위한 Node.js 및 WebSockets 작업***Korean** document is available*](/ko/Knowledge-base/Nodejs/working-with-node-js-and-websockets-for-real-time-communication)
{.links-list}


      IT Development Learning Blog

# Working with Node.js and WebSockets for Real-Time Communication

Node.js is a Javascript runtime environment that allows you to run Javascript code outside of the browser. It is versatile and can be used for developing server-side applications, command line tools, and even desktop applications.

WebSockets is a web technology that allows for full-duplex, bi-directional communication between a client and a server. It is designed for real-time communication and is often used in applications such as chat applications, collaborative editing applications, and gaming applications.

In this article, we will explore how to use Node.js and WebSockets for real-time communication. We will discuss how to set up a Node.js server that can handle WebSocket requests, and we will also build a simple chat application that uses WebSockets for real-time communication.

## Setting up a Node.js server

We will use the [ws](https://www.npmjs.com/package/ws) npm package for working with WebSockets in Node.js.

First, we need to install the `ws` package:

```
npm install ws
```

Next, we need to create a file called `server.js` and add the following code:

```javascript
const WebSocket = require('ws');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
  ws.on('message', (message) => {
    console.log(`Received message => ${message}`);
  });

  ws.send('Hello!');
});
```

In the code above, we are using the `ws` package to create a WebSocket server on port 8080. We are also handling the `connection` event, which is fired when a client connects to the server. When a connection is established, we are setting up an event handler for the `message` event, which is fired when a message is received from the client. Finally, we are sending a message to the client when the connection is established.

To run the server, we can use the following command:

```
node server.js
```

## Creating a chat application

Now that we have a Node.js server that can handle WebSocket requests, let's build a simple chat application that uses WebSockets for real-time communication.

First, we need to create a file called `client.html` and add the following code:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>WebSocket Chat</title>
</head>
<body>
  <h1>WebSocket Chat</h1>
  <form id="form">
    <label for="message">Message:</label>
    <input type="text" id="message" />
    <input type="submit" value="Send" />
  </form>
  <ul id="messages"></ul>
  <script>
    const form = document.getElementById('form');
    const messages = document.getElementById('messages');
    const message = document.getElementById('message');

    const ws = new WebSocket('ws://localhost:8080');

    ws.onopen = () => {
      console.log('Connected');
    };

    ws.onmessage = (event) => {
      const li = document.createElement('li');
      li.innerText = event.data;
      messages.appendChild(li);
    };

    ws.onerror = (error) => {
      console.log(error);
    };

    ws.onclose = () => {
      console.log('Disconnected');
    };

    form.addEventListener('submit', (event) => {
      event.preventDefault();

      ws.send(message.value);
      message.value = '';
    });
  </script>
</body>
</html>
```

In the code above, we are using HTML and Javascript to create a simple chat application. We are using the `WebSocket` API to establish a connection with the server, and we are using the `message` event to receive messages from the server and display them in the browser. We are also using the `send` method to send messages to the server.

## Conclusion

In this article, we have explored how to use Node.js and WebSockets for real-time communication. We have set up a Node.js server that can handle WebSocket requests, and we have also built a simple chat application that uses WebSockets for real-time communication.