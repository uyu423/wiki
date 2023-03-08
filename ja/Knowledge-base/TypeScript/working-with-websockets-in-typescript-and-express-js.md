---
title: TypeScript と Express.js での WebSocket の操作
description: 
published: true
date: 2023-02-17T18:12:04.549Z
tags: 
editor: markdown
dateCreated: 2023-01-30T18:57:49.580Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Working with WebSockets in TypeScript and Express.js***English** version of this document is available*](/en/Knowledge-base/TypeScript/working-with-websockets-in-typescript-and-express-js)
{.links-list}





WebSocketは、クライアントとサーバー間の通信に非常に広く使用されています。単一のTCP接続を介して双方向全二重通信チャネルを提供し、すべての主要なブラウザで非常によくサポートされています。

この記事では、TypeScriptとExpress.jsでWebSocketを使用する方法について説明します。また、Webアプリケーションでこれを使用する方法のいくつかの実用的な例を提供します。

## WebSocketとは何ですか？

WebSocketは、Webブラウザとサーバー間の双方向リアルタイム通信を可能にする比較的新しい技術です。既存のHTTP要求 - 応答モデルの代替であり、はるかに効率的な通信チャネルを提供します。

 WebSocketはTCPプロトコルに基づいており、全二重通信チャネルを使用します。これは、クライアントとサーバーが同時にデータを送受信できることを意味します。

WebSocketはすべての主要なブラウザでサポートされており、WebアプリケーションでWebSocketを簡単に使用できるように、よくサポートされている複数のライブラリとフレームワークがあります。

## WebSocketを使用する理由は何ですか？

WebSocket は、既存の HTTP 要求 - 応答モデルと比較して多くの利点を提供します。

通信期間中に開いている単一のTCP接続のみが必要なため、はるかに効率的です。これは、HTTP の場合など、各要求に対して新しい接続を確立する必要がないことを意味します。

また、次の要求を送信する前に要求が完了するのを待つ必要がないため、待ち時間ははるかに短くなります。これは、チャットアプリケーション、オンラインゲームなど、リアルタイム通信が必要なアプリケーションにとって特に重要です。

## WebSocketはどのように機能しますか？

WebSocket は、HTTP プロトコルの拡張である ws:// というプロトコルを使用します。クライアントがサーバーへのWebSocket接続を確立したい場合は、このプロトコルを使用して要求を送信します。

その後、サーバーはWebSocketプロトコルステータスコードのHTTP 101スイッチで応答し、接続はWebSocket接続にアップグレードされます。

接続が確立されると、クライアントとサーバーはいつでもデータを送受信できます。

## TypeScriptでWebSocketを使用する

wsやsocket.ioなど、TypeScriptでWebSocketサポートを提供するために使用できるいくつかのライブラリがあります。この記事では socket.io ライブラリを使用します。

Socket.io は、TypeScript アプリケーションで WebSocket を簡単に使用できるようにする、一般的でよくサポートされているライブラリです。 WebSocketプロトコルの詳細を抽象化し、データの送受信に使用できる単純なAPIを提供します。

Socket.ioには、投稿/購読メッセージング、会議室などの他の多くの機能もあります。

## Socket.ioのインストール

npm パッケージマネージャを使用して Socket.io をインストールできます。

```
npm install socket.io
```

## Socket.io サーバーの作成

Socket.io アプリケーションは、ブラウザで実行されるクライアント側ライブラリと Node.js プラットフォームで実行されるサーバー側ライブラリの 2 つの部分で構成されます。

このセクションでは、接続されているすべてのクライアントに「hello world」メッセージをブロードキャストする単純なSocket.ioサーバーを作成します。

まず socket.io ライブラリをインポートする必要があります。

```typescript
import * as io from "socket.io";
```

次に、Express.jsフレームワークを使用してHTTPサーバーを作成します。

```typescript
const app = express();
const server = http.createServer（app）;
```

その後、Socket.ioライブラリをHTTPサーバーにバインドできます。

```typescript
const io = socketIO（server）;
```

Socket.ioサーバーが稼働しているため、着信接続を処理するコードを書く必要があります。 ```connection '' event：

「タイプスクリプト」
io.on("接続", (ソケット) => {
  //
}）;
```

The ``connection '' event is emitted when a client connects to the server. The ```socket ```'オブジェクトは、コールバック機能を返すためにクライアント接続を返します。

We can now write some code to send a message to the client:

「タイプスクリプト」
io.on("接続", (ソケット) => {
  socket.emit（「こんにちは」、「こんにちは！」）;
}）;
```

The ``emit```method is used to send a message to the client. The first argument is the name of the event, and the second argument is the data to be sent.

## Creating a Socket.io client

Now that we have a Socket.io server up and running, let's create a client that will connect to it and print out the "hello world" message.

First, we need to include the Socket.io client library in our HTML page:

```html
<スクリプトsrc="/socket.io/socket.io.js"></スクリプト>
```

Next、we'll create a new ```Socket '' instance、そして接続するためにあなたのサーバー：

「JavaScript
const ソケット = io("http://localhost:8080");
```

We can then listen for the ``hello```` event that we defined on the server:

「JavaScript
socket.on("hello", (データ) => {
  console.log（データ）; //「こんにちは！」
}）;
```

## Sending and receiving data

In the previous section, we saw how to send data from the server to the client. In this section, we'll see how to do the reverse: send data from the client to the server.

私はそれを使うために「send」というメソッドを使っています：

「JavaScript
socket.send（「こんにちは」、「こんにちは！」）;
```

On the server、we can listen for the ```message '' event：

「タイプスクリプト」
socket.on("メッセージ", (データ) => {
  console.log（データ）; //「こんにちは！」
}）;
```

##結論

この記事では、TypeScriptとExpress.jsでWebSocketを使用する方法について説明しました。また、Socket.ioサーバーとクライアントを作成する方法と、それらの間でデータを送受信する方法も見てきました。