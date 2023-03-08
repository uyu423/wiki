---
title: TypeScript と WebSocket を使用したリアルタイム アプリケーションの作成
description: 
published: true
date: 2023-01-31T10:57:33.918Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:57:32.382Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Creating Real-Time Applications with TypeScript and WebSockets***English** version of this document is available*](/en/Knowledge-base/TypeScript/creating-real-time-applications-with-typescript-and-websockets)
{.links-list}



# TypeScriptとWebSocketでリアルタイムアプリケーションを作成する

WebSocketはリアルタイムアプリケーションを作成するための強力なツールです。 TypeScriptと組み合わせることで、静的型チェック、コード補完などにより、優れた開発体験を提供できます。この記事では、TypeScriptとWebSocketを使用して簡単なチャットアプリケーションを作成する方法について説明します。

## WebSocketとは何ですか？

WebSocketは、既存のTCP接続を介して双方向リアルタイム通信チャネルを作成する技術です。すべての主要なブラウザでサポートされており、シンプルなチャットクライアントから複雑なマルチプレイヤーゲームまで、さまざまなアプリケーションを作成するために使用できます。

##はじめに

開始するには、WebSocket接続を処理できるサーバーを設定する必要があります。この記事では、広く使用されているNode.jsフレームワークであるExpressを使用します。

まず、プロジェクトの新しいディレクトリを作成し、依存関係をインストールします。

```
mkdir chat-app
cd chat-app
npm init -y
npm install --save express
npm install --save ws
```

次に、サーバーコード用のファイルを作成します。

```
touch server.js
```

そして、次のコードを貼り付けます。

```javascript
const express = require('express');
const WebSocket = require（ 'ws'）;

const app = express();

const PORT = process.env.PORT || 8080;

const server = app.listen(PORT, () => {
  console.log( `Server listening on port ${PORT}`);
}）;

const wss = new WebSocket.Server（{server}）;

wss.on('connection', (ws) => {
  console.log('Client connected');

  ws.on('message', (message) => {
    console.log(`Received message: ${message}`);
  }）;

  ws.send('Hello!');
}）;
```

ここで何が起こっているのかを分析しましょう。まず、ExpressとWebSocketモジュールが必要です。次に、Expressサーバーを作成し、ポート8080でリッスンするように構成します。次に、Expressサーバーを 'server'オプションとして渡して新しいWebSocketサーバーを作成します。

次に、クライアントがWebSocketサーバーに接続するときにイベントハンドラを設定します。クライアントが接続すると、コンソールにメッセージを記録します。次に、クライアントがメッセージを送信するときにイベントハンドラを設定します。メッセージが受信されたら、コンソールに戻ります。最後に、クライアントにメッセージを送信します。

サーバーを実行するには、node コマンドを使用できます。

```
node server.js
```

## クライアントの生成

それでは、サーバーが稼働して実行されているので、クライアントを作成してみましょう。この記事では、広く使用されているReactフレームワークを使用します。

まず、依存項目をインストールする必要があります。

```
npm install --save react
npm install --save react-dom
npm install --save @types/react
npm install --save @types/react-dom
npm install --save ws
npm install --save @types/ws
```

次に、クライアントコード用のファイルを作成します。

```
touch client.js
```

そして、次のコードを貼り付けます。

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import * as ws from 'ws';

const socket = new ws('ws://localhost:8080');

socket.onopen=()=>{
  console.log（ 'Connected to server'）;
};

socket.onmessage=(event)=>{
  console.log（event.data）;
};

socket.send('Hello from the client!');

ReactDOM.render(
  <div>Hello、world！</div>、
  document.getElementById('root')
）;
```

まず、ReactおよびReactDOMモジュールをインポートします。次に、WebSocketモジュールをインポートします。次に、サーバーのURLを渡して新しいWebSocketインスタンスを作成します。

次に、ソケットが開いている時点とメッセージが受信された時点のイベントハンドラを設定します。ソケットが開いたら、コンソールにメッセージを記録します。メッセージが受信されたら、コンソールに戻ります。最後に、サーバーにメッセージを送信します。

##結論

この記事では、TypeScriptとWebSocketを使用して簡単なチャットアプリケーションを作成する方法について説明しました。この例は簡単ですが、リアルタイムアプリケーションを作成するためのWebSocketの機能を示しています。