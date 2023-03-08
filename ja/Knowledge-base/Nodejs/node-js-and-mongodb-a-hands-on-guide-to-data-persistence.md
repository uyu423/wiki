---
title: Node.js と MongoDB: データ永続化のハンズオン ガイド
description: 
published: true
date: 2023-01-31T06:43:49.316Z
tags: 
editor: markdown
dateCreated: 2023-01-31T06:43:45.847Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Node.js and MongoDB: A Hands-On Guide to Data Persistence***English** version of this document is available*](/en/Knowledge-base/Nodejs/node-js-and-mongodb-a-hands-on-guide-to-data-persistence)
{.links-list}



#Node.jsとMongoDB：データ永続性に関する実践ガイド

この記事では、Node.jsとMongoDBを使用してデータを保持する方法について説明します。 MongoDBデータベースの設定、データベースと対話するNode.jsアプリケーションの作成、CRUD操作を使用したデータ操作の基本について説明します。この記事を終えて、Node.jsとMongoDBを使用してスケーラブルなデータ駆動型アプリケーションを作成する方法を確実に理解できます。

## モンゴルDB設定

MongoDBは強力な文書指向データベースシステムです。あらゆるサイズと複雑さのデータで簡単に作業できる豊富なクエリ言語とインデックス機能があります。

MongoDBを起動するには、まず「MongoDB Community Serverのインストール」（https://www.mongodb.com/download-center/community）が必要です。 MongoDBはWindows、macOS、Linuxで利用できます。

MongoDBがインストールされたら、 `mongod`コマンドでMongoDBデーモンを起動できます。これによりMongoDBサーバーが起動し、データベースファイルを保存するための `data`ディレクトリが作成されます。

次に、MongoDBサーバー用の構成ファイルを作成する必要があります。このファイルには通常、`mongod.conf`という名前があり、MongoDBがインストールされている `bin`ディレクトリにあります。以下は、起動に使用できるデフォルトの構成ファイルです。

```
storage:
  dbPath: /data/db
  journal:
    enabled: true
```

このファイルは、MongoDBにデータベースファイル（この場合は ` / data / db`ディレクトリ）を保存する場所を知らせ、データベースの競合回復を提供する機能であるジャーナリングを有効にします。

MongoDBサーバーが稼働しているため、 `mongo`シェルを使用して接続できます。これにより、データベースと対話するためのJavaScriptインターフェースが提供されます。

## Node.jsアプリケーションの作成

MongoDBを実行しているので、データベースと対話できるNode.jsアプリケーションを作成しましょう。プロジェクトの基本ディレクトリ構造を作成することから始めましょう。

```
node-mongo
├── config
│ └── mongodb.js
├── controllers
│ └── books.js
├── models
│ └── book.js
├── routes
│ └── books.js
└── app.js
```

設定ファイルは `config` ディレクトリに、コントローラファイルは `controllers` ディレクトリに、モデルファイルは `models` ディレクトリに、パスファイルは `routes` ディレクトリに置きます。

`app.js`ファイルはアプリケーションのエントリポイントになります。ここでアプリケーションを設定し、ミドルウェアを設定します。

まず `config/mongodb.js` ファイルを生成します。このファイルには MongoDB 構成が含まれます。

```javascript
const mongoose = require（ 'mongoose'）;

mongoose.connect('mongodb://localhost/node-mongo', {
  useNewUrlParser: true,
  useUnifiedTopology: true
}）;

const db = mongoose.connection;

db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {
  console.log（ 'Connected to MongoDB'）;
}）;

module.exports = db;
```

このファイルは `mongoose` ライブラリを使って MongoDB データベースに接続します。また、データベース接続を参照するために `db`変数を設定しています。この `db` 変数は、このモジュールが必要なすべてのファイルで使用できます。

次に、 `models/book.js` ファイルを生成しましょう。このファイルには書籍モデルが含まれます。

```javascript
const mongoose = require（ 'mongoose'）;
const Schema = mongoose.Schema;

const bookSchema = new Schema（{
  title: String,
  author: String,
  year: Number,
  genre: String
}）;

const Book = mongoose.model（ 'Book'、bookSchema）;

module.exports = Book;
```

このモデルは、データベース内の書籍文書の構造を定義します。スキーマからモデルを生成するために `mongoose.model()` メソッドを使用しています。このモデルは、データベースから文書を作成するために使用されます。

これでモデルを定義したので、コントローラを作成してみましょう。コントローラにはCRUD操作のロジックが含まれます。 `controllers/books.js` ファイルを生成することから始めましょう。

```javascript
const Book = require('../models/book');

exports.getBooks = (req, res, next) => {
  Book.find((err, books) => {
    if（err）return next（err）;
    res.json（books）;
  }）;
};

exports.getBook = (req, res, next) => {
  Book.findById(req.params.id, (err, book) => {
    if（err）return next（err）;
    res.json（book）;
  }）;
};

exports.createBook = (req, res, next) => {
  const book = new Book（req.body）;
  book.save((err, book) => {
    if（err）return next（err）;
    res.json（book）;
  }）;
};

exports.updateBook = (req, res, next) => {
  Book.findByIdAndUpdate(req.params.id, req.body, (err, book) => {
    if（err）return next（err）;
    res.json（book）;
  }）;
};

exports.deleteBook = (req, res, next) => {
  Book.findByIdAndRemove(req.params.id, req.body, (err, book) => {
    if（err）return next（err）;
    res.json（book）;
  }）;
};
```

このコントローラはCRUD操作のロジックを定義します。データベースからすべての書籍を取得する `getBooks` メソッド、ID で単一の書籍を取得する `getBook` メソッド、新しい書籍を作成する `createBook` メソッド、既存の書籍を更新する `updateBook` メソッド、書籍を削除する `deleteBook`メソッド。

ここでコントローラを定義したので、パスを作成しましょう。 `routes/books.js`ファイルを生成することから始めましょう：

```javascript
const express = require('express');
const router = express.Router（）;
const booksCtrl = require('../controllers/books');

router.get('/books', booksCtrl.getBooks);
router.get('/books/:id', booksCtrl.getBook);
router.post('/books', booksCtrl.createBook);
router.put('/books/:id', booksCtrl.updateBook);
router.delete('/books/:id', booksCtrl.deleteBook);

module.exports = router;
```

このファイルでは、`express.Router`クラスを使って本API用のルータを作成します。次に、CRUD操作へのパスを定義し、それを適切なコントローラメソッドにマッピングします。

最後に `app.js` ファイルを定義します。これは私たちのアプリケーションのエントリポイントです。

```javascript
const express = require('express');
const app = express();
const booksRouter = require('./routes/books');
const mongoose = require（ 'mongoose'）;

mongoose.connect('mongodb://localhost/node-mongo');

app.use(express.json());
app.use（ '/api/v1/books'、booksRouter）;

app.listen(3000, () => {
  console.log（ 'Server listening on port 3000'）;
}）;
```

このファイルでは、アプリケーションに必要な依存関係が必要です。次に、 `express.json()` ミドルウェアを使って JSON リクエストを解析します。

次に、`express.Router`クラスを使って本API用のルーターを作成します。次に、 `booksRouter` を `/api/v1/books` パスにマップします。

最後に、アプリケーションがポート3000でリッスンするようにします。

## CRUD操作

ここでアプリケーションを設定したので、CRUD操作を実行する方法を見てみましょう。

### 本の作成

書籍を作成するには、書籍データを含むJSON本体と一緒に `/api/v1/books` エンドポイントにPOSTリクエストを送信します。

```javascript
{
"title": "The Great Gatsby",
"author": "F. Scott Fitzgerald",
"year": 1925,
"genre": "Novel"
}
```

###書籍検索

本を検索するには、 `/api/v1/books/:id` エンドポイントに GET リクエストを送信します。ここで `:id` は検索したい本の ID です。

```
/api/v1/books/5d908983b3259d1b68e53b4d
```

### 本の更新

書籍を更新するには、更新された書籍データを含むJSON本体と一緒にPUTリクエストを `/api/v1/books/:id` エンドポイントに送信します。更新が必要なフィールドのみを要求本文に含めるだけです。

```javascript
{
"title": "The Great Gatsby",
"author": "F. Scott Fitzgerald",
"year": 1926,
"genre": "Novel"
}
```

### 本の削除

書籍を削除するには、 `/api/v1/books/:id` エンドポイントに DELETE リクエストを送信します。ここで `:id` は削除する書籍の ID です。

```
/api/v1/books/5d908983b3259d1b68e53b4d
```

##結論

この記事では、Node.jsとMongoDBを使用してスケーラブルなデータ駆動型アプリケーションを作成する方法について説明しました。 MongoDBの設定、データベースと対話するNode.jsアプリケーションの作成、CRUD操作を使用したデータ操作の基本について説明します。