---
title: 060：在 Node.js 中使用 TensorFlow.js 和 WebRTC
description: 
published: true
date: 2023-02-02T21:05:32.363Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:05:30.663Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [060: Using TensorFlow.js with WebRTC in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/060-using-tensorflow-js-with-webrtc-in-node-js)
{.links-list}


# 在 Node.js 中使用 TensorFlow.js 和 WebRTC

在本文中，我们将向您展示如何在 Node.js 中将 TensorFlow.js 与 WebRTC 结合使用。我们将介绍如何设置您的开发环境、如何将 TensorFlow.js 与 WebRTC 结合使用以及如何部署您的应用程序。

## 设置你的开发环境

在我们开始之前，我们需要设置我们的开发环境。我们需要安装 Node.js 和 TensorFlow.js Node.js 库。

### 安装 Node.js

首先，我们需要安装 Node.js。您可以从 [Node.js 网站](https://nodejs.org/en/) 下载 Node.js 安装程序。运行安装程序，并按照提示安装 Node.js。

安装 Node.js 后，您可以通过打开终端并运行以下命令来验证它是否正常工作：

```
node -v
```

您应该会看到打印到终端的 Node.js 版本号。

### 安装 TensorFlow.js Node.js 库

现在我们已经安装了 Node.js，我们可以安装 TensorFlow.js Node.js 库。我们可以使用 Node.js 包管理器 npm 来完成此操作。

首先，我们需要创建一个 package.json 文件。该文件将包含有关我们项目的信息，包括我们要安装的依赖项。我们可以使用以下命令创建一个 package.json 文件：

```
npm init
```

这将提示您提供有关项目的一些信息。您可以按 enter 键接受默认值。

接下来，我们需要安装 TensorFlow.js Node.js 库。我们可以使用以下命令执行此操作：

```
npm install @tensorflow/tfjs-node
```

这将安装 TensorFlow.js Node.js 库和它需要的任何其他依赖项。

## 将 TensorFlow.js 与 WebRTC 结合使用

现在我们已经设置了开发环境，我们可以开始将 TensorFlow.js 与 WebRTC 结合使用。

WebRTC 是一种允许浏览器之间进行实时通信的技术。 TensorFlow.js 是一个用于机器学习的 JavaScript 库。这两种技术可以一起用于构建可以执行实时机器学习的应用程序。

### 入门

首先，我们需要创建一个 HTML 文件。我们可以使用 [VS Code](https://code.visualstudio.com/) 等文本编辑器来完成此操作。

在此文件中，我们需要包含 TensorFlow.js 库。我们可以通过将以下脚本标记添加到我们的 HTML 文件的头部来做到这一点：

```html
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.3/dist/tf.min.js"></script>
```

我们还需要包括 WebRTC 适配器。这是一个 JavaScript 库，可在不同浏览器的 WebRTC 实现之间提供兼容性。我们可以使用以下脚本标签包含 WebRTC 适配器：

```html
<script src="https://webrtc.github.io/adapter/adapter-latest.js"></script>
```

我们还需要包含 TensorFlow.js Node.js 库。我们可以使用脚本标签来做到这一点：

```html
<script src="./node_modules/@tensorflow/tfjs-node/dist/tfjs-node.js"></script>
```

### 创建 WebRTC 连接

现在我们已经包含了 TensorFlow.js 和 WebRTC 库，我们可以开始使用它们了。

首先，我们需要创建一个 WebRTC 连接。我们可以使用以下代码来做到这一点：

```javascript
// Get the user's media stream
navigator.mediaDevices.getUserMedia({ video: true, audio: true })
  .then(function (mediaStream) {
    // Create a WebRTC connection
    const peerConnection = new RTCPeerConnection();

    // Add the media stream to the connection
    peerConnection.addStream(mediaStream);

    // Create an offer
    peerConnection.createOffer()
      .then(function (offer) {
        // Set the offer as the local description
        peerConnection.setLocalDescription(offer);

        // Send the offer to the remote peer
        // ...
      });
  });
```

在这段代码中，我们首先获取用户的媒体流。这将使我们能够访问用户的网络摄像头和麦克风。然后我们创建一个 WebRTC 连接。此连接将用于将用户的浏览器连接到远程对等点。

接下来，我们将用户的媒体流添加到连接中。这将允许远程对等点看到和听到用户。

然后，我们创建报价。这是对用户媒体流和用户浏览器能力的描述。我们将此报价设置为本地描述。这将由远程对等方用于连接到用户。

最后，我们将报价发送给远程对等方。远程对等点将使用此提议连接到用户。

### 收到报价

现在我们已经了解了如何创建报价，让我们来看看如何接收报价。

当远程对等方向我们发送报价时，我们需要将其设置为远程描述。我们可以使用以下代码来做到这一点：

```javascript
// Get the user's media stream
navigator.mediaDevices.getUserMedia({ video: true, audio: true })
  .then(function (mediaStream) {
    // Create a WebRTC connection
    const peerConnection = new RTCPeerConnection();

    // Add the media stream to the connection
    peerConnection.addStream(mediaStream);

    // When we receive an offer
    peerConnection.on('offer', function (offer) {
      // Set the offer as the remote description
      peerConnection.setRemoteDescription(offer);

      // Create an answer
      peerConnection.createAnswer()
        .then(function (answer) {
          // Set the answer as the local description
          peerConnection.setLocalDescription(answer);

          // Send the answer to the remote peer
          // ...
        });
    });
  });
```

在这段代码中，我们首先获取用户的媒体流。这将使我们能够访问用户的网络摄像头和麦克风。然后我们创建一个 WebRTC 连接。此连接将用于将用户的浏览器连接到远程对等点。

接下来，我们将用户的媒体流添加到连接中。这将允许远程对等点看到和听到用户。

然后，我们在收到报价时设置一个事件监听器。当我们收到报价时，我们将其设置为远程描述。

最后，我们创建一个答案。这是对用户媒体流和用户浏览器能力的描述。我们将此答案设置为本地描述。这将由远程对等方用于连接到用户。

### 发送一个答案

现在我们已经了解了如何创建答案，让我们来看看如何发送答案。

当远程对等端向我们发送应答时，我们需要将其设置为远程描述。我们可以使用以下代码来做到这一点：

```javascript
// Get the user's media stream
navigator.mediaDevices.getUserMedia({ video: true, audio: true })
  .then(function (mediaStream) {
    // Create a WebRTC connection
    const peerConnection = new RTCPeerConnection();

    // Add the media stream to the connection
    peerConnection.addStream(mediaStream);

    // When we receive an answer
    peerConnection.on('answer', function (answer) {
      // Set the answer as the remote description
      peerConnection.setRemoteDescription(answer);
    });

    // Create an offer
    peerConnection.createOffer()
      .then(function (offer) {
        // Set the offer as the local description
        peerConnection.setLocalDescription(offer);

        // Send the offer to the remote peer
        // ...
      });
  });
```

在这段代码中，我们首先获取用户的媒体流。这将使我们能够访问用户的网络摄像头和麦克风。然后我们创建一个 WebRTC 连接。此连接将用于将用户的浏览器连接到远程对等点。

接下来，我们将用户的媒体流添加到连接中。这将允许远程对等点看到和听到用户。

然后，我们设置一个事件侦听器，以便在我们收到答复时使用。当我们收到答案时，我们将其设置为远程描述。

最后，我们创建一个报价。这是对用户媒体流和用户浏览器能力的描述。我们将此报价设置为本地描述。这将由远程对等方用于连接到用户。

## 部署你的应用程序

现在我们已经了解了如何将 TensorFlow.js 与 WebRTC 结合使用，让我们来看看如何部署我们的应用程序。

我们需要使用网络服务器来提供我们的 HTML 文件。我们可以使用 [Node.js HTTP 模块](https://nodejs.org/api/http.html) 来做到这一点。

首先，我们需要创建一个名为 server.js 的文件。在这个文件中，我们需要 `http` 模块并创建一个 HTTP 服务器。我们可以使用以下代码来做到这一点：

```javascript
const http = require('http');

const server = http.createServer(function (request, response) {
  // Serve the HTML file
  // ...
});

server.listen(8080);
```

在这段代码中，我们需要 `http` 模块。该模块将使我们能够访问 HTTP 服务器和客户端。然后我们创建一个 HTTP 服务器。该服务器将用于提供我们的 HTML 文件。

接下来，我们需要告诉服务器要提供什么文件。我们可以通过将以下代码添加到 createServer 回调中来完成此操作：

```javascript
const fs = require('fs');

const index = fs.readFileSync('./index.html');

response.writeHead(200, { 'Content-Type': 'text/html' });
response.end(index);
```

在这段代码中，我们需要 `fs` 模块。该模块将使我们能够访问文件系统。然后我们将 HTML 文件的内容读入一个变量。

最后，我们将 HTML 文件的内容写入响应。我们还将“Content-Type”标头设置为“text/html”。这将告诉浏览器该文件是一个 HTML 文件。

## 结论

在本文中，我们向您展示了如何在 Node.js 中将 TensorFlow.js 与 WebRTC 结合使用。我们已经了解了如何设置您的开发环境、如何将 TensorFlow.js 与 WebRTC 结合使用以及如何部署您的应用程序。