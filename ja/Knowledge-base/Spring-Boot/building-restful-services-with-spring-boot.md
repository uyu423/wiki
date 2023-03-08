---
title: Spring Boot を使用した RESTful サービスの構築
description: 
published: true
date: 2023-01-31T16:38:08.935Z
tags: 
editor: markdown
dateCreated: 2023-01-31T16:38:07.201Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Building RESTful Services with Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/building-restful-services-with-spring-boot)
{.links-list}


# Spring BootでRESTfulサービスを構築する

この記事では、Spring BootでRESTful Webサービスを構築するためのいくつかのベストプラクティスについて説明します。

次のトピックを扱います。

* REST APIの設計
* RESTfulエンドポイント設計のためのベストプラクティス
* Spring BootによるREST APIの実装
*REST APIテスト
*REST APIセキュリティ

## REST APIの設計

REST APIを設計するときは、次の要素を考慮することが重要です。

* APIが公開するリソース
*そのリソースでできること
*リソース間の関係

APIは、開発者が簡単に使用できるように設計する必要があります。理解し、使いやすく、一貫性があるはずです。

APIのエンドポイントを設計するときは、一貫した命名規則を使用する必要があります。たとえば、次のルールを使用できます。

```
/{resource}/{id}
```

ここで、{resource}はリソースの名前、{id}はリソースの識別子です。

一貫した方法でHTTPメソッドを使用するのも良い考えです。たとえば、次のルールを使用できます。

```
GET /{resource}/{id}
POST /{resource}
PUT /{resource}/{id}
DELETE /{resource}/{id}
```

ここで、GETはリソースの取得に使用され、POSTはリソースの作成に使用され、PUTはリソースの更新に使用され、DELETEはリソースの削除に使用されます。

## RESTfulエンドポイント設計のベストプラクティス

API用のエンドポイントを設計するときに念頭に置くべきいくつかのベストプラクティスがあります。

* リソースの複数名の使用
*ハイフンを使用して単語を区切る
*小文字の使用
*一貫した方法でHTTPメソッドを使用する
*一貫した方法でHTTPステータスコードを使用する

## Spring BootでREST APIを実装する

REST APIを設計するためのいくつかのベストプラクティスを取り上げたので、Spring BootでREST APIを実装する方法を見てみましょう。

Spring Bootを使用すると、「単に実行」できるスタンドアロンのプロダクションクラスSpringベースのアプリケーションを簡単に作成できます。 Spring Bootを使用して単一のリソースを公開する単純なAPIを作成します。

### 依存関係

まず、プロジェクトに次の依存関係を追加する必要があります。

*spring-boot-starter-data-rest
* spring-boot-starter-data-jpa
*スプリングブートスターターウェブ

### エンティティ

エンティティを作成することから始めましょう。エンティティ名に次の規則を使用します。

```
{resource}_{operation}
```

ここで、{resource}はリソースの名前、{operation}はリソースで実行されている操作です。

この例では、`user_create`というエンティティを作成します。

```java
@Entity
@Table(name = "user_create")
public class UserCreate {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "name")
    private String name;

    @Column(name = "email")
    private String email;

    // ゲッターとセッター
}
```

###リポジトリ

次に、エンティティのリポジトリを作成します。リポジトリ名には次の規則を使用します。

```
{resource}Repository
```

ここで {resource} はリソースの名前です。

この例では、`UserCreateRepository`というリポジトリを作成します。

```java
public interface UserCreateRepository extends JpaRepository<UserCreate, Long> {

}
```

###サービス

次に、エンティティのサービスを作成します。サービス名に次の規則を使用します。

```
{resource}Service
```

ここで {resource} はリソースの名前です。

この例では、`UserCreateService`というサービスを作成します。

```java
@Service
public class UserCreateService {

    @Autowired
    private UserCreateRepository userCreateRepository;

    public UserCreate create(UserCreate userCreate) {
        return userCreateRepository.save(userCreate);
    }
}
```

###コントローラ

最後に、エンティティ用のコントローラを作成します。コントローラ名に次の規則を使用します。

```
{resource}Controller
```

ここで {resource} はリソースの名前です。

この例では、`UserCreateController`というコントローラを作成します。

```java
@RestController
@RequestMapping("/user-creates")
public class UserCreateController {

    @Autowired
    private UserCreateService userCreateService;

    @PostMapping
    public UserCreate create(@RequestBody UserCreate userCreate) {
        return userCreateService.create（userCreate）;
    }
}
```

これがSpring Bootで簡単なREST APIを生成するために必要なすべてです。

## REST APIテスト

REST APIをテストするときに念頭に置いておくべきことがいくつかあります。

*エンドポイントにアクセスできる必要があります。
*エンドポイントは予想データを返す必要があります。
*エンドポイントは予想されるHTTPステータスコードを返す必要があります。

サンプルAPIをテストするには、次のcurlコマンドを使用できます。

```
#create a user
curl -X POST -H "Content-Type: application/json" -d '{"name":"John Doe","email":"john.doe@example.com"}' http://localhost:8080 /user-creates

#get a user
curl -X GET http://localhost:8080/user-creates/1

#update a user
curl -X PUT -H "Content-Type: application/json" -d '{"name":"John Doe","email":"john.doe@example.com"}' http://localhost:8080 /user-creates/1

#delete a user
curl -X DELETE http://localhost:8080/user-creates/1
```

## REST APIセキュリティ

REST APIを保護する際に留意する必要があることがいくつかあります。

*認証
*承認
*速度制限

認証は、ユーザーのIDを確認するプロセスです。許可は、ユーザーが実行できる操作を決定するプロセスです。レート制限は、ユーザーが作成できる要求の数を制限するプロセスです。

REST APIを保護する方法はいくつかありますが、最も広く使用されている方法の1つはJWT（JSON Webトークン）を使用することです。

JWTでサンプルAPIを保護するには、次のcurlコマンドを使用できます。

```
#login
curl -X POST -H "Content-Type: application/json" -d '{"username":"john.doe","password":"password"}' http://localhost:8080/auth/login

#get a user
curl -X GET -H "Authorization: Bearer <token>" http://localhost:8080/user-creates/1

#logout
curl -X POST -H "Authorization: Bearer <token>" http://localhost:8080/auth/logout
```

##結論

この記事では、Spring BootでRESTful Webサービスを構築するためのいくつかのベストプラクティスについて説明しました。 REST APIを設計する方法、Spring BootでREST APIを実装する方法、REST APIをテストする方法、およびREST APIを保護する方法について説明しました。