---
title: 081：使用 TensorFlow.js 和 Node.js 构建交互式可视化
description: 
published: true
date: 2023-02-03T01:44:02.563Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:44:00.866Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [081: Building Interactive Visualizations with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/081-building-interactive-visualizations-with-tensorflow-js-and-node-js)
{.links-list}


# 081：使用 TensorFlow.js 和 Node.js 构建交互式可视化

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 构建交互式可视化。

TensorFlow.js 是一个功能强大的 JavaScript 库，用于数值计算，支持在浏览器中进行机器学习。 Node.js 是一个 JavaScript 运行时，允许您在浏览器之外运行 JavaScript 代码。

这两种技术可以一起用于构建可用于探索和分析数据的交互式可视化。

## 入门

首先，您需要安装 Node.js 和 TensorFlow.js。

Node.js可以从官网下载安装：https://nodejs.org/en/

可以使用 Node.js 包管理器安装 TensorFlow.js：

```
npm install @tensorflow/tfjs
```

## 你好世界

安装 Node.js 和 TensorFlow.js 后，您可以使用以下代码创建一个简单的“Hello World”程序：

```javascript
// Load the TensorFlow.js library
const tf = require('@tensorflow/tfjs');

// Define a TensorFlow.js graph
tf.tensor([1, 2, 3, 4]).print();
```

将上面的代码保存在名为“hello.js”的文件中，并使用 Node.js 运行时运行它：

```
node hello.js
```

您应该看到以下输出：

```
Tensor
    [[1, 2, 3, 4]]
```

 恭喜！您刚刚运行了第一个 TensorFlow.js 程序。

## 构建交互式可视化

现在我们已经了解了如何开始使用 TensorFlow.js 和 Node.js，让我们看看如何使用这些技术来构建交互式可视化。

我们将使用以下库来构建我们的可视化：

- TensorFlow.js：用于数值计算和机器学习
- Node.js：用于在浏览器之外运行 JavaScript 代码
- Express：用于创建网络服务器
- Socket.IO：用于网络服务器和浏览器之间的实时通信

我们的可视化将是一个实时更新的简单折线图。

### 定义数据

首先，让我们定义要可视化的数据。我们将使用 TensorFlow.js 图表生成随机数据点。

```javascript
// Define a TensorFlow.js graph that generates random data
const data = tf.tensor(new Array(100).fill(0).map(() => Math.random()));
```

上面的代码定义了一个生成 100 个随机数据点的 TensorFlow.js 图。

### 创建网络服务器

接下来，让我们使用 Node.js 和 Express 创建一个 Web 服务器。

```javascript
// Load the Express.js library
const express = require('express');

// Create an Express.js app
const app = express();

// Define the port that the app will listen on
const port = 3000;

// Start the Express.js app
app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```

上面的代码创建了一个侦听端口 3000 的 Express.js 应用程序。

### 提供 HTML 页面

现在我们已经启动并运行了 Web 服务器，让我们提供一个 HTML 页面，该页面将用于显示我们的可视化效果。

```javascript
// Serve the HTML page
app.get('/', (req, res) => res.sendFile(__dirname + '/index.html'));
```

上面的代码定义了一个在访问根 URL 时为 HTML 页面提供服务的路由。

HTML 页面应包含以下内容：

```html
<!DOCTYPE html>
<html>
  <head>
    <title>081: Building Interactive Visualizations with TensorFlow.js and Node.js</title>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.0/dist/tf.min.js"></script>
    <script src="https://cdn.socket.io/socket.io-1.4.5.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.7.3/Chart.min.js"></script>
  </head>
  <body>
    <canvas id="chart"></canvas>
    <script>
      // Your code here
    </script>
  </body>
</html>
```

HTML 页面包括以下库：

- TensorFlow.js：用于数值计算和机器学习
- Socket.IO：用于网络服务器和浏览器之间的实时通信
- Chart.js：用于创建图表和图形

HTML 页面还包括将用于显示折线图的```<canvas>``` 元素。

### 将数据发送到浏览器

现在我们已经启动并运行了 Web 服务器，并且我们正在为 HTML 页面提供服务，让我们将数据发送到浏览器。

我们将使用 Socket.IO 在 Web 服务器和浏览器之间建立实时连接。

```javascript
// Load the Socket.IO library
const io = require('socket.io')(server);

// Send the data to the browser
io.on('connection', socket => {
  setInterval(() => {
    socket.emit('data', data.toArray());
  }, 1000);
});
```

上面的代码使用 Socket.IO 每秒向浏览器发送数据。

### 在浏览器中接收数据

现在我们正在浏览器中接收数据，让我们使用 Chart.js 将其可视化。

```javascript
// Connect to the socket.io server
const socket = io('http://localhost:3000');

// Receive the data from the server
socket.on('data', data => {
  // Visualize the data using Chart.js
  const chart = new Chart(document.getElementById('chart'), {
    type: 'line',
    data: {
      labels: data.map((_, i) => i),
      datasets: [{
        label: 'Random Data',
        data: data,
        borderColor: '#ff0000',
        fill: false
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false
    }
  });
});
```

上面的代码使用 Chart.js 将数据可视化为折线图。当收到新的数据点时，图表会实时更新。

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 构建交互式可视化。

TensorFlow.js 是一个功能强大的 JavaScript 库，用于数值计算，支持在浏览器中进行机器学习。 Node.js 是一个 JavaScript 运行时，允许您在浏览器之外运行 JavaScript 代码。

这两种技术可以一起用于构建可用于探索和分析数据的交互式可视化。