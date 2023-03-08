---
title: Real-time Communication with Socket.io
description: 
published: true
date: 2023-02-17T06:17:39.224Z
tags: 
editor: markdown
dateCreated: 2023-02-17T06:17:28.353Z
---

- [Comunicación en tiempo real con Socket.io***Spanish** document is available*](/es/Knowledge-base/Backend/real-time-communication-with-socket-io)
{.links-list}
- [与 Socket.io 的实时通信***Chinese Simplified** document is available*](/zh/Knowledge-base/Backend/real-time-communication-with-socket-io)
{.links-list}
- [Socket.io와 실시간 통신***Korean** document is available*](/ko/Knowledge-base/Backend/real-time-communication-with-socket-io)
{.links-list}



# Real-time Communication with Socket.io

In this article, we'll be discussing real-time communication with Socket.io. Socket.io is a JavaScript library that provides real-time, bi-directional communication between web clients and servers. It has a number of features that make it ideal for use in real-time applications, such as real-time messaging, chat, games, and more.

Socket.io is based on the WebSocket protocol and uses the Node.js platform. It is easy to use and easy to set up, making it a great choice for real-time applications.

## Setting up Socket.io

To use Socket.io, you need to install the socket.io module. You can do this using the Node Package Manager (NPM):

```
npm install socket.io
```

Once the module is installed, you can require it in your Node.js application:

```javascript
var io = require('socket.io')();
```

The socket.io module returns a function that you can call with the http server instance. This will set up the socket.io communication for you.

## Using Socket.io

Socket.io provides two ways to communicate:

* Events: You can emit events from the client to the server, or from the server to the client. Events can be named anything you want, and they can carry data.
* Messages: You can send messages between the client and the server. Messages are like events, but they're sent with a specific format that allows for different types of data to be sent (e.g. binary data).

### Events

To emit an event from the client to the server, you can use the emit method:

```javascript
socket.emit('eventName', data);
```

To emit an event from the server to the client, you can use the emit method on the socket object:

```javascript
socket.emit('eventName', data);
```

You can also broadcast an event to all connected clients, except for the client that emitted the event. To do this, you can use the broadcast method:

```javascript
socket.broadcast.emit('eventName', data);
```

To listen for an event, you can use the on method:

```javascript
socket.on('eventName', function(data) {
  // do something with the data
});
```

### Messages

To send a message from the client to the server, you can use the send method:

```javascript
socket.send('message');
```

To send a message from the server to the client, you can use the send method on the socket object:

```javascript
socket.send('message');
```

To broadcast a message to all connected clients, except for the client that sent the message, you can use the broadcast method:

```javascript
socket.broadcast.send('message');
```

To listen for a message, you can use the on method:

```javascript
socket.on('message', function(data) {
  // do something with the data
});
```

## Conclusion

Socket.io is a great choice for real-time applications. It is easy to use and easy to set up. It also provides a number of features that make it ideal for use in real-time applications.