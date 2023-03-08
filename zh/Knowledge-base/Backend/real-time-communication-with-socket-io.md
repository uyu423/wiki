---
title: 与 Socket.io 的实时通信
description: 
published: true
date: 2023-02-17T06:17:33.604Z
tags: 
editor: markdown
dateCreated: 2023-02-17T06:17:29.281Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Real-time Communication with Socket.io***English** document is available*](/en/Knowledge-base/Backend/real-time-communication-with-socket-io)
{.links-list}



# 与 Socket.io 的实时通信

在本文中，我们将讨论与 Socket.io 的实时通信。 Socket.io 是一个 JavaScript 库，可在 Web 客户端和服务器之间提供实时双向通信。它具有许多使其成为实时应用程序的理想选择的特性，例如实时消息传递、聊天、游戏等。

Socket.io 基于 WebSocket 协议，使用 Node.js 平台。它易于使用和设置，是实时应用程序的绝佳选择。

## 设置 Socket.io

要使用 Socket.io，您需要安装 socket.io 模块。您可以使用节点包管理器 (NPM) 执行此操作：

```
npm install socket.io
```

安装模块后，您可以在 Node.js 应用程序中要求它：

```javascript
var io = require('socket.io')();
```

socket.io 模块返回一个函数，您可以使用 http 服务器实例调用该函数。这将为您设置 socket.io 通信。

## 使用 Socket.io

Socket.io 提供了两种通信方式：

* 事件：您可以将事件从客户端发送到服务器，或从服务器发送到客户端。事件可以任意命名，并且可以携带数据。
* 消息：您可以在客户端和服务器之间发送消息。消息类似于事件，但它们以特定格式发送，允许发送不同类型的数据（例如二进制数据）。

### 活动

要从客户端向服务器发出事件，可以使用 emit 方法：

```javascript
socket.emit('eventName', data);
```

要从服务器向客户端发出事件，您可以在套接字对象上使用 emit 方法：

```javascript
socket.emit('eventName', data);
```

您还可以向所有连接的客户端广播事件，但发出事件的客户端除外。为此，您可以使用广播方法：

```javascript
socket.broadcast.emit('eventName', data);
```

要监听一个事件，你可以使用 on 方法：

```javascript
socket.on('eventName', function(data) {
  // do something with the data
});
```

### 消息

要从客户端向服务器发送消息，可以使用 send 方法：

```javascript
socket.send('message');
```

要从服务器向客户端发送消息，您可以在套接字对象上使用 send 方法：

```javascript
socket.send('message');
```

要向所有连接的客户端广播消息，除了发送消息的客户端，可以使用广播方法：

```javascript
socket.broadcast.send('message');
```

要收听消息，您可以使用 on 方法：

```javascript
socket.on('message', function(data) {
  // do something with the data
});
```

## 结论

Socket.io 是实时应用程序的绝佳选择。它易于使用且易于设置。它还提供了许多使其成为实时应用程序的理想选择的特性。