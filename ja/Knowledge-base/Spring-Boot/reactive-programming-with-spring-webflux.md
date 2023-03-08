---
title: Spring WebFlux を使用したリアクティブ プログラミング
description: 
published: true
date: 2023-01-31T19:04:52.651Z
tags: 
editor: markdown
dateCreated: 2023-01-31T19:04:48.923Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Reactive Programming with Spring WebFlux***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/reactive-programming-with-spring-webflux)
{.links-list}



# Spring WebFluxを使用したリアクティブプログラミング

リアクティブプログラミングは、データストリームおよび変更伝播に関連する宣言的プログラミングパラダイムです。これは、静的（配列など）または動的（イベントエミッタなど）のデータストリームを簡単に表現でき、アプリケーションがデータストリームの変更に反応できることを意味します。

より反応的で弾力性のあるアプリケーションの需要が高まるにつれて、レスポンシブプログラミングの必要性が高まっています。過去には、アプリケーションが単一のコードベースにすべての機能を含むモノリシックに構築されることが多かった。これにより、コードベースの一部が変更されると、他の部分で予期しない結果が生じる可能性があり、応答性を達成することが困難になります。

リアクティブプログラミングは、アプリケーションの異なる部分を分離して独立して構築するためのよりモジュール化されたアプローチを可能にします。これにより、コードベースの一部を変更しても他の部分に影響を与える可能性が少なく、レスポンシブアプリケーションを簡単に作成できます。

Spring WebFluxは、Reactorプロジェクトの上に構築されたレスポンシブWebフレームワークです。応答性と弾力性に優れ、他の反応性ライブラリと簡単に統合できるWebアプリケーションを構築できます。

この記事では、Spring WebFluxを使用してレスポンシブWebアプリケーションを構築する方法について説明します。また、反応的アプローチを使用するときに得ることができるいくつかの利点についても見てみましょう。

##リアクティブプログラミングとは？

リアクティブプログラミングは、データストリームおよび変更伝播に関連する宣言的プログラミングパラダイムです。これは、静的（配列など）または動的（イベントエミッタなど）のデータストリームを簡単に表現でき、アプリケーションがデータストリームの変更に反応できることを意味します。

より反応的で弾力性のあるアプリケーションの需要が高まるにつれて、レスポンシブプログラミングの必要性が高まっています。過去には、アプリケーションが単一のコードベースにすべての機能を含むモノリシックに構築されることが多かった。これにより、コードベースの一部が変更されると、他の部分で予期しない結果が生じる可能性があり、応答性を達成することが困難になります。

リアクティブプログラミングは、アプリケーションの異なる部分を分離して独立して構築するためのよりモジュール化されたアプローチを可能にします。これにより、コードベースの一部を変更しても他の部分に影響を与える可能性が少なく、レスポンシブアプリケーションを簡単に作成できます。

リアクティブプログラミングは、イベントおよびイベントハンドラの概念を中心にアプリケーションを設計する方法であるオブザーバパターンに基づいています。オブザーバーパターンでは、オブジェクト（トピックと呼ばれる）はオブザーバーのリストを保持し、興味深いことが発生した場合にそれを通知します。その後、観察者は適切な措置を講じることができる。

![リアクティブプログラミング](https://i.imgur.com/EwP52Uv.png)

リアクティブプログラミングでは、データストリームはトピックであり、オブザーバはデータの消費者です。消費者は、適切であると判断される方法でデータに応答することを選択することができる。

リアクティブプログラミングは関数型プログラミングに根ざしており、多くの同じ原則を共有しています。特に、リアクティブプログラミングは、プログラマがどのように起こるかではなく、起こりたいことを宣言する宣言的プログラミングのアイデアに基づいています。

## Spring WebFluxとは何ですか？

Spring WebFluxは、Reactorプロジェクトの上に構築されたレスポンシブWebフレームワークです。応答性と弾力性に優れ、他の反応性ライブラリと簡単に統合できるWebアプリケーションを構築できます。

Spring WebFluxは、伝統的なSpring MVCモデルの代替品です。従来のモデルでは、Web要求は単一のスレッドによって処理され、スレッドが完了すると応答が返されます。応答を待っている間にスレッドがブロックされるため、パフォーマンスの問題が発生する可能性があります。

レスポンシブモデルでは、Web要求は非ブロックスレッドによって処理され、応答はすぐに返されます。これにより、応答を待っている間にスレッドがブロックされないため、パフォーマンスが向上します。

![スプリングウェブフラックス](https://i.imgur.com/5B6qDfu.png)

Spring WebFluxは、生産者が消費者が処理できるよりも多くのデータを生成しないようにデータフローを管理する方法であるバックプレッシャーもサポートしています。これは、消費者が圧倒されるのを防ぐため、消費者が生産者に追いつくことができない状況で重要です。

バックプレッシャーは、リアクティブプログラミングの標準セットであるリアクティブストリーム仕様によって管理されます。 Spring WebFluxはReactive Streams仕様を実装し、すぐに背圧サポートを提供します。

##はじめに

このセクションでは、Spring WebFluxを起動する方法を見てみましょう。ユーザーのリストを表示する簡単なWebアプリケーションを作成します。

### 前提条件

始める前に、次のツールがインストールされていることを確認してください。

* Java 8以上
*メイブン3.5以上

###プロジェクトの作成

Spring Initializrツールを使用してプロジェクトを作成できます。このツールを使用すると、プロジェクトに必要な依存関係を選択してプロジェクト構造を作成できます。

次の依存関係を選択する必要があります。

* Web - この依存関係はWebFluxフレームワークを含み、Webアプリケーションを構築するために必要です。
* Lombok - この依存関係は定型句コードを減らすために使用され、オプションです。

依存関係が選択されたら、プロジェクト構造を作成できます。

### 依存関係の追加

次に、前の手順で選択した依存関係を `pom.xml`ファイルに追加する必要があります。

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-webflux</artifactId>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>
```

### ユーザーモデルの作成

ユーザーデータを表すモデルを作成する必要があります。 `src/main/java/com/example`ディレクトリに`User.java`ファイルを作成することでこれを行うことができます。

```java
@Data
public class User {
    private String id;
    private String name;
    private String email;
}
```

Lombokライブラリの `@Data`コメントを使って定型句コードを減らしました。このコメントは、ゲッター、セッター、および toString メソッドを生成します。

### ユーザーサービスの作成

次に、ユーザーデータをインポートするサービスを作成する必要があります。 `src/main/java/com/example`ディレクトリに`UserService.java`ファイルを作成することでこれを行うことができます。

```java
@Service
public class UserService {
    private List<User> users = new ArrayList<>();

    public UserService() {
        this.users.add(new User("1", "John Doe", "john.doe@example.com"));
        this.users.add(new User("2", "Jane Doe", "jane.doe@example.com"));
    }

    public List<User> getUsers() {
        return this.users;
    }
}
```

このサービスでは、データのインポートに使用できるユーザーのリストを作成しました。

### ユーザーコントローラの作成

次に、Web要求を処理するコントローラを作成する必要があります。 `src/main/java/com/example`ディレクトリに`UserController.java`ファイルを作成することでこれを行うことができます。

```java
@RestController
@RequestMapping("/users")
public class UserController {
    private UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping
    public Flux<User> getUsers() {
        return this.userService.getUsers()
                .stream()
                .map(user -> User.builder()
                        .id(user.getId())
                        .name(user.getName())
                        .email(user.getEmail())
                        .build())
                .collect(Collectors.toList())
                .flux();
    }
}
```

このコントローラでは、 `/users` パスを `getUsers()` メソッドにマップしました。このメソッドはサービスからユーザーのリストを取得し、`Flux`として返します。

「フラックス」は、非同期的にエクスポートできるデータストリームです。 RxJavaのObservableに似ています。

### アプリケーションの実行

これで、次のコマンドを実行してアプリケーションを実行できます。

```
./mvnw spring-boot:run
```

これで `http://localhost:8080/users` からアプリケーションにアクセスできます。

##結論

この記事では、Spring WebFluxを使用してレスポンシブWebアプリケーションを構築する方法について説明しました。我々はまた、反応的アプローチを使用するときに得ることができるいくつかの利点についても見てきました。

リアクティブプログラミングの詳細については、次のリソースを参照してください。

* [リアクティブプログラミング]（https://en.wikipedia.org/wiki/Reactive_programming）
* [リアクティブストリーム]（http://www.reactive-streams.org/）
* [リアクター](https://projectreactor.io/)
* [スプリングウェブフラックス](https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html)