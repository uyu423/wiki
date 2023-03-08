---
title: 067：使用 TensorFlow.js 和 Node.js 创建桌面应用程序
description: 
published: true
date: 2023-02-02T22:36:28.229Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:36:26.665Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [067: Creating Desktop Applications with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/067-creating-desktop-applications-with-tensorflow-js-and-node-js)
{.links-list}


# 067：使用 TensorFlow.js 和 Node.js 创建桌面应用程序

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 创建桌面应用程序。

TensorFlow.js 是一个强大的 JavaScript 机器学习工具。 Node.js 是一个 JavaScript 运行时，允许您在浏览器之外运行 JavaScript 代码。

这两种技术可以一起用于创建使用机器学习的桌面应用程序。

## 入门

首先，您需要安装 Node.js 和 TensorFlow.js。

Node.js 可以从 [Node.js 网站](https://nodejs.org/en/) 下载。可以使用 [Node.js 包管理器](https://www.npmjs.com/) 安装 TensorFlow.js：

```
npm install @tensorflow/tfjs
```

安装 Node.js 和 TensorFlow.js 后，您就可以开始创建桌面应用程序了。

## 创建桌面应用程序

要使用 TensorFlow.js 和 Node.js 创建桌面应用程序，您需要创建一个 Node.js 文件和一个 HTML 文件。

Node.js 文件将用于运行您的机器学习代码。 HTML 文件将用于显示机器学习代码的结果。

我们将从创建一个名为“main.js”的 Node.js 文件开始。在此文件中，我们将需要 TensorFlow.js 库并加载预训练模型。

```javascript
const tf = require('@tensorflow/tfjs');

// Load a pre-trained model.
const model = tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

接下来，我们将创建一个名为“index.html”的 HTML 文件。在此文件中，我们将包含以下代码：

```html
<html>
  <head>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs"></script>
    <script src="main.js"></script>
  </head>
  <body>
    <h1>Hello, TensorFlow.js!</h1>
  </body>
</html>
```

此代码包括 TensorFlow.js 库和 `main.js` 文件。它还包含一个简单的“<h1>”标签。

最后，我们需要使用 Node.js 运行 index.html 文件。我们可以通过运行以下命令来完成此操作：

```
node index.html
```

这将启动本地服务器并在您的默认网络浏览器中打开“index.html”文件。

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 创建桌面应用程序。我们还了解了如何加载预训练模型并在 Node.js 文件中运行它。

如果您有兴趣了解有关 TensorFlow.js 和 Node.js 的更多信息，我建议您查看以下资源：

- [TensorFlow.js 入门](https://js.tensorflow.org/tutorials/getting-started.html)
- [TensorFlow.js 初学者](https://www.youtube.com/watch?v=HEQDRWMK6yY)
- [Node.js 初学者](https://www.youtube.com/watch?v=U8XF6AFGqlc)