---
title: Spring Boot DevTools: 開発の合理化
description: 
published: true
date: 2023-02-01T04:57:32.965Z
tags: 
editor: markdown
dateCreated: 2023-02-01T04:57:29.168Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Spring Boot DevTools: Streamlining Development***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-devtools-streamlining-development)
{.links-list}



#Spring Boot DevTools：開発の合理化

Spring Boot DevToolsは、Spring Bootアプリケーションで作業するときに開発環境を改善するために使用できる一連のツールを提供します。これらのツールを使用して、アプリケーションをすばやく再起動し、静的リソースをリアルタイムで再ロードし、他の多くの開発関連タスクを実行できます。

この記事では、Spring Boot DevToolsを使用して開発プロセスを簡素化する方法について説明します。また、DevToolsが提供する他の機能のいくつかを見てみましょう。

##クイック再起動

DevToolsの最も便利な機能の1つは、アプリケーションをすばやく再起動する機能です。アプリケーションの実行中に「R」キーを押すだけです。

DevTools はコードに対するすべての変更を自動的に検出し、アプリケーションを再起動します。つまり、変更するたびにアプリケーションを手動で停止して起動する必要はありません。

##ライブリロード

DevTools のもう一つの便利な機能はリアルタイムリロードです。この機能は、HTML、CSS、JavaScriptなどの静的リソースが変更されたときに自動的にリロードするために使用できます。

ライブリロードを使用するには、まず `pom.xml`ファイルに次の依存関係を追加する必要があります。

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-devtools</artifactId>
  <optional>true</optional>
</dependency>
```

その後、 `application.properties`ファイルに次の属性を追加してリアルタイムリロードを有効にできます。

``properties
spring.devtools.livereload.enabled=true
```

##リモート開発

DevToolsは、Spring Bootアプリケーションをリモートでデバッグして開発する機能も提供します。これは、 `application.properties`ファイルに次の属性を追加することによって行うことができます。

``properties
spring.devtools.remote.secret=<secret>
```

`<秘密>`を選択した秘密に置き換えます。この秘密は、着信要求を認証するために使用されます。

完了したら、次のコマンドを使用してデバッグモードでアプリケーションを起動できます。

```
$ mvn spring-boot:run -Dspring-boot.run.jvmArguments='-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5005'
```

これにより、デバッグモードでアプリケーションが起動し、ポート5005でリッスンします。その後、EclipseやVisual Studio Codeなどのリモートデバッガを使用してアプリケーションに接続できます。

##結論

この記事では、Spring Boot DevToolsを使用して開発プロセスを簡素化する方法について説明しました。 DevToolsが提供する他の機能のいくつかも見てきました。

開発環境を改善したい場合は、DevToolsをチェックしてみてください。