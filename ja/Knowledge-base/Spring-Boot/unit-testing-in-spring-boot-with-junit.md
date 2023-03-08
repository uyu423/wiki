---
title: JUnit を使用した Spring Boot での単体テスト
description: 
published: true
date: 2023-02-01T17:27:43.885Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:27:41.273Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}



- [Unit Testing in Spring Boot with JUnit***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/unit-testing-in-spring-boot-with-junit)
{.links-list}


# JUnit を使用した Spring Boot での単体テスト

ユニットテストは、ソフトウェアの個々のユニット/コンポーネントをテストして、各ユニットが期待どおりに機能することを確認するソフトウェアテスト方法です。ユニットは、アプリケーションのテスト可能な最小部分です。 Spring Boot では、単体テストは通常 JUnit を使用して記述されます。

JUnit は、Java の一般的なテスト フレームワークです。これは、Github でホストされているオープン ソース プロジェクトです。 JUnit は、テスト駆動開発の開発において重要であり、SUnit に由来する xUnit として総称される単体テスト フレームワークのファミリーの 1 つです。

この記事では、JUnit を使用して Spring Boot アプリケーションを単体テストする方法を見ていきます。 RestController エンドポイントをテストする簡単なテストを作成します。この記事のサンプル コードは、Github で見つけることができます。

## プロジェクトのセットアップ

簡単なSpring Bootプロジェクトをセットアップすることから始めます。 Spring Initializr を使用してプロジェクトを生成します。次の依存関係を選択します。

- ウェブ
-JPA
- H2 データベース
- ロンボク

Lombok は、Java アプリケーションのボイラープレート コードを削減するために使用できるライブラリです。これを使用して、テスト用に記述する必要があるコードの量を減らします。

プロジェクトが生成されたら、選択した IDE にインポートできます。 IntelliJ IDEA を使用します。

## 単体テストを書く

プロジェクトのセットアップが完了したので、単体テストを記述できます。テスト用の新しいパッケージ `com.example.demo.controller` を作成することから始めます。このパッケージでは、新しいクラス `DemoControllerTest` を作成します。

このクラスには @RunWith(SpringRunner.class) と @WebMvcTest(DemoController.class) のアノテーションが付けられます。 `@RunWith` アノテーションは、JUnit に `SpringRunner` クラスを使用してテストを実行するように指示します。 `@WebMvcTest` アノテーションは、Spring MVC コントローラーをテストするために使用されます。 Spring MVC を自動構成し、完全自動構成を無効にします。

`DemoControllerTest` クラスでは、`MockMvc` オブジェクトの `@Autowired` フィールドを作成します。 `MockMvc` は、コントローラーへの HTTP 要求を実行し、応答をアサートするために使用されます。 「@BeforeEach」で注釈を付けた「@Before」メソッドも作成します。このメソッドは、`MockMvc` オブジェクトを初期化するために使用されます。

ジャバ
@RunWith(SpringRunner.class)
@WebMvcTest(DemoController.class)
public class DemoControllerTest {

    @Autowired
    プライベート MockMvc mockMvc;

    @BeforeEach
    public void setup() {
        mockMvc = MockMvcBuilders.webAppContextSetup(webApplicationContext)
                。建てる（）;
    }
}
```java
@RunWith(SpringRunner.class)
@WebMvcTest(DemoController.class)
public class DemoControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @BeforeEach
    public void setup() {
        mockMvc = MockMvcBuilders.webAppContextSetup(webApplicationContext)
                .build();
    }
}
```

`MockMvc` オブジェクトで `perform` メソッドを使用して HTTP リクエストを実行します。 `get` メソッドを使用して `GET` リクエストを作成します。次に、`andExpect` メソッドを使用して、応答のステータスとコンテンツをアサートします。

## テストの実行

これでテストを実行できます。 `./mvnw test` コマンドを使用して、コマンド ラインからテストを実行できます。 IDE 内からテストを実行することもできます。

## 結論

この記事では、JUnit を使用して Spring Boot アプリケーションを単体テストする方法を見てきました。 RestController エンドポイントをテストする簡単なテストを作成しました。