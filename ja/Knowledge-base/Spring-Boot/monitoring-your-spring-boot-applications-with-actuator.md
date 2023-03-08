---
title: アクチュエーターを使用した Spring Boot アプリケーションのモニタリング
description: 
published: true
date: 2023-02-17T18:02:49.105Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:16:13.719Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Monitoring Your Spring Boot Applications with Actuator***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/monitoring-your-spring-boot-applications-with-actuator)
{.links-list}


# アクチュエーターを使用した Spring Boot アプリケーションのモニタリング

監視はあらゆるアプリケーションの重要な側面であり、Spring Boot は、アクチュエーターを使用してアプリケーションを監視する簡単な方法を提供します。 Actuator は、さまざまな監視および管理エンドポイントを提供する Spring Boot モジュールです。この記事では、Actuator を使用して Spring Boot アプリケーションを監視する方法を見ていきます。

## アクチュエータ エンドポイントの有効化

Actuator を使用するには、「spring-boot-actuator」依存関係をプロジェクトに追加する必要があります。この依存関係を `pom.xml` ファイルに追加できます。

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-actuator</artifactId>
  <version>2.1.2.RELEASE</version>
</dependency>
```

依存関係を追加したら、`@EnableActuator` アノテーションを `@SpringBootApplication` クラスに追加して、アクチュエータ エンドポイントを有効にできます。

ジャバ
@SpringBootアプリケーション
@EnableActuator
パブリック クラス アプリケーション {

  public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
  }
}
```java
@SpringBootApplication
@EnableActuator
public class Application {

  public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
  }
}
```

### アプリケーションの指標を監視する

`metrics` エンドポイントは、アプリケーションのメトリックに関する情報を提供します。 `metrics` エンドポイントにアクセスするには、`http://localhost:8080/{context-path}/actuator/metrics` に移動します。

`metrics` エンドポイントは、アプリケーションのメトリックに関する情報を JSON 形式で返します。 JSON 形式には、次の情報が含まれています。

- `names`: メトリックの名前。
- `values`: メトリックの値。

以下は、`metrics` エンドポイント応答の例です。

json
{
  "名前": [
    "jvm.memory.max",
    「jvm.memory.used」
  ]、
  "値": {
    "jvm.memory.max":49989655552,
    "jvm.memory.used":3246466048
  }
}
```json
{
  "status": "UP",
  "details": {
    "diskSpace": {
      "status": "UP",
      "details": {
        "total":49989655552,
        "free":3246466048,
        "threshold":10485760
      }
    }
  }
}
```

## 結論

この記事では、Actuator を使用して Spring Boot アプリケーションを監視する方法について説明しました。 Actuator は、アプリケーションを監視するためのシンプルで強力な方法を提供します。 Actuator エンドポイントを使用すると、アプリケーションの正常性、メトリック、および構成に関する詳細情報を取得できます。