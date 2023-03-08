---
title: TypeScript と Node.js でのデータ ストリームの操作
description: 
published: true
date: 2023-02-17T18:06:39.288Z
tags: 
editor: markdown
dateCreated: 2023-01-30T15:36:42.645Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Working with Data Streams in TypeScript and Node.js***English** version of this document is available*](/en/Knowledge-base/TypeScript/working-with-data-streams-in-typescript-and-node-js)
{.links-list}

    
#はじめに

この記事では、TypeScriptとNode.jsでデータストリームを操作する方法について説明します。 Node.jsで利用可能なさまざまな種類のストリーム、生成方法、およびデータ操作にストリームを使用する方法について説明します。

Node.jsストリームは、データをより効率的に使用するのに役立つ強力なツールです。ストリームはデータを読み書きするために使用でき、一緒に接続してデータに対して複雑な操作を実行できます。

Node.jsで利用可能なストリームには、読み取り可能、書き込み可能、デュアル、および変換の4つの主な種類があります。読み取り可能なストリームを使用すると、ソースからデータを読み取ることができ、書き込み可能なストリームを使用するとターゲットにデータを書き込むことができ、デュアルストリームを使用するとデータを読み書きできます。変換ストリームを使用するとデータを読み書きするとき修正できます。

この記事では、ストリームの最初の2つのタイプである読み取り可能および書き込み可能に焦点を当てます。読み書きできるストリームを作成する方法と、それを使用してデータを読み書きする方法を見てみましょう。

#読みやすいストリームを作成する

Node.jsで読み取り可能なストリームを作成する方法はいくつかあります。最も簡単な方法は `fs.createReadStream()` メソッドを使うことです。

```javascript
const fs = require('fs');

const readableStream = fs.createReadStream('/path/to/file');
```

このメソッドは、ファイルパスを唯一の引数として使用し、ファイルの内容を読み取るために使用できる読み取り可能なストリームを返します。

読み取り可能なストリームを作成する別の方法は、 `net.createServer()` メソッドを使用することです。

```javascript
const net = require（ 'net'）;

const server = net.createServer((socket) => {
  // socket is a readable stream
}）;
```

このメソッドは、TCPサーバーを作成し、サーバーからデータを読み取るために使用できる読み取り可能なストリームを返します。

#書き込み可能なストリームの作成

書き込み可能なストリームは `fs.createWriteStream()` メソッドを使って作成できます。

```javascript
const fs = require('fs');

const writableStream = fs.createWriteStream('/path/to/file');
```

このメソッドは、ファイルへのパスを唯一の引数として使用し、ファイルにデータを書き込むために使用できる書き込み可能なストリームを返します。

書き込み可能なストリームを作成する別の方法は、 `net.createServer()` メソッドを使用することです。

```javascript
const net = require（ 'net'）;

const server = net.createServer((socket) => {
  // socket is a writable stream
}）;
```

このメソッドは、TCPサーバーを作成し、サーバーにデータを書き込むために使用できる書き込み可能なストリームを返します。

#読めるストリームから読む

読み取り可能なストリームを作成したら、 `read()` メソッドを使用してストリームからデータの読み取りを開始できます。

```javascript
readableStream.read();
```

このメソッドはストリームからデータを読み取り、文字列として返します。

読み取ることができるデータがない場合、 `read()` メソッドは `null` を返します。

# 書き込み可能なストリームへの書き込み

書き込み可能なストリームを作成したら、 `write()` メソッドを使用してデータの書き込みを開始できます。

```javascript
writableStream.write('some data');
```

このメソッドはストリームにデータを書き込みます。データは文字列またはバッファです。

#ストリームを一緒に配管する

Node.jsストリームの最も強力な機能の1つは、ストリームを一緒にリンクする機能です。

パイピングを使用すると、1つのストリームのデータが自動的に別のストリームに転送されるように、2つ以上のストリームを一緒にリンクできます。

たとえば、読み取り可能なストリームを書き込み可能なストリームにパイプできます。

```javascript
readableStream.pipe(writableStream);
```

これにより、読み出し可能ストリームのデータが書き込み可能ストリームに書き込まれる。

複数のストリームを一緒にパイプすることもできます。たとえば、読み取り可能なストリームを変換ストリームにパイプし、変換ストリームを書き込み可能なストリームにパイプすることができます。

```javascript
readableStream
  .pipe(transformStream)
  .pipe(writableStream);
```

これにより、読み取り可能なストリームのデータが変換ストリームによって変換され、書き込み可能なストリームに書き込まれます。

#結論

この記事では、TypeScriptとNode.jsでデータストリームを操作する方法について説明しました。 Node.jsで利用可能なさまざまな種類のストリーム、生成方法、およびデータ操作にストリームを使用する方法について説明しました。

Node.jsストリームは、データをより効率的に使用するのに役立つ強力なツールです。ストリームはデータを読み書きするために使用でき、一緒に接続してデータに対して複雑な操作を実行できます。

Node.jsでデータを操作する方法の詳細については、次のような他の便利なリソースを確認してください。

- [Node.jsストリームハンドブック]（https://nodestreams.com/）
- [Node.jsストリームAPI]（https://nodejs.org/api/stream.html）
- [Node.jsでストリーミングデータを扱う]（https://www.twilio.com/blog/working-with-streaming-data-in-node-js）
- [Node.jsストリーム：知っておくべきこと]