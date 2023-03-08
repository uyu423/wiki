---
title: 084：在 Node.js 中使用 TensorFlow.js 和其他 JavaScript 库
description: 
published: true
date: 2023-02-03T02:37:09.769Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:37:08.084Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [084: Using TensorFlow.js with Other JavaScript Libraries in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/084-using-tensorflow-js-with-other-javascript-libraries-in-node-js)
{.links-list}


# 在 Node.js 中将 TensorFlow.js 与其他 JavaScript 库一起使用

TensorFlow.js 是一个强大的 JavaScript 机器学习工具，它与其他 JavaScript 库配合得很好。在本文中，我们将向您展示如何将 TensorFlow.js 与 Node.js 和 Express 结合使用。

## 先决条件

要跟进这篇文章，您需要一些东西：

- 安装了 Node.js 和 npm
- 文本编辑器 - 我们推荐 Visual Studio Code
- JavaScript的基础知识

## 入门

首先，让我们为我们的项目创建一个新目录：

```
mkdir tensorflowjs-node
cd tensorflowjs-node
```

接下来，我们将使用 npm 初始化我们的项目：

```
npm init -y
```

现在我们的项目已经建立，我们可以安装我们需要的依赖项。我们将使用以下库：

- [TensorFlow.js](https://www.tensorflow.org/js)
- [快递](https://expressjs.com/)
- [正文解析器](https://www.npmjs.com/package/body-parser)

我们可以使用以下命令安装这些依赖项：

```
npm install --save @tensorflow/tfjs express body-parser
```

## 你好，TensorFlow.js！

现在我们已经安装了依赖项，我们可以开始编写一些代码了。让我们首先创建一个名为“index.js”的文件。在这个文件中，我们将编写一个简单的脚本来打印“Hello, TensorFlow.js!”到控制台：

```javascript
// index.js

const tf = require('@tensorflow/tfjs');

console.log('Hello, TensorFlow.js!');
```

如果我们使用 Node.js 运行这个脚本，我们应该看到以下输出：

```
$ node index.js
Hello, TensorFlow.js!
```

## 将 TensorFlow.js 与 Express 结合使用

现在我们已经了解了如何在 Node.js 脚本中使用 TensorFlow.js，让我们来看看如何将它与 Express 一起使用。对于这个例子，我们将创建一个简单的服务器来响应带有数字列表的“GET”请求。

首先，让我们要求我们需要的依赖项：

```javascript
// index.js

const tf = require('@tensorflow/tfjs');
const express = require('express');
const bodyParser = require('body-parser');
```

接下来，我们将创建一个 Express 实例并配置 body-parser 来解析 JSON 主体：

```javascript
// index.js

const app = express();
app.use(bodyParser.json());
```

现在，让我们定义一个路由来响应带有数字列表的“GET”请求：

```javascript
// index.js

app.get('/numbers', (req, res) => {
  const numbers = [1, 2, 3, 4, 5];
  res.json(numbers);
});
```

最后，我们将在端口“3000”上启动服务器：

```javascript
// index.js

app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

如果我们使用 Node.js 运行这个脚本，我们应该看到以下输出：

```
$ node index.js
Server is listening on port 3000
```

我们现在可以向 `http://localhost:3000/numbers` 发送 `GET` 请求，我们将收到带有数字列表的 JSON 响应。

## 将 TensorFlow.js 与 Express 和 body-parser 结合使用

在上一节中，我们了解了如何将 TensorFlow.js 与 Express 结合使用。在本节中，我们将扩展示例以展示如何使用“body-parser”来解析 JSON 主体。

首先，让我们要求我们需要的依赖项：

```javascript
// index.js

const tf = require('@tensorflow/tfjs');
const express = require('express');
const bodyParser = require('body-parser');
```

接下来，我们将创建一个 Express 实例并配置 body-parser 来解析 JSON 主体：

```javascript
// index.js

const app = express();
app.use(bodyParser.json());
```

现在，让我们定义一个路由，该路由将使用请求的主体响应 POST 请求：

```javascript
// index.js

app.post('/body', (req, res) => {
  res.json(req.body);
});
```

最后，我们将在端口“3000”上启动服务器：

```javascript
// index.js

app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

如果我们使用 Node.js 运行这个脚本，我们应该看到以下输出：

```
$ node index.js
Server is listening on port 3000
```

我们现在可以将带有 JSON 正文的 POST 请求发送到 http://localhost:3000/body，我们将收到带有请求正文的 JSON 响应。

## 将 TensorFlow.js 与 Express 和 body-parser 结合使用

在上一节中，我们了解了如何将 TensorFlow.js 与 Express 和 body-parser 结合使用。在本节中，我们将扩展示例以展示如何使用 TensorFlow.js 对请求正文执行推理。

首先，让我们要求我们需要的依赖项：

```javascript
// index.js

const tf = require('@tensorflow/tfjs');
const express = require('express');
const bodyParser = require('body-parser');
```

接下来，我们将创建一个 Express 实例并配置 body-parser 来解析 JSON 主体：

```javascript
// index.js

const app = express();
app.use(bodyParser.json());
```

现在，让我们定义一个路由，该路由将使用请求的主体响应 POST 请求：

```javascript
// index.js

app.post('/inference', (req, res) => {
  const input = tf.tensor(req.body);
  const output = tf.add(input, 1);
  res.json(output.dataSync());
});
```

最后，我们将在端口“3000”上启动服务器：

```javascript
// index.js

app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

如果我们使用 Node.js 运行这个脚本，我们应该看到以下输出：

```
$ node index.js
Server is listening on port 3000
```

我们现在可以将 POST 请求发送到带有 JSON 正文的 http://localhost:3000/inference ，我们将收到带有推理结果的 JSON 响应。

## 包起来

在本文中，我们了解了如何将 TensorFlow.js 与 Node.js 和 Express 结合使用。我们还看到了如何使用 TensorFlow.js 和 body-parser 来解析 JSON 主体。

## 资源

- [TensorFlow.js](https://www.tensorflow.org/js)
- [快递](https://expressjs.com/)
- [正文解析器](https://www.npmjs.com/package/body-parser)