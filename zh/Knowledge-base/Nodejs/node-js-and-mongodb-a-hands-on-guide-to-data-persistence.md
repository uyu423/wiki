---
title: Node.js 和 MongoDB：数据持久化实践指南
description: 
published: true
date: 2023-01-31T06:43:49.316Z
tags: 
editor: markdown
dateCreated: 2023-01-31T06:43:45.849Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Node.js and MongoDB: A Hands-On Guide to Data Persistence***English** version of this document is available*](/en/Knowledge-base/Nodejs/node-js-and-mongodb-a-hands-on-guide-to-data-persistence)
{.links-list}



# Node.js 和 MongoDB：数据持久化实践指南

在本文中，我们将探讨如何使用 Node.js 和 MongoDB 来持久化数据。我们将介绍设置 MongoDB 数据库、创建 Node.js 应用程序以与数据库交互以及使用 CRUD 操作来操作数据的基础知识。到本文结束时，您将深入了解如何使用 Node.js 和 MongoDB 创建可扩展的数据驱动应用程序。

## 设置 MongoDB

MongoDB 是一个强大的面向文档的数据库系统。它具有丰富的查询语言和索引功能，可以轻松处理任何大小和复杂性的数据。

要开始使用 MongoDB，您首先需要[安装 MongoDB 社区服务器](https://www.mongodb.com/download-center/community)。 MongoDB 适用于 Windows、macOS 和 Linux。

安装 MongoDB 后，您可以使用 `mongod` 命令启动 MongoDB 守护进程。这将启动 MongoDB 服务器并创建一个“数据”目录来存储数据库文件。

接下来，您需要为 MongoDB 服务器创建一个配置文件。此文件通常名为“mongod.conf”，位于安装 MongoDB 的“bin”目录中。以下是可用于入门的基本配置文件：

```
storage:
  dbPath: /data/db
  journal:
    enabled: true
```

该文件告诉 MongoDB 在哪里存储数据库文件（在本例中为 `/data/db` 目录）并启用日志功能，这是为数据库提供崩溃恢复的功能。

现在 MongoDB 服务器已启动并正在运行，您可以使用 `mongo` shell 连接到它。这将为您提供一个用于与数据库交互的 JavaScript 接口。

## 创建一个 Node.js 应用程序

现在我们已经启动并运行了 MongoDB，让我们创建一个可以与数据库交互的 Node.js 应用程序。我们将从为我们的项目创建一个基本的目录结构开始：

```
node-mongo
├── config
│   └── mongodb.js
├── controllers
│   └── books.js
├── models
│   └── book.js
├── routes
│   └── books.js
└── app.js
```

我们将配置文件放在 `config` 目录中，我们的控制器文件放在 `controllers` 目录中，我们的模型文件放在 `models` 目录中，我们的路由文件放在 `routes` 目录中。

`app.js` 文件将是我们应用程序的入口点。这是我们配置应用程序和设置中间件的地方。

首先，让我们创建 `config/mongodb.js` 文件。该文件将包含我们的 MongoDB 配置：

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/node-mongo', {
  useNewUrlParser: true,
  useUnifiedTopology: true
});

const db = mongoose.connection;

db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {
  console.log('Connected to MongoDB');
});

module.exports = db;
```

在这个文件中，我们使用 `mongoose` 库连接到我们的 MongoDB 数据库。我们还设置了一个 db 变量来引用我们的数据库连接。此 `db` 变量将可用于需要此模块的任何文件。

接下来，让我们创建 `models/book.js` 文件。该文件将包含我们的书籍模型：

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const bookSchema = new Schema({
  title: String,
  author: String,
  year: Number,
  genre: String
});

const Book = mongoose.model('Book', bookSchema);

module.exports = Book;
```

该模型定义了我们数据库中书籍文档的结构。我们正在使用 `mongoose.model()` 方法从我们的模式创建模型。该模型将用于在我们的数据库中创建文档。

现在我们已经定义了模型，让我们创建我们的控制器。控制器将包含我们的 CRUD 操作的逻辑。我们将从创建“controllers/books.js”文件开始：

```javascript
const Book = require('../models/book');

exports.getBooks = (req, res, next) => {
  Book.find((err, books) => {
    if (err) return next(err);
    res.json(books);
  });
};

exports.getBook = (req, res, next) => {
  Book.findById(req.params.id, (err, book) => {
    if (err) return next(err);
    res.json(book);
  });
};

exports.createBook = (req, res, next) => {
  const book = new Book(req.body);
  book.save((err, book) => {
    if (err) return next(err);
    res.json(book);
  });
};

exports.updateBook = (req, res, next) => {
  Book.findByIdAndUpdate(req.params.id, req.body, (err, book) => {
    if (err) return next(err);
    res.json(book);
  });
};

exports.deleteBook = (req, res, next) => {
  Book.findByIdAndRemove(req.params.id, req.body, (err, book) => {
    if (err) return next(err);
    res.json(book);
  });
};
```

这个控制器定义了我们的 CRUD 操作的逻辑。我们有一个 getBooks 方法可以从我们的数据库中获取所有书籍，一个 getBook 方法可以通过 ID 获取一本书，一个 createBook 方法可以创建一本新书，一个 updateBook 方法可以更新现有的书，和一个 deleteBook 方法来删除一本书。

现在我们已经定义了我们的控制器，让我们创建我们的路由。我们将从创建 `routes/books.js` 文件开始：

```javascript
const express = require('express');
const router = express.Router();
const booksCtrl = require('../controllers/books');

router.get('/books', booksCtrl.getBooks);
router.get('/books/:id', booksCtrl.getBook);
router.post('/books', booksCtrl.createBook);
router.put('/books/:id', booksCtrl.updateBook);
router.delete('/books/:id', booksCtrl.deleteBook);

module.exports = router;
```

在这个文件中，我们使用 `express.Router` 类为我们的图书 API 创建一个路由器。然后我们为我们的 CRUD 操作定义路由并将它们映射到适当的控制器方法。

最后，我们将定义我们的 app.js 文件。这是我们应用程序的入口点：

```javascript
const express = require('express');
const app = express();
const booksRouter = require('./routes/books');
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/node-mongo');

app.use(express.json());
app.use('/api/v1/books', booksRouter);

app.listen(3000, () => {
  console.log('Server listening on port 3000');
});
```

在这个文件中，我们需要我们的应用程序所需的依赖项。然后我们使用 `express.json()` 中间件来解析 JSON 请求。

接下来，我们使用 `express.Router` 类为我们的图书 API 创建一个路由器。然后我们将 `booksRouter` 映射到 `/api/v1/books` 路径。

最后，我们告诉我们的应用程序监听端口 3000。

## 增删改查操作

现在我们已经设置了应用程序，让我们看看如何执行 CRUD 操作。

### 创建一本书

要创建一本书，我们将向 `/api/v1/books` 端点发送一个 POST 请求，其中包含一个包含书籍数据的 JSON 正文：

```javascript
{
	"title": "The Great Gatsby",
	"author": "F. Scott Fitzgerald",
	"year": 1925,
	"genre": "Novel"
}
```

### 检索一本书

要检索一本书，我们将向 `/api/v1/books/:id` 端点发送一个 GET 请求，其中 `:id` 是我们要检索的书的 ID：

```
/api/v1/books/5d908983b3259d1b68e53b4d
```

### 更新一本书

要更新图书，我们将向 `/api/v1/books/:id` 端点发送一个 PUT 请求，其中包含一个包含更新图书数据的 JSON 正文。只有需要更新的字段需要包含在请求正文中：

```javascript
{
	"title": "The Great Gatsby",
	"author": "F. Scott Fitzgerald",
	"year": 1926,
	"genre": "Novel"
}
```

### 删除一本书

要删除一本书，我们将向 `/api/v1/books/:id` 端点发送一个 DELETE 请求，其中 `:id` 是我们要删除的书的 ID：

```
/api/v1/books/5d908983b3259d1b68e53b4d
```

## 结论

在本文中，我们了解了如何使用 Node.js 和 MongoDB 创建可扩展的数据驱动应用程序。我们已经介绍了设置 MongoDB、创建 Node.js 应用程序以与数据库交互以及使用 CRUD 操作来操作数据的基础知识。