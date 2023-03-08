---
title: ネットワーク プログラミングのための Java の Networking API の探索
description: 
published: true
date: 2023-01-31T04:23:51.532Z
tags: 
editor: markdown
dateCreated: 2023-01-31T04:23:49.859Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Exploring Java's Networking API for Network Programming***English** version of this document is available*](/en/Knowledge-base/Java/exploring-java-s-networking-api-for-network-programming)
{.links-list}

    
Javaプログラミングには常に強力なネットワーキングコンポーネントがあります。デスクトップからWeb、モバイルまで、幅広いアプリケーションを開発するために使用できる汎用性の高い言語です。 Javaプラットフォームには、ネットワークプログラミングに必要なすべての機能を提供するネットワーククラスとインタフェースの広範なライブラリがあります。

この記事では、Java Networking APIとそれを使用して実装できるいくつかの一般的なネットワーキングシナリオについて説明します。また、利用可能ないくつかの高度な機能についても見てみましょう。

JavaプラットフォームのネットワーキングAPIは、要求/応答モデルに基づいています。クライアントが要求し、サーバーが応答します。クライアントとサーバーは同じマシン上にあっても別のマシン上にあってもかまいません。要求と応答は任意の形式にすることができますが、最も一般的な形式はHTTPです。

HTTP は World Wide Web で使用される形式です。 TCP / IPプロトコルの上に構築された単純なテキストベースのプロトコル。 HTTP は状態非保存です。つまり、各要求は他の要求とは無関係です。これはWebアプリケーションのための非常に効率的なプロトコルです。

JavaプラットフォームのネットワーキングAPIには、ネットワークプログラミングに必要な低レベル機能を提供する一連のクラスとインタフェースが含まれています。 java.netパッケージには、コアネットワーキングクラスとインタフェースが含まれています。 javax.net パッケージには、コアネットワーキングクラスとインタフェースの拡張が含まれています。

java.net.URL クラスは、Java プラットフォームのネットワーキング API のゲートウェイです。インターネット上のリソースを識別する方法であるUniform Resource Locatorを表します。リソースは、Webページ、画像、ファイル、またはURLで識別できるすべてのものにすることができます。

java.net.URL クラスには、データを読み込み、URL に書き込む複数のメソッドがあります。最も一般的に使用される方法は次のとおりです。

- getContent()
- openConnection()
- オープンストリーム()
- getInputStream()

getContent() メソッドは、URL の内容を表すオブジェクトを返します。 openConnection() メソッドは、URL への接続を表す URLConnection オブジェクトを返します。 openStream() メソッドは、URL からデータを読み取るために使用できる InputStream を返します。 getInputStream() メソッドは、URL からデータを読み取るために使用できる InputStream を返します。

java.net.URLConnection クラスは URL への接続を表します。接続を開き、URLからデータを読み取るために使用できます。 URLConnection クラスには、データを読み込み、URL に書き込む複数のメソッドがあります。最も一般的に使用される方法は次のとおりです。

- getContent()
- getInputStream()
- getOutputStream()
- setDoInput()
- setDoOutput()
- 接続する()

getContent() メソッドは、URL の内容を表すオブジェクトを返します。 getInputStream() メソッドは、URL からデータを読み取るために使用できる InputStream を返します。 getOutputStream() メソッドは、URL にデータを書き込むために使用できる OutputStream を返します。 setDoInput() メソッドは、入力に URLConnection を使用するかどうかを設定します。 setDoOutput() メソッドは、出力に URLConnection を使用するかどうかを設定します。 connect() メソッドは URL への接続を開きます。

java.net.Socket クラスは、2 台のコンピューター間の通信エンドポイントであるソケットを表します。ソケットはデータの読み書きに使用できます。最も一般的に使用される方法は次のとおりです。

- getInputStream()
- getOutputStream()
- 閉じる()

getInputStream() メソッドは、Socket からデータを読み取るために使用できる InputStream を返します。 getOutputStream() メソッドは、Socket にデータを書き込むために使用できる OutputStream を返します。 close() メソッドはソケットを閉じます。

java.net.ServerSocket クラスは、サーバーの通信エンドポイントであるサーバーソケットを表します。 ServerSocketを使用して、クライアントからの着信接続を受け入れることができます。最も一般的に使用される方法は次のとおりです。

- 同意する()
- 閉じる()

accept() メソッドは、クライアントからの着信接続を受け入れます。 close() メソッドは ServerSocket を閉じます。

JavaプラットフォームのネットワーキングAPIを使用するには、TCP / IPプロトコルの基本的な理解が必要です。 TCP / IPは、インターネットからコンピュータ間の通信に使用されるプロトコルです。 TCP（Transport Control Protocol）とIP（Internet Protocol）の2つの部分からなるプロトコル。

転送制御プロトコル（TCP）は、データが正しい順序で正しい順序で転送されるようにする役割を果たします。 2台のコンピュータ間の接続を確立し、データを小さなパケットに転送してこれを行います。その後、パケットは宛先で正しい順序で再組み立てされます。

インターネットプロトコル（IP）は、送信元から宛先にデータパケットをルーティングする役割を果たします。これは、ルーティングテーブルとして知られる一連のルールを使用して行われます。

JavaプラットフォームのネットワーキングAPIには、ネットワークプログラミングに必要な低レベル機能を提供する一連のクラスとインタフェースが含まれています。 java.netパッケージには、コアネットワーキングクラスとインタフェースが含まれています。 javax.net パッケージには、コアネットワーキングクラスとインタフェースの拡張が含まれています。

java.net.URL クラスは、Java プラットフォームのネットワーキング API のゲートウェイです。インターネット上のリソースを識別する方法であるUniform Resource Locatorを表します。リソースは、Webページ、画像、ファイル、またはURLで識別できるすべてのものにすることができます。

java.net.URL クラスには、データを読み込み、URL に書き込む複数のメソッドがあります。最も一般的に使用される方法は次のとおりです。

- getContent()
- openConnection()
- オープンストリーム()
- getInputStream()

getContent() メソッドは、URL の内容を表すオブジェクトを返します。 openConnection() メソッドは、URL への接続を表す URLConnection オブジェクトを返します。 openStream() メソッドは、URL からデータを読み取るために使用できる InputStream を返します。 getInputStream() メソッドは、URL からデータを読み取るために使用できる InputStream を返します。

java.net.URLConnection クラスは URL への接続を表します。接続を開き、URLからデータを読み取るために使用できます。 URLConnection クラスには、データを読み込み、URL に書き込む複数のメソッドがあります。最も一般的に使用される方法は次のとおりです。

- getContent()
- getInputStream()
- getOutputStream()
- setDoInput()
- setDoOutput()
- 接続する()

getContent() メソッドは、URL の内容を表すオブジェクトを返します。 getInputStream() メソッドは、URL からデータを読み取るために使用できる InputStream を返します。 getOutputStream() メソッドは、URL にデータを書き込むために使用できる OutputStream を返します。 setDoInput() メソッドは、入力に URLConnection を使用するかどうかを設定します。 setDoOutput() メソッドは、出力に URLConnection を使用するかどうかを設定します。 connect() メソッドは URL への接続を開きます。

java.net.Socket クラスは、2 台のコンピューター間の通信エンドポイントであるソケットを表します。ソケットはデータの読み書きに使用できます。最も一般的に使用される方法は次のとおりです。

- getInputStream()
- getOutputStream()
- 閉じる()

getInputStream() メソッドは、Socket からデータを読み取るために使用できる InputStream を返します。 getOutputStream() メソッドは、Socket にデータを書き込むために使用できる OutputStream を返します。 close() メソッドはソケットを閉じます。

java.net.ServerSocket クラスは、サーバーの通信エンドポイントであるサーバーソケットを表します。 ServerSocketを使用して、クライアントからの着信接続を受け入れることができます。最も一般的に使用される方法は次のとおりです。

- 同意する()
- 閉じる()

accept() メソッドは、クライアントからの着信接続を受け入れます。 close() メソッドは ServerSocket を閉じます。

java.net.DatagramSocket クラスは、データグラムを送受信するための通信エンドポイントであるデータグラムソケットを表します。データグラムは、長く続く接続なしで送信できる小さな独立したメッセージです。最も一般的に使用される方法は次のとおりです。

- 送る()
- 受け取る()
- 閉じる()

send() メソッドはデータグラムを送信します。 receive() メソッドはデータグラムを受け取ります。 close() メソッドは DatagramSocket を閉じます。

java.net.DatagramPacket クラスは、長く続く接続を必要とせずに送信できる、小さく独立したメッセージであるデータグラムパケットを表します。最も一般的に使用される方法は次のとおりです。

- getData()
- getLength()
- getAddress()
- getPort()

getData() メソッドは、パケットに含まれるデータを返します。 getLength() メソッドは、パケットに含まれるデータの長さを返します。 getAddress() メソッドは送信者のアドレスを返します。 getPort() メソッドは送信者のポートを返します。

Javaプログラミングには常に強力なネットワーキングコンポーネントがあります。デスクトップからWeb、モバイルまで、幅広いアプリケーションを開発するために使用できる汎用性の高い言語です。 Javaプラットフォームには、ネットワークプログラミングに必要なすべての機能を提供するネットワーククラスとインタフェースの広範なライブラリがあります。

この記事では、Java Networking APIとそれを使用して実装できるいくつかの一般的なネットワーキングシナリオについて説明しました。また、利用可能ないくつかの高度な機能も見ました。