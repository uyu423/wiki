---
title: 054：使用 TensorFlow.js 和 Node.js 创建 REST API
description: 
published: true
date: 2023-02-02T19:36:27.167Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:36:25.586Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [054: Creating REST APIs with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/054-creating-rest-apis-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 创建 REST API

## 介绍

在本文中，我们将向您展示如何使用 TensorFlow.js 和 Node.js 创建 REST API。我们将介绍启动和运行项目所需的所有步骤，包括安装所需的依赖项、设置项目和编写代码。

在本文结束时，您将能够使用 TensorFlow.js 和 Node.js 创建自己的 REST API。

## 先决条件

在我们开始之前，您需要做一些事情才能跟进：

- 文本编辑器。我们推荐 [Visual Studio Code](https://code.visualstudio.com/)。
- [Node.js](https://nodejs.org/en/) 安装在您的机器上。
- [npm](https://www.npmjs.com/) 安装在您的机器上。
- [TensorFlow.js](https://js.tensorflow.org/) 安装在您的机器上。

## 设置你的项目

设置好先决条件后，您就可以开始设置项目了。

首先，为您的项目创建一个新目录。我们将调用我们的 `tfjs-rest-api`。

接下来，通过在项目目录中运行“npm init”来初始化项目。这将为您的项目创建一个“package.json”文件。

现在您有了一个 `package.json` 文件，您可以为您的项目安装依赖项。运行以下命令安装[Express](https://expressjs.com/)、[Body-Parser](https://www.npmjs.com/package/body-parser)和[TensorFlow.js]( https://www.npmjs.com/package/@tensorflow/tfjs）：

```
npm install express body-parser @tensorflow/tfjs --save
```

这将安装依赖项并将它们添加到您的 `package.json` 文件中。

## 编写代码

现在您已经设置了项目，可以开始编写代码了。

打开文本编辑器并在项目目录中创建一个新文件。我们将调用我们的 `index.js`。

在这个文件中，我们首先需要我们之前安装的依赖项：

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const tf = require('@tensorflow/tfjs');
```

接下来，我们将设置我们的 Express 服务器：

```javascript
const app = express();
const port = 3000;

app.use(bodyParser.json());

app.listen(port, () => {
  console.log(`Server listening on port ${port}`);
});
```

现在我们的服务器已经设置好了，我们可以开始编写我们的 API 端点了。

我们的第一个端点将是对 `/` 的 `GET` 请求，它将返回一条简单的消息：

```javascript
app.get('/', (req, res) => {
  res.send('Hello, world!');
});
```

我们的第二个端点将是对 `/predict` 的 `POST` 请求，它将接收一个数字数组并返回基于这些数字的预测：

```javascript
app.post('/predict', (req, res) => {
  const input = tf.tensor2d([req.body.numbers], [1, req.body.numbers.length]);
  const output = model.predict(input);
  res.send(output.dataSync());
});
```

在此端点中，我们使用预训练的 [TensorFlow.js](https://js.tensorflow.org/) 模型进行预测。您可以在 [此处](https://storage.googleapis.com/tfjs-models/tfjs/mnist_model/model.json) 找到此模型。

## 测试你的 API

现在您已经设置了 API 端点，可以开始测试它们了。

要测试您的“GET”端点，您可以使用 [Postman](https://www.getpostman.com/) 等工具。

要测试您的 `POST` 端点，您可以使用以下命令：

```
curl -X POST -H "Content-Type: application/json" -d '{"numbers": [1, 2, 3, 4, 5]}' http://localhost:3000/predict
```

这应该返回“[6]”的预测。

## 结论

在本文中，我们向您展示了如何使用 TensorFlow.js 和 Node.js 创建 REST API。我们涵盖了启动和运行项目所需的所有步骤，包括安装所需的依赖项、设置项目和编写代码。

到本文结束时，您应该能够使用 TensorFlow.js 和 Node.js 创建自己的 REST API。