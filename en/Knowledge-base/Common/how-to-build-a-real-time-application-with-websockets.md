---
title: How to Build a Real-Time Application with WebSockets
description: 
published: true
date: 2023-02-17T18:03:13.574Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:54:19.543Z
---

- [WebSocket으로 실시간 애플리케이션을 구축하는 방법***Korean** version of this document is available*](/ko/Knowledge-base/Common/how-to-build-a-real-time-application-with-websockets)
{.links-list}
- [WebSocket を使用してリアルタイム アプリケーションを構築する方法***Japanese** version of this document is available*](/ja/Knowledge-base/Common/how-to-build-a-real-time-application-with-websockets)
{.links-list}
- [如何使用 WebSockets 构建实时应用程序***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Common/how-to-build-a-real-time-application-with-websockets)
{.links-list}


# How to Build a Real-Time Application with WebSockets

In this article, we'll show you how to build a real-time application with WebSockets. We'll go over the basics of WebSockets and how to use them to create a simple chat application.

WebSockets are a protocol that allows for full-duplex communication between a client and a server. This means that both the client and the server can send and receive data at the same time. WebSockets are especially well-suited for applications that require real-time communication, such as chat applications, multiplayer games, and collaboration tools.

## Creating a WebSocket Server

To use WebSockets in your application, you'll need to create a WebSocket server. You can do this with any web server that supports the WebSocket protocol. For the purposes of this article, we'll be using the Node.js web server.

```javascript
var WebSocketServer = require('ws').Server;

var wss = new WebSocketServer({
  port: 8080
});

wss.on('connection', function(ws) {
  ws.on('message', function(message) {
    console.log('Received: %s', message);
  });

  ws.send('Hello, world!');
});
```

This code creates a WebSocket server that listens on port 8080 for incoming connections. When a connection is made, the server creates a WebSocket instance for that connection. The server then listens for messages from the client. When a message is received, it is logged to the console. The server also sends a message to the client when the connection is first made.

The WebSocket server can be run with the Node.js command-line interface.

```
node server.js
```

## Creating a WebSocket Client

Now that we have a WebSocket server up and running, we need to create a WebSocket client to connect to it. For the purposes of this article, we'll be using the browser-based JavaScript client.

```javascript
var ws = new WebSocket('ws://localhost:8080');

ws.onopen = function() {
  ws.send('Hello, world!');
};

ws.onmessage = function(event) {
  console.log(event.data);
};
```

This code creates a WebSocket instance and connects it to the WebSocket server. The code also defines two event handlers. The first event handler is for the ```open``` event. This event is fired when the connection is established. The second event handler is for the ```message``` event. This event is fired when the server sends a message to the client.

## Sending and Receiving Messages

Now that we have a WebSocket server and client set up, we can start sending and receiving messages. The ```send``` method can be used to send messages from the client to the server. The ```onmessage``` event handler can be used to receive messages from the server.

```javascript
ws.send('Hello, world!');

ws.onmessage = function(event) {
  console.log(event.data);
};
```

In this code, the ```send``` method is used to send a message from the client to the server. The ```onmessage``` event handler is used to receive the message from the server. The message is logged to the console.