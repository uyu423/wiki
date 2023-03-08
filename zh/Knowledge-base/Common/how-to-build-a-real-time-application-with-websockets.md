---
title: 如何使用 WebSockets 构建实时应用程序
description: 
published: true
date: 2023-02-17T18:03:17.538Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:54:19.545Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [How to Build a Real-Time Application with WebSockets***English** version of this document is available*](/en/Knowledge-base/Common/how-to-build-a-real-time-application-with-websockets)
{.links-list}


# 如何使用 WebSockets 构建实时应用程序

在本文中，我们将向您展示如何使用 WebSockets 构建实时应用程序。我们将介绍 WebSockets 的基础知识以及如何使用它们来创建简单的聊天应用程序。

WebSockets 是一种允许在客户端和服务器之间进行全双工通信的协议。这意味着客户端和服务器可以同时发送和接收数据。 WebSockets 特别适合需要实时通信的应用程序，例如聊天应用程序、多人游戏和协作工具。

## 创建 WebSocket 服务器

要在您的应用程序中使用 WebSocket，您需要创建一个 WebSocket 服务器。您可以使用任何支持 WebSocket 协议的 Web 服务器来执行此操作。出于本文的目的，我们将使用 Node.js Web 服务器。

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

此代码创建一个 WebSocket 服务器，该服务器在端口 8080 上侦听传入连接。建立连接后，服务器会为该连接创建一个 WebSocket 实例。然后服务器监听来自客户端的消息。收到消息后，它会记录到控制台。首次建立连接时，服务器还会向客户端发送一条消息。

WebSocket 服务器可以使用 Node.js 命令行界面运行。

```
node server.js
```

## 创建 WebSocket 客户端

现在我们已经启动并运行了一个 WebSocket 服务器，我们需要创建一个 WebSocket 客户端来连接它。出于本文的目的，我们将使用基于浏览器的 JavaScript 客户端。

```javascript
var ws = new WebSocket('ws://localhost:8080');

ws.onopen = function() {
  ws.send('Hello, world!');
};

ws.onmessage = function(event) {
  console.log(event.data);
};
```

此代码创建一个 WebSocket 实例并将其连接到 WebSocket 服务器。该代码还定义了两个事件处理程序。第一个事件处理程序用于 ```open``` event. This event is fired when the connection is established. The second event handler is for the ```message``` event. This event is fired when the server sends a message to the client.

## Sending and Receiving Messages

Now that we have a WebSocket server and client set up, we can start sending and receiving messages. The ```send``` method can be used to send messages from the client to the server. The ```onmessage``` event handler can be used to receive messages from the server.

```javascript
ws.send('你好，世界！');

ws.onmessage = 函数（事件）{
  控制台日志（事件数据）；
};
```

In this code, the ```send``` 方法用于从客户端向服务器发送消息。 ```onmessage``` 事件处理程序用于从服务器接收消息。该消息被记录到控制台。