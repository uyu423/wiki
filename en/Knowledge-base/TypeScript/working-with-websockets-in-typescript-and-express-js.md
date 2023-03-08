---
title: Working with WebSockets in TypeScript and Express.js
description: 
published: true
date: 2023-02-17T18:12:01.946Z
tags: 
editor: markdown
dateCreated: 2023-01-30T18:57:49.579Z
---

- [TypeScript 및 Express.js에서 WebSocket 작업***Korean** version of this document is available*](/ko/Knowledge-base/TypeScript/working-with-websockets-in-typescript-and-express-js)
{.links-list}
- [TypeScript と Express.js での WebSocket の操作***Japanese** version of this document is available*](/ja/Knowledge-base/TypeScript/working-with-websockets-in-typescript-and-express-js)
{.links-list}
- [在 TypeScript 和 Express.js 中使用 WebSockets***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/TypeScript/working-with-websockets-in-typescript-and-express-js)
{.links-list}





WebSockets are a very popular way to communicate between a client and a server. They provide a bi-directional, full-duplex communication channel over a single TCP connection, and are very well supported by all major browsers.

In this article, we'll show you how to use WebSockets in TypeScript and Express.js. We'll also provide some practical examples of how to use them in your web applications.

## What are WebSockets?

WebSockets are a relatively new technology, which enables bi-directional, real-time communication between a web browser and a server. They are an alternative to the traditional HTTP request-response model, and provide a much more efficient communication channel.

 WebSockets are based on the TCP protocol, and use a full-duplex communication channel. This means that both the client and the server can send and receive data at the same time.

WebSockets are supported by all major browsers, and there are a number of well-supported libraries and frameworks that make it easy to use them in your web applications.

## Why use WebSockets?

WebSockets provide a number of benefits over the traditional HTTP request-response model.

They are much more efficient, as they only require a single TCP connection, which stays open for the duration of the communication. This means that there is no need to set up a new connection for each request, as is the case with HTTP.

They are also much lower latency, as there is no need to wait for a request to complete before the next one can be sent. This is especially important for applications that require real-time communication, such as chat applications, online games, and so on.

## How do WebSockets work?

WebSockets use a protocol called ws://, which is an extension of the HTTP protocol. When a client wants to establish a WebSocket connection to a server, it sends a request using this protocol.

The server then responds with an HTTP 101 switch to WebSockets protocol status code, and the connection is then upgraded to a WebSocket connection.

Once the connection is established, the client and server can send and receive data at any time.

## Using WebSockets in TypeScript

There are a number of libraries that can be used to provide WebSocket support in TypeScript, such as ws and socket.io. In this article, we'll be using the socket.io library.

Socket.io is a popular and well-supported library that makes it easy to use WebSockets in your TypeScript applications. It abstracts away the details of the WebSocket protocol, and provides a simple API that can be used to send and receive data.

Socket.io also provides a number of other features, such as pub/sub messaging, rooms, and so on.

## Installing Socket.io

Socket.io can be installed using the npm package manager:

```
npm install socket.io
```

## Creating a Socket.io server

Socket.io applications have two parts: a client-side library that runs in the browser, and a server-side library that runs on the Node.js platform.

In this section, we'll create a simple Socket.io server that will broadcast a "hello world" message to all connected clients.

First, we need to import the socket.io library:

```typescript
import * as io from "socket.io";
```

Next, we'll create an HTTP server using the Express.js framework:

```typescript
const app = express();
const server = http.createServer(app);
```

We can then bind the Socket.io library to the HTTP server:

```typescript
const io = socketIO(server);
```

Now that we have a Socket.io server up and running, we need to write some code to handle incoming connections. We can do this using the ```connection``` event:

```typescript
io.on("connection", (socket) => {
  //
});
```

The ```connection``` event is emitted when a client connects to the server. The ```socket``` object that is passed to the callback function represents the client connection.

We can now write some code to send a message to the client:

```typescript
io.on("connection", (socket) => {
  socket.emit("hello", "Hello, world!");
});
```

The ```emit``` method is used to send a message to the client. The first argument is the name of the event, and the second argument is the data to be sent.

## Creating a Socket.io client

Now that we have a Socket.io server up and running, let's create a client that will connect to it and print out the "hello world" message.

First, we need to include the Socket.io client library in our HTML page:

```html
<script src="/socket.io/socket.io.js"></script>
```

Next, we'll create a new ```Socket``` instance, and connect it to our server:

```javascript
const socket = io("http://localhost:8080");
```

We can then listen for the ```hello``` event that we defined on the server:

```javascript
socket.on("hello", (data) => {
  console.log(data); // "Hello, world!"
});
```

## Sending and receiving data

In the previous section, we saw how to send data from the server to the client. In this section, we'll see how to do the reverse: send data from the client to the server.

We can do this using the ```send``` method:

```javascript
socket.send("hello", "Hello, world!");
```

On the server, we can listen for the ```message``` event:

```typescript
socket.on("message", (data) => {
  console.log(data); // "Hello, world!"
});
```

##Conclusion

In this article, we've seen how to use WebSockets in TypeScript and Express.js. We've also seen how to create a Socket.io server and client, and how to send and receive data between them.