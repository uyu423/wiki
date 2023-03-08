---
title: 使用 Node.js 和 WebSockets 进行实时通信
description: 
published: true
date: 2023-02-17T01:55:39.089Z
tags: 
editor: markdown
dateCreated: 2023-02-17T01:55:30.792Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Working with Node.js and WebSockets for Real-Time Communication***English** document is available*](/en/Knowledge-base/Nodejs/working-with-node-js-and-websockets-for-real-time-communication)
{.links-list}


      IT开发学习博客

# 使用 Node.js 和 WebSockets 进行实时通信

Node.js 是一个 Javascript 运行时环境，允许您在浏览器之外运行 Javascript 代码。它用途广泛，可用于开发服务器端应用程序、命令行工具，甚至桌面应用程序。

WebSockets 是一种 Web 技术，允许在客户端和服务器之间进行全双工、双向通信。它专为实时通信而设计，常用于聊天应用程序、协作编辑应用程序和游戏应用程序等应用程序中。

在本文中，我们将探讨如何使用 Node.js 和 WebSockets 进行实时通信。我们将讨论如何设置可以处理 WebSocket 请求的 Node.js 服务器，我们还将构建一个使用 WebSocket 进行实时通信的简单聊天应用程序。

## 设置 Node.js 服务器

我们将使用 [ws](https://www.npmjs.com/package/ws) npm 包在 Node.js 中使用 WebSockets。

首先，我们需要安装 `ws` 包：

```
npm install ws
```

接下来，我们需要创建一个名为 server.js 的文件并添加以下代码：

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

在上面的代码中，我们使用 `ws` 包在端口 8080 上创建一个 WebSocket 服务器。我们还处理 `connection` 事件，当客户端连接到服务器时会触发该事件。建立连接后，我们会为“消息”事件设置一个事件处理程序，该事件会在收到来自客户端的消息时触发。最后，我们在建立连接时向客户端发送消息。

要运行服务器，我们可以使用以下命令：

```
node server.js
```

## 创建聊天应用程序

现在我们有了一个可以处理 WebSocket 请求的 Node.js 服务器，让我们构建一个使用 WebSocket 进行实时通信的简单聊天应用程序。

首先，我们需要创建一个名为 `client.html` 的文件并添加以下代码：

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

在上面的代码中，我们使用 HTML 和 Javascript 创建了一个简单的聊天应用程序。我们正在使用 `WebSocket` API 与服务器建立连接，我们正在使用 `message` 事件从服务器接收消息并将其显示在浏览器中。我们还使用 `send` 方法向服务器发送消息。

## 结论

在本文中，我们探讨了如何使用 Node.js 和 WebSockets 进行实时通信。我们设置了一个可以处理 WebSocket 请求的 Node.js 服务器，我们还构建了一个使用 WebSockets 进行实时通信的简单聊天应用程序。