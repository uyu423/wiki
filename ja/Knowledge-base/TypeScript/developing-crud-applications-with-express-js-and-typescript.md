---
title: Express.js と TypeScript を使用した CRUD アプリケーションの開発
description: 
published: true
date: 2023-01-31T02:57:44.969Z
tags: 
editor: markdown
dateCreated: 2023-01-31T02:57:43.273Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Developing CRUD Applications with Express.js and TypeScript***English** version of this document is available*](/en/Knowledge-base/TypeScript/developing-crud-applications-with-express-js-and-typescript)
{.links-list}


# Express.jsとTypeScriptによるCRUDアプリケーションの開発

最も一般的なタイプのWebアプリケーションはCRUDアプリケーションです。 CRUDは、生成、読み取り、更新、削除を意味します。 CRUDアプリケーションはデータを管理するために使用されます。この記事では、Express.jsとTypeScriptを使用してCRUDアプリケーションを開発する方法について説明します。

## Express.jsとは何ですか？

Express.jsはNode.js用のWebアプリケーションフレームワークです。バックエンドの開発に使用されます。 Express.jsは、開発プロセスをはるかに簡単にする一連の機能を提供します。

##タイプスクリプトとは何ですか？

TypeScriptは、JavaScriptの上位セットであるプログラミング言語です。主に大規模なアプリケーションを開発するために使用されます。 TypeScriptは型付き言語なので、特定のデータ型で変数を宣言できます。これは、変数に異なるデータ型の値が割り当てられたときに発生する可能性のあるエラーを防ぐのに役立ちます。

## CRUDアプリケーションの開発

このセクションでは、Express.jsとTypeScriptを使用してCRUDアプリケーションを開発します。アプリケーションにMongoDBデータベースを使用します。

###プロジェクト設定

まず、プロジェクト用の新しいディレクトリを作成する必要があります。プロジェクト名を「crud-app」と指定します。

```
mkdir crud-app
```

次に、npmを使用してプロジェクトを初期化する必要があります。 "--typescript"フラグを使用してプロジェクトをTypeScriptプロジェクトに初期化します。

```
npm init --typescript
```

これにより、プロジェクトディレクトリに "package.json"ファイルが作成されます。このファイルには、プロジェクトに必要な依存関係などのプロジェクトに関する情報が含まれています。

これで、プロジェクトに依存関係をインストールする必要があります。 「express」と「mongodb」パッケージを使用します。

```
npm install express mongodb
```

TypeScriptコンパイラもインストールする必要があります。これには「typescript」パッケージを使用します。

```
npm install typescript
```

最後に、「tsconfig.json」ファイルを作成する必要があります。このファイルにはTypeScriptコンパイラの設定が含まれています。このファイルで「target」属性と「outDir」属性を設定します。 「target」属性はJavaScriptのターゲットバージョンを指定します。 "outDir"属性は、コンパイルされたJavaScriptファイルが出力されるディレクトリを指定します。

```json
{
    "compilerOptions": {
        "target": "es6",
        "outDir": "dist"
    }
}
```

### データベースの作成

まず、アプリケーション用のデータベースを作成する必要があります。データベース名を「crud_db」と指定します。

次に、データベースにコレクションを作成する必要があります。コレクションの名前を「ユーザー」として指定します。

最後に、一部のデータをコレクションに挿入する必要があります。各ユーザーに1つずつ2つの文書を挿入します。

```json
{
    "_id": ObjectId("5f3f6a8ea864fa22a0b1d9f1"),
    "name": "John Doe",
    "age": 30,
    "email": "john.doe@example.com"
}
```

```json
{
    "_id": ObjectId("5f3f6a8ea864fa22a0b1d9f2"),
    "name": "Jane Doe",
    "age": 28,
    "email": "jane.doe@example.com"
}
```

### Express.js サーバーの作成

これで、サーバー用のTypeScriptファイルを作成する必要があります。このファイルの名前は「server.ts」です。

このファイルから最初に「express」モジュールをインポートします。

```javascript
import * as express from 'express';
```

次に、「express」クラスのインスタンスを作成します。

```javascript
const app = express();
```

これでパスを設定する必要があります。 CRUD ジョブごとに 1 つずつ 2 つのパスを作成します。

「作成」パスの場合は、「POST」メソッドを使用します。

「読み取り」パスには「GET」メソッドを使用します。

「更新」パスには「PUT」メソッドを使用します。

「削除」パスの場合は、「DELETE」メソッドを使用します。

```javascript
app.post('/create', (req, res) => {
    // TODO: Implement the create route
}）;

app.get('/read/:id', (req, res) => {
    // TODO: Implement the read route
}）;

app.put('/update/:id', (req, res) => {
    // TODO: Implement the update route
}）;

app.delete('/delete/:id', (req, res) => {
    // TODO: Implement the delete route
}）;
```

最後にサーバーを起動する必要があります。 「listen」メソッドを使用してサーバーを起動します。 「ポート」プロパティを「3000」に設定します。

```javascript
app.listen(3000, () => {
    console.log('Server is listening on port 3000');
}）;
```

### CRUDタスクの実装

このセクションでは、アプリケーションのCRUD操作を実装します。

#### ユーザーの作成

「作成」パスの場合は、要求本文から新しいユーザーのデータを取得する必要があります。

次に、データを "users" コレクションに挿入します。

最後に顧客に回答を送ります。

```javascript
app.post('/create', async(req, res) => {
    const user = req.body;
    const result = await users.insertOne（user）;
    res.send(result);
}）;
```

#### ユーザーを読む

「読み取り」パスの場合は、要求から「id」パラメーターを取得する必要があります。

次に、一致する「id」を持つ文書の「users」コレクションを照会します。

最後に顧客に回答を送ります。

```javascript
app.get('/read/:id', async(req, res) => {
    const id = req.params.id;
    const result = await users.findOne({ "_id": ObjectId(id) });
    res.send(result);
}）;
```

#### ユーザー更新

「更新」パスの場合は、要求から「id」パラメーターを取得する必要があります。

次に、要求本文で更新されたユーザーのデータを取得します。

次に、一致する「id」を持つ文書の「users」コレクションを照会します。

最後に、文書を更新して顧客に返信します。

```javascript
app.put('/update/:id', async(req, res) => {
    const id = req.params.id;
    const user = req.body;
    const result = await users.findOneAndUpdate(
        { "_id": ObjectId(id) },
        { $set: user },
        { returnOriginal: false }
    ）;
    res.send(result);
}）;
```

#### ユーザーの削除

「削除」パスの場合は、要求から「id」パラメーターを取得する必要があります。

次に、一致する「id」を持つ文書の「users」コレクションを照会します。

その後、文書を削除して顧客に返信します。

```javascript
app.delete('/delete/:id', async(req, res) => {
    const id = req.params.id;
    const result = await users.findOneAndDelete({ "_id": ObjectId(id) });
    res.send(result);
}）;
```

## アプリケーションテスト

これでCRUDタスクを実装したので、アプリケーションをテストする必要があります。

TypeScriptコードをコンパイルすることから始めましょう。

```
tsc
```

これにより、「dist」ディレクトリにサーバー用のJavaScriptファイルが生成されます。

次に、サーバーを起動する必要があります。

```
node dist/server.js
```

これでCRUD操作をテストするためにサーバーに要求を送信できます。

#### ユーザーの作成

「作成」パスをテストするには、「curl」コマンドを使用します。

```
curl -X POST http://localhost:3000/create -d '{"name":"John Doe","age":30,"email":"john.doe@example.com"}' -H " Content-Type: application/json"
```

これにより、新しいユーザーのデータとともに「生成」パスに「POST」要求が送信されます。

#### ユーザーを読む

「読み取り」パスをテストするには、「curl」コマンドを使用します。

```
curl http://localhost:3000/read/5f3f6a8ea864fa22a0b1d9f1
```

これにより、「id」パラメーターは、読みたいユーザーの「id」に設定されている「読み取り」パスに「GET」要求を送信します。

#### ユーザー更新

「更新」パスをテストするには、「curl」コマンドを使用します。

```
curl -X PUT http://localhost:3000/update/5f3f6a8ea864fa22a0b1d9f1 -d '{"name":"John Doe","age":31,"email":"john.doe@example.com"}' - H "Content-Type: application/json"
```

これにより、「id」パラメータが更新したいユーザーの「id」に設定された「update」パスに「PUT」要求が送信されます。

#### ユーザーの削除

「削除」パスをテストするには、「curl」コマンドを使用します。

```
curl -X DELETE http://localhost:3000/delete/5f3f6a8ea864fa22a0b1d9f1
```

削除するユーザーの「id」に設定された「id」パラメーターを使用して、「削除」パスに「DELETE」要求を送信します。