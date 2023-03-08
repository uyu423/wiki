---
title: Building Real-Time Chat Applications with TypeScript and WebSockets
description: 
published: true
date: 2023-02-24T20:32:49.595Z
tags: 
editor: markdown
dateCreated: 2023-02-24T20:32:42.621Z
---

- [TypeScript 및 WebSocket으로 실시간 채팅 애플리케이션 구축***Korean** document is available*](/ko/Knowledge-base/TypeScript/building-real-time-chat-applications-with-typescript-and-websockets)
{.links-list}


# Building Real-Time Chat Applications with TypeScript and WebSockets

WebSockets are a relatively new technology that enables two-way real-time communication between a client and server. They are commonly used in chat applications to provide a real-time, immersive experience to users.

While WebSockets are great for chat applications, they can also be used for other types of applications that require real-time communication between a client and server, such as gaming, collaboration, and notification applications.

In this article, we will show you how to build a real-time chat application using TypeScript and WebSockets. We will be using the Node.js WebSocket library ws and the Express web framework.

## Getting Started

Before we get started, we need to install the dependencies that we will be using. We will be using the Node.js WebSocket library ws and the Express web framework.

To install these dependencies, you can use the following command:

```
npm install --save ws express
```

## Creating the Server

Now that we have our dependencies installed, we can create our server. We will start by creating a file called server.ts and adding the following code:

```typescript
import * as WebSocket from 'ws';
import * as express from 'express';

const app = express();

const server = app.listen(8080, () => {
    console.log('Server is listening on port 8080');
});

const wss = new WebSocket.Server({ server });
```

Let's break down this code to see what it is doing. We start by importing the WebSocket and express modules. We then create an instance of the express application and create a server that listens on port 8080.

Finally, we create an instance of the WebSocket server. This will be used to broadcast messages to all connected clients.

## Connecting the Client

Now that we have our server set up, we need to create a client that can connect to it. We will start by creating a file called client.ts and adding the following code:

```typescript
import * as WebSocket from 'ws';

const ws = new WebSocket('ws://localhost:8080');

ws.on('open', () => {
    console.log('Connected to server');
});

ws.on('message', (message: string) => {
    console.log(`Received message from server: ${message}`);
});
```

This code should be familiar to you if you have used WebSockets before. We start by creating a WebSocket instance and connect to our server. We then set up event handlers for the open and message events.

The open event is fired when a connection is established and the message event is fired when a message is received from the server.

## Sending Messages

Now that we have our server and client set up, we can start sending messages between them.

We will start by adding the following code to our server.ts file:

```typescript
wss.on('connection', (ws: WebSocket) => {
    ws.on('message', (message: string) => {
        console.log(`Received message from client: ${message}`);

        // Broadcast the message to all connected clients
        wss.clients.forEach((client: WebSocket) => {
            if (client != ws) {
                client.send(message);
            }
        });
    });
});
```

This code sets up an event handler for the connection event. This event is fired when a client connects to the server.

We then set up another event handler for the message event. This event is fired when a message is received from the client.

Finally, we loop through all of the clients that are connected to the server and send the message to all of them except for the client that sent the message. This will ensure that the message is broadcast to all connected clients.

Now, if we add the following code to our client.ts file:

```typescript
ws.send('Hello, world!');
```

We will see the following output in the console:

```
Connected to server
Received message from server: Hello, world!
```

## Conclusion

In this article, we have shown you how to build a real-time chat application using TypeScript and WebSockets. We have also shown you how to broadcast messages to all connected clients.

If you want to learn more about TypeScript and WebSockets, here are some resources that you can check out:

- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/basic-types.html)
- [WebSockets Tutorial](https://www.tutorialspoint.com/websockets/index.htm)
- [Building a WebSocket Server with Node.js](https://www.sitepoint.com/websockets-node-js/)