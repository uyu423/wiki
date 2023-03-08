---
title: 055：在 Node.js 中集成 TensorFlow.js 和 MongoDB
description: 
published: true
date: 2023-02-02T19:43:49.243Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:43:44.592Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [055: Integrating TensorFlow.js with MongoDB in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/055-integrating-tensorflow-js-with-mongodb-in-node-js)
{.links-list}


# 05：在 Node.js 中集成 TensorFlow.js 和 MongoDB

在本文中，我们将学习如何在 Node.js 中将 TensorFlow.js 与 MongoDB 集成。我们将涵盖以下主题：

- 什么是 TensorFlow.js？
- 什么是 MongoDB？
- 如何安装 TensorFlow.js 和 MongoDB
- 如何将 TensorFlow.js 与 MongoDB 集成

## 什么是 TensorFlow.js？

TensorFlow.js 是一个用于训练和部署机器学习模型的 JavaScript 库。它由 Google 开发并在 Apache 2.0 开源许可下发布。

TensorFlow.js 可以以多种方式使用，包括：

- 在浏览器中，使用 JavaScript
- 在 Node.js 中，使用 JavaScript
- 在 React Native 应用程序中
- 在 Docker 容器中

## 什么是 MongoDB？

MongoDB 是一个强大的面向文档的数据库系统。它由 MongoDB, Inc. 开发，并根据 GNU Affero 通用公共许可证发布。

MongoDB 可以以多种方式使用，包括：

- 作为传统的数据库系统
- 作为 NoSQL 数据库
- 作为面向文档的数据库
- 作为图形数据库

## 如何安装 TensorFlow.js 和 MongoDB

在将 TensorFlow.js 与 MongoDB 集成之前，我们需要同时安装 TensorFlow.js 和 MongoDB。

### 安装 TensorFlow.js

TensorFlow.js 有两种安装方式：

- 使用脚本标签
- 使用包管理器

#### 使用脚本标签

您可以使用脚本标记将 TensorFlow.js 库包含在您的 HTML 文件中。

```html
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.3/dist/tf.min.js"></script>
```

#### 使用包管理器

如果您使用 npm 或 yarn 等包管理器，则可以使用以下命令安装 TensorFlow.js：

```
npm install @tensorflow/tfjs
```

### 安装 MongoDB

安装MongoDB有两种方式：

- 使用脚本
- 使用包管理器

#### 使用脚本

您可以使用脚本来安装 MongoDB。该脚本将为您下载并安装 MongoDB。

```
curl -O https://fastdl.mongodb.org/osx/mongodb-osx-x86_64-4.2.2.tgz
tar -zxvf mongodb-osx-x86_64-4.2.2.tgz
mkdir -p mongodb
cp -R -n mongodb-osx-x86_64-4.2.2/ mongodb
```

#### 使用包管理器

如果您使用的是像 Homebrew 这样的包管理器，则可以使用以下命令安装 MongoDB：

```
brew install mongodb
```

## 如何将 TensorFlow.js 与 MongoDB 集成

现在我们已经安装了 TensorFlow.js 和 MongoDB，我们可以开始集成它们了。

为此，我们需要执行以下操作：

- 安装 MongoDB Node.js 驱动程序
- 连接到 MongoDB 数据库
- 创建模式
- 训练模型
- 部署模型

### 安装 MongoDB Node.js 驱动

我们需要做的第一件事是安装 MongoDB Node.js 驱动程序。我们可以使用以下命令执行此操作：

```
npm install mongodb
```

### 连接到MongoDB数据库

接下来，我们需要连接到 MongoDB 数据库。我们可以使用以下代码来做到这一点：

```javascript
const MongoClient = require('mongodb').MongoClient;

const url = 'mongodb://localhost:27017';

MongoClient.connect(url, { useNewUrlParser: true }, (err, client) => {
  if (err) throw err;

  const db = client.db('test');

  console.log('Connected to MongoDB');
});
```

### 创建模式

现在我们已经连接到 MongoDB 数据库，我们需要创建一个模式。我们可以使用以下代码来做到这一点：

```javascript
const schema = new mongoose.Schema({
  name: String,
  age: Number,
  gender: String
});
```

### 训练模型

现在我们有了一个模式，我们可以训练一个模型。我们可以使用以下代码来做到这一点：

```javascript
const model = tf.sequential();

model.add(tf.layers.dense({ units: 1, inputShape: [1] }));

model.compile({ loss: 'meanSquaredError', optimizer: 'sgd' });

const xs = tf.tensor2d([1, 2, 3, 4], [4, 1]);
const ys = tf.tensor2d([1, 3, 5, 7], [4, 1]);

model.fit(xs, ys, { epochs: 10 }).then(() => {
  model.predict(tf.tensor2d([5], [1, 1])).print();
});
```

### 部署模型

最后，我们需要部署模型。我们可以使用以下代码来做到这一点：

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.use(express.static('public'));

app.get('/', (req, res) => {
  res.sendFile(__dirname + '/index.html');
});

app.listen(port, () => console.log(`Listening on port ${port}`));
```

## 结论

在本文中，我们学习了如何在 Node.js 中将 TensorFlow.js 与 MongoDB 集成。我们涵盖了以下主题：

- 什么是 TensorFlow.js？
- 什么是 MongoDB？
- 如何安装 TensorFlow.js 和 MongoDB
- 如何将 TensorFlow.js 与 MongoDB 集成

如果您有任何问题或意见，请随时在下方留言。