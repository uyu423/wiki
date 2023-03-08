---
title: WebSocket を使用してリアルタイム アプリケーションを構築する方法
description: 
published: true
date: 2023-02-17T18:03:16.212Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:54:19.544Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [How to Build a Real-Time Application with WebSockets***English** version of this document is available*](/en/Knowledge-base/Common/how-to-build-a-real-time-application-with-websockets)
{.links-list}


#WebSocketでリアルタイムアプリケーションを構築する方法

この記事では、WebSocketを使用してリアルタイムアプリケーションを構築する方法について説明します。 WebSocketの基本とWebSocketを使用して簡単なチャットアプリケーションを作成する方法を見てみましょう。

WebSocket は、クライアントとサーバー間の全二重通信を可能にするプロトコルです。これは、クライアントとサーバーが同時にデータを送受信できることを意味します。 WebSocketは、チャットアプリケーション、マルチプレイヤーゲーム、コラボレーションツールなど、リアルタイム通信が必要なアプリケーションに特に適しています。

## WebSocketサーバーの作成

アプリケーションでWebSocketを使用するには、WebSocketサーバーを作成する必要があります。 WebSocketプロトコルをサポートするすべてのWebサーバーでこれを行うことができます。この記事の目的には Node.js Web サーバーを使用します。

```javascript
var WebSocketServer = require('ws').Server;

var wss = new WebSocketServer({
  port: 8080
}）;

wss.on('connection', function(ws) {
  ws.on('message', function(message) {
    console.log('Received: %s', message);
  }）;

  ws.send('Hello, world!');
}）;
```

このコードは、着信接続をポート 8080 でリッスンする WebSocket サーバーを作成します。接続が確立されると、サーバーはその接続のWebSocketインスタンスを作成します。その後、サーバーはクライアントからのメッセージを受信します。メッセージを受信すると、コンソールに記録されます。サーバーはまた、最初に接続されたときにクライアントにメッセージを送信します。

WebSocketサーバーは、Node.jsコマンドラインインターフェースとして実行できます。

```
node server.js
```

## WebSocketクライアントの作成

これでWebSocketサーバーが稼働しているため、WebSocketクライアントを作成して接続する必要があります。このドキュメントの目的には、ブラウザベースのJavaScriptクライアントを使用します。

```javascript
var ws = new WebSocket('ws://localhost:8080');

ws.onopen = function() {
  ws.send('Hello, world!');
};

ws.onmessage = function(event) {
  console.log（event.data）;
};
```

このコードはWebSocketインスタンスを作成し、WebSocketサーバーに接続します。このコードは2つのイベントハンドラも定義します。最初のイベントハンドラは「open」イベントです。 This event is fired when the connection is established. The second event handler is for the ```message '' event. This event is fired when the server sends a message to the client.

## Sending and Receiving Messages

Now that we have a WebSocket server and client set up, we can start sending and receiving messages. The ```send '' method can be used to send messages from the client to the server. ```onmessage '' event handler can be used to receive messages from the server.

「JavaScript
ws.send（「こんにちは、世界！」）;

ws.onmessage =関数（イベント）{
  console.log（event.data）;
};
```

このコードでは、「send」メソッドはクライアントからサーバーにメッセージを送信するために使用されます。 「onmessage」イベントハンドラは、サーバーからメッセージを受信するために使用されます。メッセージがコンソールに記録されます。