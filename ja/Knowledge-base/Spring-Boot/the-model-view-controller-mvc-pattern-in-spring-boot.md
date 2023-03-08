---
title: Spring Boot のモデル ビュー コントローラー (MVC) パターン
description: 
published: true
date: 2023-02-01T06:57:43.312Z
tags: 
editor: markdown
dateCreated: 2023-02-01T06:57:41.714Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [The Model-View-Controller (MVC) Pattern in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-model-view-controller-mvc-pattern-in-spring-boot)
{.links-list}



#Spring BootのModel-View-Controller（MVC）パターン

MVC（Model-View-Controller）は、アプリケーションをモデル、ビュー、およびコントローラの3つの主要な論理コンポーネントに分割するアーキテクチャソフトウェア設計パターンです。

MVCパターンは通常、ビジネスロジック（モデル）と制御フロー（コントローラ）からプレゼンテーションレイヤ（ビュー）を分離するためにWebアプリケーションで使用されます。これらの問題を分離することで、コードベースをクリーンでメンテナンス可能に保ち、アプリケーションをより簡単にテストして拡張できます。

Spring MVCアプリケーションでは、コントローラはユーザー要求を処理し、適切な応答を生成する役割を果たします。ビューはユーザーに応答をレンダリングする役割を果たします。モデルは、ビューに表示するデータを格納するデータ構造です。

MVCパターンはWebアプリケーションに限定されません。デスクトップ、モバイル、Webなど、あらゆる種類のアプリケーションで使用できます。

## MVCパターンはどのように機能しますか？

ユーザー要求がアプリケーションに入ると、コントローラはそれを処理する責任があります。コントローラはレンダリングするビューを決定し、ビューに表示するデータをビューに渡します。その後、ビューはユーザーに応答をレンダリングします。

MVCパターンには次の利点があります。

- アプリケーションの問題を分離し、コードベースのメンテナンスとテストを容易にします。
- アプリケーションを簡単に拡張できます。
- アプリケーションに新機能を簡単に追加できます。

## Spring BootでMVCパターンを実装する

Spring Bootは、スタンドアロンのプロダクションクラスSpringベースのアプリケーションを簡単に作成できる人気のあるJava Webアプリケーションフレームワークです。

Spring Boot MVCアプリケーションは通常、次の3つの層で構成されています。

- コントローラレイヤー
- サービス層
- リポジトリレイヤー

コントローラ層は、ユーザー要求を処理し、適切な応答を生成する役割を果たします。サービス層はビジネスロジックを担当します。ストレージ層はデータアクセスを担当します。

次の図は、3つの層間の関係を示しています。

![スプリングブートMVC](https://miro.medium.com/max/875/1*tYH4i0zAj7zQLxB7-tscKg.png)

Spring Boot MVCアプリケーションでは、コントローラは通常Spring @RestControllerです。サービス層は通常Spring @Serviceです。リポジトリ階層は通常Spring @Repositoryです。

次のコードスニペットは、コントローラ、サービス、リポジトリにコメントを追加する方法を示しています。

```java
@RestController
public class HelloController {

    @RequestMapping("/hello")
    public String hello() {
        return "Hello, world!";
    }
}
```

```java
@Service
public class HelloService {

    public String getHelloMessage() {
        return "Hello, world!";
    }
}
```

```java
@Repository
public class HelloRepository {

    public String getHelloMessage() {
        return "Hello, world!";
    }
}
```

##結論

MVC パターンは、アプリケーションをモデル、ビュー、コントローラの 3 つの主要な論理コンポーネントに分割する、広く使用されているソフトウェア設計パターンです。

Spring MVCアプリケーションでは、コントローラはユーザー要求を処理し、適切な応答を生成する役割を果たします。ビューはユーザーに応答をレンダリングする役割を果たします。モデルは、ビューに表示するデータを格納するデータ構造です。

MVCパターンには次の利点があります。

- アプリケーションの問題を分離し、コードベースのメンテナンスとテストを容易にします。
- アプリケーションを簡単に拡張できます。
- アプリケーションに新機能を簡単に追加できます。

##リファレンス

- [モデルビューコントローラー](https://en.wikipedia.org/wiki/Model–view–controller)
- [Spring MVC]（https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc）
- [Spring Boot MVC]（https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-spring-mvc.html）