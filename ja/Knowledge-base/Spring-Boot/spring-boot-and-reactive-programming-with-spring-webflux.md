---
title: Spring WebFlux を使用した Spring Boot とリアクティブ プログラミング
description: 
published: true
date: 2023-02-01T03:18:35.867Z
tags: 
editor: markdown
dateCreated: 2023-02-01T03:18:31.790Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Spring Boot and Reactive Programming with Spring WebFlux***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-reactive-programming-with-spring-webflux)
{.links-list}


  このブログの対象読者は、Spring WebFluxを使用したSpring BootおよびReactiveプログラミングについて学びたいIT開発の専門家です。


# Spring WebFluxを使用したSpring BootおよびReactiveプログラミング

Spring Bootは、開発者がWebアプリケーションをすばやく作成してデプロイできるようにする人気のあるJavaアプリケーションフレームワークです。 Spring BootはSpring Frameworkの上に構築され、Javaプラットフォームを使用しています。

リアクティブプログラミングは、応答性と弾力性に優れたコードを書くのに役立つプログラミングパラダイムです。ブロックされず、非同期のイベントベースのプログラミングスタイルです。

Spring WebFluxは、Spring Frameworkの上に構築されたWebアプリケーション用のレスポンシブプログラミングモデルです。完全に遮断されることなく背圧をサポートし、イベントループ実行モデルを使用します。

この記事では、Spring BootとSpring WebFluxを使用してレスポンシブWebアプリケーションを作成する方法について説明します。また、Reactive Streams APIを使用してイベントストリームを生成する方法を見てみましょう。

## Spring Bootプロジェクトの設定

最初にすべきことは、新しいSpring Bootプロジェクトを作成することです。 Spring Initializr Webサイトを使用して、必要な依存関係を持つプロジェクトを作成できます。

次の依存関係を選択する必要があります。

* Web - Webアプリケーション用
*レスポンシブWeb - レスポンシブプログラミングモデル用
* Lombok - 定型句コードの簡略化

![スプリングイニシャライザ](https://i.imgur.com/Rv4U2in.png)

プロジェクトが作成されると、好みのIDEにインポートできます。 IntelliJ IDEAを使用します。

##ハローワールド

簡単なHello World Webアプリケーションを作成しましょう。クライアントに文字列を返すコントローラを作成します。

まず、 `com.example.demo`パッケージに `HelloController.java`という新しいファイルを作成する必要があります。

```java
package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello, World!";
    }

}
```

`HelloController`クラスから `@RestController`にクラスに注釈を付けました。このコメントは、クラスをWebコントローラとして表示するために使用されます。

また、 `@GetMapping` で `hello()` メソッドに注釈を付けました。このコメントは、HTTP GETリクエストを `hello（）`メソッドにマッピングするために使用されます。

`hello()` メソッドは文字列を返します。この文字列はJSONに変換され、クライアントに返されます。

これで、アプリケーションを実行して `/hello` エンドポイントにアクセスできるようになります。次の出力が表示されます。

```
Hello, World!
```

## リアクティブストリーム

Reactive Streamsは、非遮断背圧を使用した非同期ストリーム処理用のAPIです。 4つのインターフェースで構成されています。

*パブリッシャ - データストリームをエクスポートします。
*加入者 - データストリームを消費します。
*プロセッサ - データストリームを変換します。
* サブスクリプション - パブリッシャとサブスクライバの間の一対一の関係を示します。

Reactive Streamsは、特定のプログラミング言語やプラットフォームにとらわれません。言語に拘束されず、すべてのJVMベースの言語で使用できます。

## ストリームの作成

次に、Reactive Streams APIを使用してイベントストリームを生成する方法を見てみましょう。整数ストリームを解放するために `Publisher`インタフェースを使用します。

まず、 `com.example.demo`パッケージに `Publisher.java`という新しいファイルを作成する必要があります。

```java
package com.example.demo;

import org.reactivestreams.Publisher;
import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

import java.util.concurrent.atomic.AtomicInteger;

public class Publisher implements org.reactivestreams.Publisher<Integer> {

    private Subscriber<? super Integer> subscriber;
    private AtomicInteger counter;

    public Publisher() {
        this.counter = new AtomicInteger();
    }

    @Override
    public void subscribe(Subscriber<? super Integer> s) {
        this.subscriber = s;
        this.subscriber.onSubscribe(new Subscription() {
            @Override
            public void request(long n) {
                for(int i = 0; i < n; i++) {
                    if (counter.incrementAndGet() > 10) {
                        subscriber.onComplete();
                        break;
                    }else{
                        subscriber.onNext(counter.get());
                    }
                }
            }

            @Override
            public void cancel() {

            }
        }）;
    }
}
```

`Publisher`クラスで `Publisher`インタフェースの `subscribe（）`メソッドを実装しました。このメソッドは、ストリームに「購読者」を購読するために使用されます。

`subscribe()` メソッドで匿名の `Subscription` オブジェクトを使用しています。このオブジェクトは「発行者」からデータを要求するために使用されます。 「発行者」に10個の項目を要請しています。

また、Publisherがエクスポートしたアイテムの数を追跡するためにAtomicIntegerを使用しています。

## ストリーム登録

これで、 `Publisher`がエクスポートしたイベントストリームを購読することができます。 `Publisher` インタフェースで `subscribe()` メソッドを使用します。

まず、 `com.example.demo`パッケージに `Subscriber.java`という新しいファイルを作成する必要があります。

```java
package com.example.demo;

import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

public class Subscriber implements org.reactivestreams.Subscriber<Integer> {

    @Override
    public void onSubscribe(Subscription s) {
        s.request（Long.MAX_VALUE）;
    }

    @Override
    public void onNext(Integer integer) {
        System.out.println("Received: " + integer);
    }

    @Override
    public void onError(Throwable t) {
        t.printStackTrace();
    }

    @Override
    public void onComplete() {
        System.out.println("Done!");
    }
}
```

`Subscriber`クラスで`Subscriber`インタフェースの `onSubscribe()`メソッドを実装しました。このメソッドは、イベントストリームを購読するために使用されます。

`onSubscribe()` メソッドで `Publisher` から無制限のイベントストリームを要求しています。

また、`onNext()`、`onError()`、および `onComplete()` メソッドも実装しました。これらのメソッドは、`Publisher`からイベントをエクスポートすると呼び出されます。

## ストリームテスト

これで、 `Publisher`がエクスポートしたイベントストリームをテストできます。

まず、 `com.example.demo`パッケージに `DemoApplicationTests.java`という新しいファイルを作成する必要があります。

```java
package com.example.demo;

import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

ツイートをサイトに埋め込む
public class DemoApplicationTests {

    @Test
    public void testStream() {
        Publisher publisher = new Publisher();
        Subscriber subscriber = new Subscriber();
        publisher.subscribe(subscriber);
    }

}
```

`DemoApplicationTests`クラスで`testStream（）`メソッドを作成しました。この方法では、 `Publisher`と `Subscriber`を生成します。次に、「購読者」を「発行者」に購読します。

テストを実行すると、次の出力が表示されます。

```
Received: 1
Received: 2
Received: 3
Received: 4
Received: 5
Received: 6
Received: 7
Received: 8
Received: 9
Received: 10
ドーン！
```

##レスポンシブWebアプリケーションの作成

Reactive Streams APIの使い方を見てきたので、それを使ってレスポンシブWebアプリケーションを作成する方法を見てみましょう。

レスポンシブWebアプリケーションは、レスポンシブプログラミングモデルを使用するWebアプリケーションです。レスポンシブプログラミングモデルでは、アプリケーションはメッセージ配信を使用して互いに通信する、小さく独立した同時プロセスのセットとして構築されています。

レスポンシブWebアプリケーションでは、Webアプリケーションは、メッセージ配信を使用して互いに通信する、小さく独立した同時プロセスのセットとして構築されています。

## こんにちはリアクティブワールド

簡単な「Hello Reactive World」Webアプリケーションを作成しましょう。クライアントに文字列を返すコントローラを作成します。

まず、 `com.example.demo`パッケージに `HelloReactiveController.java`という新しいファイルを作成する必要があります。

```java
package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import reactor.core.publisher.Mono;

@RestController
public class HelloReactiveController {

    @GetMapping("/hello-reactive")
    public Mono<String> helloReactive() {
        return Mono.just("Hello, Reactive World!");
    }

}
```

`HelloReactiveController`クラスから `@RestController`でクラスに注釈を付けました。このコメントは、クラスをWebコントローラとして表示するために使用されます。

また、 `@GetMapping` で `helloReactive()` メソッドに注釈を付けました。このコメントは、HTTP GETリクエストを `helloReactive（）`メソッドにマッピングするために使用されます。

`helloReactive()` メソッドは `Mono<String>` を返します。 「Mono」は、0個または1個のアイテムを放出するレスポンシブストリームです。この場合、`Mono`は単一の文字列をエクスポートします。

これで、アプリケーションを実行して `/hello-reactive` エンドポイントにアクセスできるようになりました。次の出力が表示されます。

```
Hello、Reactive World！
```

##レスポンシブストリームの作成

単純なレスポンシブWebアプリケーションを作成する方法を見てきたので、より複雑なレスポンシブストリームを作成する方法を見てみましょう。

`Publisher`から放出される整数ストリームを生成します。次に、「Processor」を使用して整数ストリームを文字列ストリームに変換します。最後に、 `Subscriber`を使って文字列ストリームを消費します。

まず、 `com.example.demo`パッケージに `Publisher.java`という新しいファイルを作成する必要があります。

```java
package com.example.demo;

import org.reactivestreams.Publisher;
import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

import java.util.concurrent.atomic.AtomicInteger;

public class Publisher implements org.reactivestreams.Publisher<Integer> {

    private Subscriber<? super Integer> subscriber;
    private AtomicInteger counter;

    public Publisher() {
        this.counter = new AtomicInteger();
    }

    @Override
    public void subscribe(Subscriber<? super Integer> s) {
        this.subscriber = s;
        this.subscriber.onSubscribe(new Subscription() {
            @Override
            public void request(long n) {
                for(int i = 0; i < n; i++) {
                    if (counter.incrementAndGet() > 10) {
                        subscriber.onComplete();
                        break;
                    }else{
                        subscriber.onNext(counter.get());
                    }
                }
            }

            @Override
            public void cancel() {

            }
        }）;
    }
}
```

`Publisher`クラスで `Publisher`インタフェースの `subscribe（）`メソッドを実装しました。このメソッドは、ストリームに「購読者」を購読するために使用されます。

`subscribe()` メソッドで匿名の `Subscription` オブジェクトを使用しています。このオブジェクトは「発行者」からデータを要求するために使用されます。 「発行者」に10個の項目を要請しています。

また、Publisherがエクスポートしたアイテムの数を追跡するためにAtomicIntegerを使用しています。

## ストリーム変換

これで `プロセッサ`を使って整数ストリームを文字列ストリームに変換できるようになりました。 `Processor` インタフェースの `map()` メソッドを使って各整数を文字列に変換します。

まず、 `com.example.demo`パッケージに `Processor.java`という新しいファイルを作成する必要があります。

```java
package com.example.demo;

import org.reactivestreams.Processor;
import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

public class Processor implements org.reactivestreams.Processor<Integer, String> {

    private Subscriber<? super String> subscriber;
    private Subscription subscription;

    @Override
    public void subscribe(Subscriber<? super String> s) {
        this.subscriber = s;
        this.subscriber.onSubscribe(new Subscription() {
            @Override
            public void request(long n) {
                subscription.request(n);
            }

            @Override
            public void cancel() {
                subscription.cancel();
            }
        }）;
    }

    @Override
    public void onSubscribe(Subscription s) {
        this.subscription = s;
        this.subscription.request(Long.MAX_VALUE);
    }

    @Override
    public void onNext(Integer integer) {
        this.subscriber.onNext(integer.toString());
    }

    @Override
    public void onError(Throwable t) {
        this.subscriber.onError(t);
    }

    @Override
    public void onComplete() {
        this.subscriber.onComplete();
    }
}
```

`Processor`クラスで `Processor`インタフェースの `subscribe()`と`onSubscribe()`メソッドを実装しました。これらのメソッドは、ストリームに「加入者」を購読するために使用されます。

`subscribe()` メソッドで匿名の `Subscription` オブジェクトを使用しています。このオブジェクトは「発行者」からデータを要求するために使用されます。 「発行者」に制限のないイベントストリームを要求しています。

また、Publisherがエクスポートしたアイテムの数を追跡するためにAtomicIntegerを使用しています。

## ストリーム消費

これで、 `Processor`が放出する文字列ストリームを使うために `Subscriber`を使うことができます。

まず、 `com.example.demo`パッケージに `Subscriber.java`という新しいファイルを作成する必要があります。

```java
package com.example.demo;

import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

public class Subscriber implements org.reactivestreams.Subscriber<String> {

    @Override
    public void onSubscribe(Subscription s) {
        s.request（Long.MAX_VALUE）;
    }

    @Override
    public void onNext(String s) {
        System.out.println("Received: " + s);
    }

    @Override
    public void onError(Throwable t) {
        t.printStackTrace();
    }

    @Override
    public void onComplete() {
        System.out.println("Done!");
    }
}
```

`サブスクライバ`クラスで`onSubscribe()`メソッドを実装しました。