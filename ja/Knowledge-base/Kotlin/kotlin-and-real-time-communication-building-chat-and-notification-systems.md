---
title: Kotlin とリアルタイム コミュニケーション: チャットと通知システムの構築
description: 
published: true
date: 2023-01-31T19:44:36.589Z
tags: 
editor: markdown
dateCreated: 2023-01-31T19:44:32.803Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Kotlin and Real-time Communication: Building Chat and Notification Systems***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-real-time-communication-building-chat-and-notification-systems)
{.links-list}



#Kotlinとリアルタイムコミュニケーション：チャットと通知システムの構築

JVM言語として、Kotlinの怪我は彗星のように起こりました。 2010年にJetBrainsでプロジェクトとして初めて発表した後、着実に人気を得て、2017年には「2番目に愛される」（https://www.infoworld.com/article/3226274/application-development/kotlin-trumpets-its-way -to-second-most-loved-language-in-stack-overflow-developer-survey.html) 言語をスタックオーバーフロー開発者アンケートに含めます。

Kotlinが人気の主な理由の1つは、Javaとの相互運用性です。つまり、KotlinコードはJavaをサポートするすべてのプラットフォームで実行できるため、さまざまなデバイスをターゲットにしたい開発者にとって魅力的なオプションになります。

Kotlinが人気のもう一つの理由は、リアルタイム通信（RTC）サポートです。 RTCは、複数の当事者間の即時通信を可能にする技術です。チャット、ビデオ会議、ゲームなどのアプリケーションに使用されます。

KotlinのRTCサポートはJava WebSocket APIに基づいています。 WebSocket API は、ブラウザとサーバー間で通信する標準的な方法を提供します。リアルタイムアプリケーション用に設計されており、すべての主要なブラウザでサポートされています。

KotlinのRTCサポートはチャットと通知システムの開発に理想的な選択です。この記事では、Kotlinを使用して簡単なチャットシステムを開発する方法を説明します。また、KotlinのRTCサポートを使用して簡単な通知システムを開発する方法も紹介します。

## Kotlinによるチャットシステムの開発

Kotlinでチャットシステムを開発するのは簡単です。 IntelliJ IDEA IDEを使用して新しいKotlinプロジェクトを作成することから始めましょう。

プロジェクト名を「KotlinChat」と指定し、プロジェクトのデフォルト設定を使用します。

プロジェクトが作成されたら、build.gradleファイルに次の依存関係を追加する必要があります。

```kotlin
implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:1.3.5"
implementation "org.jetbrains.kotlinx:kotlinx-coroutines-websockets:1.3.5"
```

最初の依存関係はKotlinのコルーチンのサポートです。コルーチンは同時プログラミングのための強力なツールです。これにより、非同期コードと非ブロックコードを書くことができます。

2番目の依存関係は、KotlinのWebSocketサポートに関するものです。 WebSocket APIを使用してチャットサーバーと通信します。

依存関係を設定したので、チャットシステム用のコードを書くことができます。

Main.ktという名前の新しいファイルを作成することから始めましょう。このファイルにはチャットシステムのエントリポイントが含まれます。

Main.ktで基本機能を定義します。この関数はチャットシステムの起動時に呼び出されます。

```kotlin
fun main() {

}
```

基本機能内で ChatClient クラスの新しいインスタンスを作成します。このクラスはチャットサーバーへの接続を管理します。

```kotlin
fun main() {
    val chatClient = ChatClient()
}
```

次に、 chatClient インスタンスで connect 関数を呼び出します。この機能はチャットサーバーへの接続を確立します。

```kotlin
fun main() {
    val chatClient = ChatClient()
    chatClient.connect()
}
```

接続関数は、チャットサーバーのURLとコールバック関数の2つの引数を使用します。コールバック関数は、チャットサーバーに接続すると呼び出されます。

```kotlin
fun main() {
    val chatClient = ChatClient()
    chatClient.connect("ws://localhost:8080/chat", {
        println("Connected to chat server")
    }）
}
```

接続が確立されたら、メッセージの送受信を開始できます。

メッセージを送信するために、 chatClient インスタンスで send 関数を呼び出します。この関数は、送信するメッセージとコールバック関数の2つの引数を使用します。メッセージが送信されると、コールバック関数が呼び出されます。

```kotlin
fun main() {
    val chatClient = ChatClient()
    chatClient.connect("ws://localhost:8080/chat", {
        println("Connected to chat server")
        chatClient.send("Hello, world!", {
            println("Message sent")
        }）
    }）
}
```

メッセージを受信するために、 chatClient インスタンスで受信機能を呼び出します。この関数はコールバック関数を引数として使用します。コールバック関数は、メッセージが受信されると呼び出されます。

```kotlin
fun main() {
    val chatClient = ChatClient()
    chatClient.connect("ws://localhost:8080/chat", {
        println("Connected to chat server")
        chatClient.send("Hello, world!", {
            println("Message sent")
        }）
        chatClient.receive {
            println("Message received: $it")
        }
    }）
}
```

受信関数は、受信したメッセージを引数として使用してコールバック関数を呼び出します。

それでは、メッセージの送受信方法を見てみましたので、ChatClientクラスを見てみましょう。

ChatClient クラスには次のコードが含まれています。

```kotlin
class ChatClient {

    private val websocket = WebSocket()

    fun connect(url: String, onConnect: () -> Unit) {
        websocket.connect(url) {
            onConnect()
        }
    }

    fun send(message: String, onSend: () -> Unit) {
        websocket.send(message) {
            onSend()
        }
    }

    fun receive(onReceive: (String) -> Unit) {
        websocket.receive {
            onReceive(it)
        }
    }
}
```

ChatClient クラスには、接続、送信、受信の 3 つの機能があります。接続と転送機能の使用方法はすでに見てきました。

受信機能は送信機能と似ています。コールバック関数を引数として使用します。コールバック関数は、受信したメッセージを引数として使用して呼び出されます。

ChatClient クラスには websocket プロパティもあります。このプロパティはWebSocket型です。 WebSocketクラスは、Java WebSocket APIを取り巻くKotlinラッパーです。

ChatClient クラスは WebSocket クラスを使用してチャットサーバーと通信します。接続、送受信機能はすべて、WebSocket クラスの対応する機能を囲むラッパーです。

## Kotlinによる通知システムの開発

Kotlinで通知システムを開発するのは簡単です。 IntelliJ IDEA IDEを使用して新しいKotlinプロジェクトを作成することから始めましょう。

プロジェクト名を「KotlinNotifications」と指定し、プロジェクトのデフォルト設定を使用します。

プロジェクトが作成されたら、build.gradleファイルに次の依存関係を追加する必要があります。

```kotlin
implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:1.3.5"
implementation "org.jetbrains.kotlinx:kotlinx-coroutines-websockets:1.3.5"
```

最初の依存関係はKotlinのコルーチンのサポートです。コルーチンは同時プログラミングのための強力なツールです。これにより、非同期コードと非ブロックコードを書くことができます。

2番目の依存関係は、KotlinのWebSocketサポートに関するものです。 WebSocket APIを使用して通知サーバーと通信します。

依存関係が設定されているので、通知システムのコード作成を開始できます。

Main.ktという名前の新しいファイルを作成することから始めましょう。このファイルには、通知システムのエントリポイントが含まれます。

Main.ktで基本機能を定義します。この関数は、通知システムの起動時に呼び出されます。

```kotlin
fun main() {

}
```

基本機能内に NotificationClient クラスの新しいインスタンスを作成します。このクラスは通知サーバーへの接続を管理します。

```kotlin
fun main() {
    val notificationClient = NotificationClient()
}
```

次に、notificationClientインスタンスで接続関数を呼び出します。この機能は、通知サーバーへの接続を確立します。

```kotlin
fun main() {
    val notificationClient = NotificationClient()
    notificationClient.connect()
}
```

接続関数は、通知サーバーのURLとコールバック関数の2つの引数を使用します。コールバック関数は、通知サーバーへの接続が確立されると呼び出されます。

```kotlin
fun main() {
    val notificationClient = NotificationClient()
    notificationClient.connect("ws://localhost:8080/notifications", {
        println("Connected to notification server")
    }）
}
```

接続が確立されたら、メッセージの送受信を開始できます。

メッセージを送信するには、notificationClientインスタンスからsend関数を呼び出します。この関数は、送信するメッセージとコールバック関数の2つの引数を使用します。メッセージが送信されると、コールバック関数が呼び出されます。

```kotlin
fun main() {
    val notificationClient = NotificationClient()
    notificationClient.connect("ws://localhost:8080/notifications", {
        println("Connected to notification server")
        notificationClient.send("Hello, world!", {
            println("Message sent")
        }）
    }）
}
```

メッセージを受信するには、notificationClientインスタンスで受信機能を呼び出します。この関数はコールバック関数を引数として使用します。コールバック関数は、メッセージが受信されると呼び出されます。

```kotlin
fun main() {
    val notificationClient = NotificationClient()
    notificationClient.connect("ws://localhost:8080/notifications", {
        println("Connected to notification server")
        notificationClient.send("Hello, world!", {
            println("Message sent")
        }）
        notificationClient.receive {
            println("Message received: $it")
        }
    }）
}
```

受信関数は、受信したメッセージを引数として使用してコールバック関数を呼び出します。

ここでメッセージの送受信方法を見てみましたので、NotificationClientクラスを見てみましょう。

NotificationClient クラスには次のコードが含まれています。

```kotlin
class NotificationClient {

    private val websocket = WebSocket()

    fun connect(url: String, onConnect: () -> Unit) {
        websocket.connect(url) {
            onConnect()
        }
    }

    fun send(message: String, onSend: () -> Unit) {
        websocket.send(message) {
            onSend()
        }
    }

    fun receive(onReceive: (String) -> Unit) {
        websocket.receive {
            onReceive(it)
        }
    }
}
```

NotificationClient クラスには、接続、送信、受信の 3 つの機能があります。接続と転送機能の使用方法はすでに見てきました。

受信機能は送信機能と似ています。コールバック関数を引数として使用します。コールバック関数は、受信したメッセージを引数として使用して呼び出されます。

NotificationClient クラスには websocket プロパティもあります。このプロパティはWebSocket型です。 WebSocketクラスは、Java WebSocket APIを取り巻くKotlinラッパーです。

NotificationClient クラスは WebSocket クラスを使用して通知サーバーと通信します。接続、送受信機能はすべて、WebSocket クラスの対応する機能を囲むラッパーです。