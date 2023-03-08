---
title: Node.js と Redis: キャッシングとセッション管理のハンズオン ガイド
description: 
published: true
date: 2023-01-31T05:36:53.662Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:36:52.038Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Node.js and Redis: A Hands-On Guide to Caching and Session Management***English** version of this document is available*](/en/Knowledge-base/Nodejs/node-js-and-redis-a-hands-on-guide-to-caching-and-session-management)
{.links-list}


#Node.jsとRedis：キャッシュとセッション管理のための練習ガイド

この記事では、Node.jsとRedisを使用してデータをキャッシュし、セッションを管理する方法について説明します。次のトピックを扱います。

*キャッシングとは？
*レディスとは？
* Node.jsとRedisを一緒に使用するのはなぜですか？
* RedisでNode.jsからデータをキャッシュする方法
* RedisでNode.jsでセッションを管理する方法

## キャッシングとは？

キャッシュは、元のデータストアよりも高速にアクセスできる場所に頻繁にアクセスするデータを格納する技術です。データをキャッシュすると、データストアへのアクセスにかかる時間が短縮され、アプリケーションのパフォーマンスが向上します。

キャッシュには、クライアント側キャッシュとサーバー側キャッシュの2種類があります。クライアント側キャッシュは、ブラウザキャッシュなどのクライアントシステムにデータを格納します。サーバー側のキャッシュはサーバーにデータを格納します。

この記事では、Redisを使用したサーバー側のキャッシュに焦点を当てます。

##レディスとは？

Redisは、データベース、キャッシュ、またはメッセージブローカーとして使用できるオープンソースのメモリ内データストアです。 RedisはCで書かれており、Node.jsを含むいくつかのプログラミング言語をサポートしています。

RedisはKey-Valueストアです。つまり、キーと値のペアの形でデータを保存します。キーを使用して値を取得できます。 Redisは、文字列、リスト、セット、ハッシュなど、さまざまなデータ型をサポートしています。

## Node.jsとRedisを一緒に使用するのはなぜですか？

Node.jsは、スケーラブルなサーバーサイドアプリケーションを構築するために使用されるJavaScriptランタイム環境です。 Node.jsは高速で効率的で、データ集約型アプリケーションの構築に適しています。

Redisは、Node.jsアプリケーションで使用するのに適した高速で柔軟で強力なデータストアです。 Redis はデータベース、キャッシュ、メッセージブローカーとして使用でき、Node.js を含む複数のプログラミング言語をサポートしています。

Node.jsとRedisは高速で効率的で、データ集約型のアプリケーションを構築するのに適しています。

## RedisでNode.jsでデータをキャッシュする方法

このセクションでは、Redisを使用してNode.jsでデータをキャッシュする方法について説明します。次のトピックを扱います。

* Node.jsプロジェクトの設定
* Redisサーバーに接続
*キャッシュクライアントの作成
*キャッシュにデータを追加
*キャッシュからデータをインポートする
*キャッシュからデータを削除

### Node.jsプロジェクトの設定

まず、Node.jsプロジェクトを設定する必要があります。プロジェクトの新しいディレクトリを作成し、プロジェクトディレクトリに `app.js`というファイルを作成します。

`app.js`ファイルにはRedisモジュールが必要です。 Redisサーバーへの接続も確立します。

```javascript
var redis = require("redis");
var client = redis.createClient();
```

### Redisサーバーに接続

次に、Redisサーバーに接続する必要があります。 Redisモジュールの `createClient`メソッドを呼び出してこれを行います。

```javascript
var redis = require("redis");
var client = redis.createClient();
```

`createClient`メソッドは`host`と`port`の2つの引数を受け入れます。 `host`引数はRedisサーバーのホスト名またはIPアドレス、`port`引数はRedisサーバーのポート番号です。

ローカルマシンでRedisを実行している場合は、`host`と`port`にデフォルト値を使用できます。

```javascript
var redis = require("redis");
var client = redis.createClient();
```

### キャッシュクライアントの作成

これでRedisサーバーに接続したので、キャッシュクライアントを作成できます。 Redisモジュールの `createClient`メソッドを呼び出してこれを行います。

```javascript
var redis = require("redis");
var client = redis.createClient();

var cache = redis.createClient();
```

`createClient`メソッドは`host`と`port`の2つの引数を受け入れます。 `host`引数はRedisサーバーのホスト名またはIPアドレス、`port`引数はRedisサーバーのポート番号です。

ローカルマシンでRedisを実行している場合は、`host`と`port`にデフォルト値を使用できます。

```javascript
var redis = require("redis");
var client = redis.createClient();

var cache = redis.createClient();
```

### キャッシュにデータを追加

キャッシュクライアントがある場合は、キャッシュにデータを追加できます。キャッシュクライアントの `set` メソッドを呼び出してこれを行います。

`set`メソッドは`key`、`value`、および`callback`の3つの引数を受け入れます。 'key'引数はキャッシュエントリのキー、'value'引数はキャッシュエントリの値、'callback'引数はデータがキャッシュに追加されたときに呼び出される関数です。

```javascript
var redis = require("redis");
var client = redis.createClient();

var cache = redis.createClient();

cache.set("key", "value", function(err, data) {
  if(err){
    console.log（err）;
  }else{
    console.log（data）;
  }
}）;
```

上記の例では、キャッシュにキーと値のペアを追加しました。キーは「キー」、値は「値」です。

### キャッシュからデータを取得

キャッシュにデータを追加したので、キャッシュクライアントの `get`メソッドを呼び出してデータを取得できます。

`get`メソッドは`key`と`callback`の2つの引数を受け入れます。 `key`引数はキャッシュエントリのキーであり、`callback`引数はデータがキャッシュから取得されたときに呼び出される関数です。

```javascript
var redis = require("redis");
var client = redis.createClient();

var cache = redis.createClient();

cache.get("key", function(err, data) {
  if(err){
    console.log（err）;
  }else{
    console.log（data）;
  }
}）;
```

上記の例では、キャッシュから 'key'キーのデータを取得しました。

### キャッシュからデータを削除する

キャッシュクライアントの `del` メソッドを呼び出して、キャッシュからデータを削除できます。

`del`メソッドは`key`と`callback`の2つの引数を受け入れます。 `key`引数はキャッシュエントリのキーで、`callback`引数はデータがキャッシュから削除されたときに呼び出される関数です。

```javascript
var redis = require("redis");
var client = redis.createClient();

var cache = redis.createClient();

cache.del("key", function(err, data) {
  if(err){
    console.log（err）;
  }else{
    console.log（data）;
  }
}）;
```

上記の例では、キャッシュから 'key'キーのデータを削除しました。

## RedisでNode.jsでセッションを管理する方法

このセクションでは、Redisを使用してNode.jsでセッションを管理する方法について説明します。次のトピックを扱います。

* Node.jsプロジェクトの設定
* Redisサーバーに接続
*セッションストアの作成
* セッションストアにデータを追加
*セッションストアからデータを取得する
* セッションストアからデータを削除する

### Node.jsプロジェクトの設定

まず、Node.jsプロジェクトを設定する必要があります。プロジェクトの新しいディレクトリを作成し、プロジェクトディレクトリに `app.js`というファイルを作成します。

`app.js`ファイルにはRedisモジュールが必要です。 Redisサーバーへの接続も確立します。

```javascript
var redis = require("redis");
var client = redis.createClient();
```

### Redisサーバーに接続

次に、Redisサーバーに接続する必要があります。 Redisモジュールの `createClient`メソッドを呼び出してこれを行います。

`createClient`メソッドは`host`と`port`の2つの引数を受け入れます。 `host`引数はRedisサーバーのホスト名またはIPアドレス、`port`引数はRedisサーバーのポート番号です。

ローカルマシンでRedisを実行している場合は、`host`と`port`にデフォルト値を使用できます。

```javascript
var redis = require("redis");
var client = redis.createClient();
```

### セッションストアの作成

これでRedisサーバーに接続したので、セッションストアを作成できます。 Redisモジュールの `createClient`メソッドを呼び出してこれを行います。

`createClient`メソッドは`host`と`port`の2つの引数を受け入れます。 `host`引数はRedisサーバーのホスト名またはIPアドレス、`port`引数はRedisサーバーのポート番号です。

ローカルマシンでRedisを実行している場合は、`host`と`port`にデフォルト値を使用できます。

```javascript
var redis = require("redis");
var client = redis.createClient();

var session = redis.createClient();
```

### セッションストアにデータを追加する

これでセッションリポジトリがあるので、リポジトリにデータを追加できます。セッションストアの `set` メソッドを呼び出してこれを行います。

`set`メソッドは`key`、`value`、および`callback`の3つの引数を受け入れます。 `key`引数はセッション項目のキーであり、`value`引数はセッション項目の値であり、`callback`引数はデータがセッションストアに追加されたときに呼び出される関数です。

```javascript
var redis = require("redis");
var client = redis.createClient();

var session = redis.createClient();

session.set("key", "value", function(err, data) {
  if(err){
    console.log（err）;
  }else{
    console.log（data）;
  }
}）;
```

上記の例では、セッションストアにキーと値のペアを追加しました。キーは「キー」、値は「値」です。

### セッションストアからデータを取得する

これでセッションストアにデータを追加したので、セッションストアの `get`メソッドを呼び出してデータを取得できます。

`get`メソッドは`key`と`callback`の2つの引数を受け入れます。 `key`引数はセッションエントリのキーで、 `callback`引数はセッションストアからデータを取得するときに呼び出される関数です。

```javascript
var redis = require("redis");
var client = redis.createClient();

var session = redis.createClient();

session.get("key", function(err, data) {
  if(err){
    console.log（err）;
  }else{
    console.log（data）;
  }
}）;
```

上記の例では、セッションストアから 'key'キーのデータを取得しました。

### セッションストアからデータを削除する

セッションストアの `del` メソッドを呼び出して、セッションストアからデータを削除できます。

`del`メソッドは`key`と`callback`の2つの引数を受け入れます。 `key`引数はセッションエントリのキーであり、 `callback`引数はセッションストアからデータが削除されたときに呼び出される関数です。

```javascript
var redis = require("redis");
var client = redis.createClient();

var session = redis.createClient();

session.del("key", function(err, data) {
  if(err){
    console.log（err）;
  }else{
    console.log（data）;
  }
}）;
```

上記の例では、セッションストアから 'key'キーのデータを削除しました。

##結論

この記事では、Node.jsとRedisを使用してデータをキャッシュし、セッションを管理する方法について説明しました。 Node.jsプロジェクトを設定し、Redisサーバーに接続し、キャッシュクライアントとセッションストアを作成する方法を見てきました。また、キャッシュとセッションストアにデータを追加し、キャッシュとセッションストアからデータを取得し、キャッシュとセッションストアからデータを削除する方法も検討しました。