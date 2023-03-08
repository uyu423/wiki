---
title: 063：使用 TensorFlow.js 和 Node.js 进行实时情感分析
description: 
published: true
date: 2023-02-02T21:43:51.639Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:43:45.469Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [063: Real-Time Sentiment Analysis with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/063-real-time-sentiment-analysis-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 进行实时情感分析

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 构建实时情绪分析应用程序。

## 什么是情感分析？

情感分析是从文本中提取基于观点的信息的过程。这对于各种应用程序都非常有用，例如了解客户反馈或衡量公众对新闻事件的反应。

## 构建应用程序

我们将使用以下工具来构建我们的应用程序：

- [TensorFlow.js](https://js.tensorflow.org/)
- [Node.js](https://nodejs.org/en/)
- [套接字.io](https://socket.io/)

### 设置环境

首先，我们需要设置我们的开发环境。我们将为此项目使用 [Node.js](https://nodejs.org/en/)，因此请确保已安装它。

安装 Node.js 后，我们可以创建一个新的项目目录并使用 [npm](https://www.npmjs.com/) 对其进行初始化：

```
mkdir sentiment-analysis
cd sentiment-analysis
npm init -y
```

这将创建一个名为“sentiment-analysis”的新目录，并使用“package.json”文件对其进行初始化。

接下来，我们需要为我们的项目安装依赖项。我们将使用 [TensorFlow.js](https://js.tensorflow.org/) 和 [Socket.io](https://socket.io/)：

```
npm install @tensorflow/tfjs socket.io
```

这将在我们的项目中安装“@tensorflow/tfjs”和“socket.io”包。

### 创建模型

现在我们已经设置好环境，可以开始构建情绪分析模型了。我们将使用来自 TensorFlow Hub 的[预训练模型](https://tfhub.dev/google/tfjs-models/tfjs-sentiment/2)。

要使用这个模型，我们首先需要将它加载到 TensorFlow.js 中：

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
const model = await tf.loadModel('https://tfhub.dev/google/tfjs-models/tfjs-sentiment/2/default/1');
```

接下来，我们需要创建一个函数，它接受一串文本并返回一个介于 0 和 1 之间的分数，其中 0 为负数，1 为正数。我们可以通过将文本输入模型并获取输出的 argmax 来做到这一点：

```javascript
function getSentiment(text) {
  // Convert the text to a tensor.
  const input = tf.tensor1d([text]);

  // Get the model's predictions.
  const predictions = model.predict(input);

  // Get the highest scoring prediction.
  const argMax = predictions.argMax(-1);

  // We only need the highest scoring prediction's index.
  const index = argMax.dataSync()[0];

  // Get the predicted label.
  const label = (index === 0) ? 'negative' : 'positive';

  // Get the predicted probability.
  const probability = predictions.dataSync()[index];

  return { label, probability };
}
```

现在我们已经建立了模型，我们可以继续创建服务器。

### 创建服务器

我们将使用 [Node.js](https://nodejs.org/) 和 [Socket.io](https://socket.io/) 为我们的应用程序创建服务器。

首先，我们需要依赖项：

```javascript
const tf = require('@tensorflow/tfjs');
const io = require('socket.io')();
```

接下来，我们需要创建一个函数来处理来自套接字的传入文本：

```javascript
function handleText(socket, text) {
  // Get the sentiment of the text.
  const { label, probability } = getSentiment(text);

  // Emit the results to the socket.
  socket.emit('results', { label, probability });
}
```

最后，我们需要启动服务器并监听传入的连接：

```javascript
// Start the server.
io.listen(3000);

// Listen for incoming connections.
io.on('connection', (socket) => {
  // Listen for text from the socket.
  socket.on('text', (text) => handleText(socket, text));
});
```

现在我们已经设置了服务器，我们可以继续创建客户端。

### 创建客户端

我们将使用 [Socket.io](https://socket.io/) 为我们的应用程序创建客户端。

首先，我们需要加载 Socket.io 客户端库：

```html
<script src="/socket.io/socket.io.js"></script>
```

接下来，我们需要创建一个套接字并将其连接到服务器：

```javascript
// Connect to the server.
const socket = io.connect('http://localhost:3000');
```

现在我们已经设置了套接字，我们可以开始向服务器发送文本。我们将通过监听用户输入并将其发送到套接字来完成此操作：

```javascript
// Listen for user input.
document.querySelector('#text-input').addEventListener('input', (event) => {
  // Get the input text.
  const text = event.target.value;

  // Emit the text to the socket.
  socket.emit('text', text);
});
```

最后，我们需要监听服务器的结果并将它们显示给用户：

```javascript
// Listen for results from the server.
socket.on('results', (results) => {
  // Get the results element.
  const element = document.querySelector('#results');

  // Clear the element.
  element.innerHTML = '';

  // Create a new paragraph for each result.
  results.forEach((result) => {
    const { label, probability } = result;
    const paragraph = document.createElement('p');
    paragraph.innerHTML = `${label}: ${probability}`;
    element.appendChild(paragraph);
  });
});
```

现在我们已经设置了客户端，我们可以测试应用程序了。

## 测试应用程序

要测试应用程序，请在浏览器中打开“index.html”。然后，在文本输入中输入一些文本并按回车键。您应该会看到结果出现在 results 元素中。

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 构建实时情绪分析应用程序。我们还了解了如何使用 TensorFlow Hub 中的预训练模型。

如果您有兴趣了解有关情绪分析的更多信息，可以通过以下资源进一步阅读：

- [使用 TensorFlow.js 进行情感分析](https://medium.com/tensorflow/sentiment-analysis-with-tensorflow-js-bccd4d9d4a30)
- [使用 TensorFlow.js 进行实时情感分析](https://www.tensorflow.org/js/tutorials/sentiment/index)