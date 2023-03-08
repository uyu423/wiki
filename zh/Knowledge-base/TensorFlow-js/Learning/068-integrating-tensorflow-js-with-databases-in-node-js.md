---
title: 068：在 Node.js 中将 TensorFlow.js 与数据库集成
description: 
published: true
date: 2023-02-02T22:43:43.548Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:43:38.871Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [068: Integrating TensorFlow.js with Databases in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/068-integrating-tensorflow-js-with-databases-in-node-js)
{.links-list}


# 068：将 TensorFlow.js 与 Node.js 中的数据库集成

TensorFlow.js 是一个强大的 JavaScript 机器学习工具。在本文中，我们将向您展示如何在 Node.js 中使用 TensorFlow.js 和数据库。

## 设置你的环境

在我们开始之前，我们需要设置我们的环境。我们需要安装 Node.js 和 TensorFlow.js Node.js API。

您可以从 [Node.js 网站](https://nodejs.org/en/) 安装 Node.js。

安装 Node.js 后，您可以使用以下命令安装 TensorFlow.js Node.js API：

```
npm install @tensorflow/tfjs-node
```

## 连接到数据库

现在我们已经设置了环境，我们可以开始使用数据库了。

我们将使用 [sqlite3](https://www.npmjs.com/package/sqlite3) Node.js 模块连接到 SQLite 数据库。 SQLite 是一个轻型数据库，不需要单独的服务器。

首先，我们需要安装 sqlite3 模块：

```
npm install sqlite3
```

接下来，我们将创建一个名为“database.js”的文件，其中包含以下内容：

```javascript
const sqlite3 = require('sqlite3').verbose();

const db = new sqlite3.Database('./database.sqlite3');

db.serialize(() => {
  // create a table
  db.run('CREATE TABLE IF NOT EXISTS items (name, value)');

  // insert some data
  const stmt = db.prepare('INSERT INTO items VALUES (?, ?)');
  for (let i = 0; i < 10; i++) {
    stmt.run(`Item ${i}`, i);
  }
  stmt.finalize();

  // query the data
  db.each('SELECT * FROM items', (err, row) => {
    console.log(row.name + ': ' + row.value);
  });
});

db.close();
```

在这个文件中，我们连接到一个名为“database.sqlite3”的 SQLite 数据库。然后我们创建一个名为“items”的表并向其中插入一些数据。

最后，我们从数据库中查询数据并将其打印到控制台。

要运行此文件，您可以使用以下命令：

```
node database.js
```

## 将 TensorFlow.js 与数据库一起使用

现在我们已经了解了如何连接到数据库，让我们来看看如何将 TensorFlow.js 与数据库一起使用。

我们将使用上一节中相同的 `database.js` 文件。我们只需添加几行代码即可将数据从数据库加载到 TensorFlow.js `tf.data.Dataset` 中。

```javascript
const sqlite3 = require('sqlite3').verbose();
const tf = require('@tensorflow/tfjs-node');

const db = new sqlite3.Database('./database.sqlite3');

db.serialize(() => {
  // create a table
  db.run('CREATE TABLE IF NOT EXISTS items (name, value)');

  // insert some data
  const stmt = db.prepare('INSERT INTO items VALUES (?, ?)');
  for (let i = 0; i < 10; i++) {
    stmt.run(`Item ${i}`, i);
  }
  stmt.finalize();

  // query the data
  const dataset = tf.data.Dataset.fromSqlQuery('SELECT * FROM items', db, (err, row) => {
    return {
      name: row.name,
      value: row.value
    };
  });

  // print the data
  dataset.forEachAsync(item => {
    console.log(item.name + ': ' + item.value);
  });
});

db.close();
```

在此文件中，我们使用“tf.data.Dataset.fromSqlQuery()”函数将数据从数据库加载到“tf.data.Dataset”中。然后我们将数据打印到控制台。

要运行此文件，您可以使用以下命令：

```
node database.js
```

## 概括

在本文中，我们了解了如何将 TensorFlow.js 与 Node.js 中的数据库结合使用。我们已经了解了如何连接到数据库以及如何使用 TensorFlow.js 从数据库加载数据。