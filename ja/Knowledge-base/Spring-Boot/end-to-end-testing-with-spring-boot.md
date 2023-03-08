---
title: Spring Bootを使用したエンドツーエンドテスト
description: 
published: true
date: 2023-02-01T17:40:26.138Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:40:23.614Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}



- [End-to-end Testing with Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/end-to-end-testing-with-spring-boot)
{.links-list}


# Spring BootによるEnd-to-Endテスト

Webアプリケーションを構築する際のエンドツーエンド（E2E）テストは、開発プロセスの重要な部分です。定義に応じて、E2Eテストは最初から最後までアプリケーション全体をカバーするテストタイプです。

従来のWebアプリケーションでは、フロントエンドコードはバックエンドサーバーに要求を送信し、要求を処理して応答を返します。 Spring Bootアプリケーションを使用すると、フロントエンドコードは依然として要求を生成しますが、バックエンドサーバーはSpring Bootアプリケーションです。

E2Eテストは、開発者がユーザーインターフェイス（UI）からバックエンドサーバーまで、アプリケーション全体をテストできるため、重要です。さらに、開発者はアプリケーションが本番環境にデプロイされたときにどのように機能するかをテストできます。

利用可能なさまざまなE2Eテストフレームワークがありますが、この記事ではSpring BootとSpring Bootが提供するE2Eテストフレームワークに焦点を当てます。

## スプリングブートとは何ですか？

Spring Bootは、開発者がSpringベースのアプリケーションをすばやく作成してデプロイできるようにするフレームワークです。次のように開発と展開をより簡単にするためのいくつかの機能を提供します。

- 組み込みトムキャットサーバー
- 自動構成
- スターターテンプレート

Spring Bootは、Springベースのアプリケーションを簡単に作成してデプロイできるため、E2Eテスト開発に優れた選択肢です。

## E2Eテストフレームワークとは何ですか？

E2Eテストフレームワークは、開発者がE2Eテストをすばやく作成して実行できるツールのセットです。 JUnitテストフレームワークに基づいており、次のようにE2Eテストを簡単にするためのいくつかの機能を提供します。

- テスト用にSpring Bootアプリケーションを設定するために使用できる@SpringBootTestアノテーション
- テスト用にWebサーバーを構成するために使用できる@WebIntegrationTestアノテーション
- SpringアプリケーションコンテキストでBeanをモックするために使用できる@MockBeanアノテーション

E2Eテストフレームワークは、E2Eテストを簡単に作成して実行できるため、E2Eテストを開発するための優れた選択肢です。

## E2Eテストの作成

次に、E2Eテストフレームワークを使用してE2Eテストを作成する方法を見てみましょう。ユーザーのリストを返す単一のエンドポイントを持つ単純なSpring Bootアプリケーションをテストします。

最初にすべきことは、新しいJUnitテストクラスを作成し、@SpringBootTestでコメントを追加することです。

「Java
ツイートをサイトに埋め込む
パブリッククラスUserControllerTest {

}
```java
@SpringBootTest
public class UserControllerTest {

}
```

@Testアノテーションは、メソッドをテストメソッドとして表示するために使用されます。

テストメソッドでUserControllerインスタンスを作成し、getUsers（）メソッドを呼び出す必要があります。

「Java
@試験
パブリック無効 testGetUsers() {
    UserController userController = new UserController();
    List<User> user = userController.getUsers();
}
```java
@Test
public void testGetUsers() {

}
```

リストに予想されるユーザー数が含まれていると主張することもできます。

「Java
@試験
パブリック無効 testGetUsers() {
    UserController userController = new UserController();
    List<User> user = userController.getUsers();
    assertThat（ユーザー）。hasSize（2）;
}
```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
}
```

完全なE2Eテストは次のとおりです。

「Java
ツイートをサイトに埋め込む
パブリッククラスUserControllerTest {

    @試験
    パブリック無効 testGetUsers() {
        UserController userController = new UserController();
        List<User> user = userController.getUsers();
        assertThat(ユーザー)
            .contains(new User("user1@example.com", "ユーザー 1"),
                      new User("user2@example.com", "ユーザー 2"));
    }
}
```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
    assertThat(users).isNotEmpty();
}
```

## 結論

この記事では、E2Eテストフレームワークを使用してE2Eテストを作成して実行する方法について説明しました。 @SpringBootTestと@Testアノテーションを使ってSpring Bootアプリケーションを設定し、メソッドをテストメソッドとして表示する方法も見ました。