---
title: 059：在 Node.js 中将 TensorFlow.js 与 WebSockets 集成
description: 
published: true
date: 2023-02-02T20:44:16.079Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:44:11.378Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [059: Integrating TensorFlow.js with WebSockets in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/059-integrating-tensorflow-js-with-websockets-in-node-js)
{.links-list}


# 059：在 Node.js 中将 TensorFlow.js 与 WebSockets 集成

TensorFlow.js 是用于在浏览器中训练和部署机器学习模型的强大工具。然而，由于可用资源有限，浏览器中的训练模型可能会很慢且效率低下。

加速训练的一种方法是使用 WebSockets 将数据发送到服务器进行训练。这样，服务器可以使用其资源更快地训练模型。

在本文中，我们将向您展示如何设置 Node.js 服务器并使用 WebSockets 将数据发送到服务器以训练 TensorFlow.js 模型。

## 先决条件

在我们开始之前，您需要做一些事情：

- 文本编辑器。我们推荐 [Visual Studio Code](https://code.visualstudio.com/)。
- [Node.js](https://nodejs.org/en/) 安装在您的计算机上。
- [NPM](https://www.npmjs.com/)（Node.js 附带）安装在您的计算机上。
- [TensorFlow.js](https://js.tensorflow.org/) 安装在您的计算机上。

## 设置 Node.js 服务器

首先，我们需要设置一个 Node.js 服务器。我们将使用 [Express](https://expressjs.com/) 网络框架让事情变得更简单。

创建一个名为“server.js”的新文件并将以下代码粘贴到其中：

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => res.send('Hello World!'));

app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```

此代码创建一个基本的 Express 服务器，它侦听端口 3000。

接下来，我们需要为我们的服务器安装依赖项。在您的终端中，导航到 `server.js` 所在的目录并运行以下命令：

```
npm install express --save
```

这将安装 Express 框架并将其作为依赖项保存在我们的 package.json 文件中。

现在我们的服务器已经设置好了，我们可以通过在终端中运行以下命令来启动它：

```
node server.js
```

您应该看到以下输出：

```
Example app listening on port 3000!
```

## 向服务器发送数据

现在我们的服务器已经启动并运行，我们可以开始向它发送数据了。我们将使用 [WebSockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) 将数据从浏览器发送到服务器。

首先，我们需要安装 [ws](https://github.com/websockets/ws) WebSocket 库。在您的终端中，导航到 `server.js` 所在的目录并运行以下命令：

```
npm install ws --save
```

这将安装 `ws` 库并将其作为依赖项保存在我们的 `package.json` 文件中。

接下来，我们需要修改我们的 server.js 文件以使用 ws 库。用以下代码替换 `server.js` 的内容：

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

此代码创建一个新的 WebSocket 服务器，它侦听端口 8080。建立连接后，服务器将记录它收到的任何消息。

现在我们的服务器已设置为接收数据，我们可以编写一些代码来向它发送数据。创建一个名为“client.html”的新文件并将以下代码粘贴到其中：

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

此代码创建一个新的 WebSocket 连接到我们的服务器，并在连接打开时发送一条消息。它还记录它收到的任何消息。

在浏览器中打开“client.html”，您应该会在控制台中看到以下输出：

```
Hello!
```

## 发送数据到服务器进行训练

现在我们可以将数据发送到我们的服务器，我们可以使用它来训练 TensorFlow.js 模型。我们将使用 [Iris 数据集](https://en.wikipedia.org/wiki/Iris_flower_data_set) 来训练一个简单的分类模型。

首先，我们需要修改我们的 server.js 文件以包含 TensorFlow.js 库。用以下代码替换 `server.js` 的内容：

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

此代码包含 TensorFlow.js 库并创建基本分类模型。

接下来，我们需要修改我们的 `client.html` 文件以将数据发送到服务器进行训练。用以下代码替换 `client.html` 的内容：

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

此代码在连接打开时向服务器发送数据。它还记录它收到的任何消息。

在浏览器中打开“client.html”，您应该会在控制台中看到以下输出：

```
Received message => 1,2,3,4
```

## 结论

在本文中，我们向您展示了如何设置 Node.js 服务器并使用 WebSockets 将数据发送到服务器以训练 TensorFlow.js 模型。

这是在浏览器中训练机器学习模型的一种强大方式。通过使用服务器的资源，我们可以更快、更高效地训练模型。