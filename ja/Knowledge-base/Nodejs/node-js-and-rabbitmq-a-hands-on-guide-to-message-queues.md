---
title: Node.js と RabbitMQ: メッセージ キューのハンズオン ガイド
description: 
published: true
date: 2023-01-31T17:05:09.819Z
tags: 
editor: markdown
dateCreated: 2023-01-31T17:05:08.133Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Node.js and RabbitMQ: A Hands-On Guide to Message Queues***English** version of this document is available*](/en/Knowledge-base/Nodejs/node-js-and-rabbitmq-a-hands-on-guide-to-message-queues)
{.links-list}


  IT開発学習ブログに「Node.jsとRabbitMQ：メッセージキューの練習ガイド」の記事を書いてください。

Node.jsは、開発者がネットワークアプリケーションを迅速に構築できるようにするプログラミングプラットフォームです。 RabbitMQは、メッセージキューシステムを実装するのに役立つオープンソースメッセージブローカーです。

この記事では、Node.jsとRabbitMQを使用してメッセージキューシステムを設定する方法について説明します。始めるのに役立ついくつかのコード例もあります。

メッセージキューは、メッセージを非同期的に処理できるようにメッセージを保存する方法です。つまり、サービスが遅い場合や利用できない場合でも、アプリケーションを実行し続けることができます。

メッセージ待ち行列システムは、画像処理やデータ分析など、時間のかかる作業やリソース集約的なタスクの処理に使用できます。また、独立して拡張できるようにサービスを分離するためにも使用できます。

この資料では、次のトピックについて説明します。

*メッセージキューを使用する理由は何ですか？
* RabbitMQ設定
* Node.jsでメッセージを送受信する
*ワーカーとのメッセージ処理
*監視キュー

## メッセージキューを使用するのはなぜですか？

アプリケーションでメッセージキューを使用する理由はいくつかあります。

### 非同期処理

メッセージキューの主な利点の1つは、タスクを非同期的に処理できることです。つまり、サービスが遅い場合や利用できない場合でも、アプリケーションを実行し続けることができます。

たとえば、eコマースWebサイトがある場合は、ユーザーがサイトを閲覧し続けるようにバックグラウンドで注文を処理できます。または、ソーシャルメディアアプリケーションがある場合は、ユーザーがコンテンツをアップロードし続けるように画像とビデオを非同期的に処理できます。

### デカップリングサービス

メッセージキューの別の利点は、サービスを分離するために使用できることです。これは、アプリケーションの他の部分を独立して拡張できることを意味します。

たとえば、イベントチケットを販売するWebサイトがある場合は、メッセージキューを使用して注文を処理できます。これにより、Webサイトとは無関係に注文処理サービスを拡張できます。

### 安定した処理

メッセージキューは、ジョブをより確実に処理する方法も提供できます。これは、メッセージが処理されるまでキューに格納されるためです。

サービスが利用できない場合、メッセージはサービスがオンラインになるまでキューに入れられます。つまり、サービスに断続的な問題があってもアプリケーションを実行し続けることができます。

## RabbitMQの設定

RabbitMQは、メッセージキューシステムを実装するために使用できるオープンソースメッセージブローカーです。

RabbitMQには、サーバーとクライアントという2つの主要コンポーネントがあります。サーバーはキューにメッセージを保管する役割を果たします。クライアントはメッセージの送受信を担当します。

RabbitMQを設定するには、コンピュータにサーバーとクライアントをインストールする必要があります。

### サーバーのインストール

[RabbitMQ Webサイト]（https://www.rabbitmq.com/download.html）からRabbitMQサーバーをダウンロードできます。

サーバーをダウンロードしたら、インストールする必要があります。 Windowsでは、RabbitMQをサービスとしてインストールできます。 Linuxでは、apt-getなどのパッケージマネージャを使用してインストールできます。

### クライアントのインストール

[npm Package Manager]（https://www.npmjs.com/）を使用してRabbitMQクライアントをインストールできます。

RabbitMQクライアントをインストールするには、ターミナルを開き、次のコマンドを実行します。

```
npm install rabbitmq-client
```

## Node.jsでメッセージを送受信する

RabbitMQをインストールしたので、メッセージの送受信を開始できます。

このセクションでは、Node.jsを使用してメッセージを送受信する方法について説明します。

###メッセージを送信

メッセージを送信するには、RabbitMQサーバーへの接続を作成する必要があります。 `createConnection`メソッドを使ってこれを行うことができます。

接続を作成したら、チャンネルを作成する必要があります。チャンネルはメッセージの送受信に使用されます。

メッセージを送信するには、 `sendToQueue`メソッドを使用する必要があります。このメソッドは、キュー名とメッセージという2つの引数を使用します。

以下は、メッセージの送信方法の例です。

```javascript
var rabbitmq = require('rabbitmq-client');

var connection = rabbitmq.createConnection({
  host: 'localhost',
  port: 5672
}）;

connection.on('ready', function() {
  var channel = connection.createChannel();

  channel.sendToQueue（ 'my-queue'、 'Hello、world！'）;
}）;
```

この例では、RabbitMQ サーバーへの接続を作成しました。また、チャネルを作成し、 `sendToQueue`メソッドを使用して `my-queue`キューにメッセージを送信しました。

### メッセージの受信

メッセージを受信するには、 `consume`メソッドを使用する必要があります。このメソッドは、キュー名とコールバック関数の2つの引数を使用します。

コールバック関数は、受信した各メッセージに対して呼び出されます。この関数は、メッセージとコールバック関数の2つの引数を使用します。

メッセージ引数は、次の属性を含むオブジェクトです。

* `content`: メッセージ内容
* `fields`: メッセージフィールドを含むオブジェクト
* `properties`: メッセージ属性を含むオブジェクト

コールバック関数はメッセージを確認するために使用されます。これはRabbitMQにメッセージが処理され、キューから削除される可能性があることを伝えます。

以下は、メッセージの受信方法の例です。

```javascript
var rabbitmq = require('rabbitmq-client');

var connection = rabbitmq.createConnection({
  host: 'localhost',
  port: 5672
}）;

connection.on('ready', function() {
  var channel = connection.createChannel();

  channel.consume('my-queue', function(message) {
    console.log(message.content.toString());

    channel.ack（message）;
  }）;
}）;
```

この例では、RabbitMQ サーバーへの接続を作成しました。また、チャネルを作成し、 `consume`メソッドを使用して `my-queue`キューのメッセージを消費しました。

また、受信した各メッセージに対して呼び出されるコールバック関数も定義しました。この関数はメッセージをコンソールに出力し、`ack`メソッドを呼び出してメッセージをAckします。

## ワーカーによるメッセージ処理

前のセクションでは、メッセージの送受信方法について説明しました。このセクションでは、ワーカーを使用してメッセージを処理する方法について説明します。

ワーカーは、バックグラウンドで実行され、キュー内のメッセージを処理するNode.jsスクリプトです。

ワーカーを作成するには、 `fork`メソッドを使用する必要があります。このメソッドは、ワーカースクリプトのパスと引数配列の2つの引数を使用します。

ワーカースクリプトには次の引数が渡されます。

* RabbitMQサーバーへのパス
*キュー名

以下は、ワーカーの作成方法の例です。

```javascript
var rabbitmq = require('rabbitmq-client');

var connection = rabbitmq.createConnection({
  host: 'localhost',
  port: 5672
}）;

connection.on('ready', function() {
  var channel = connection.createChannel();

  channel.fork('worker.js', ['my-queue']);
}）;
```

この例では、RabbitMQ サーバーへの接続を作成しました。また、チャンネルを作成し、 `fork`メソッドを使ってワーカーを分岐しました。

ワーカーはRabbitMQサーバーと `my-queue`キューへのパスを渡されます。

ワーカースクリプト（ `worker.js`）は次のようになります。

```javascript
var rabbitmq = require('rabbitmq-client');

var connection = rabbitmq.createConnection(process.argv[0]);

connection.on('ready', function() {
  var channel = connection.createChannel();

  channel.consume(process.argv[1], function(message) {
    // process the message
  }）;
}）;
```

このスクリプトでは、RabbitMQサーバーへの接続を作成しました。また、チャネルを作成し、`consume`メソッドを使用してキューからメッセージを消費しました。

## 監視キュー

問題を特定して修正できるように、キューを監視することが重要です。

RabbitMQは、キューを監視するために使用できるWebインターフェースを提供します。 Webインタフェースにアクセスするには、 `rabbitmq-server`コマンドでRabbitMQサーバーを起動する必要があります。

サーバーが実行されると、http：//localhost：15672/からWebインターフェースにアクセスできます。

Web インターフェイスは次の情報を提供します。

*キュー内のメッセージ数
* 配信されたメッセージ数
*確認されたメッセージ数
*拒否されたメッセージの数

Web インターフェイスを使用してメッセージの内容を表示することもできます。

##結論

この記事では、Node.jsとRabbitMQを使用してメッセージキューシステムを設定する方法を説明しました。始めるのに役立ついくつかのコード例も提供しました。