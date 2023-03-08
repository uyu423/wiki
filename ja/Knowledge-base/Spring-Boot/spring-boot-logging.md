---
title: Spring Boot ロギング
description: 
published: true
date: 2023-02-01T02:17:22.389Z
tags: 
editor: markdown
dateCreated: 2023-02-01T02:17:20.844Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Spring Boot Logging***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-logging)
{.links-list}



#Spring Boot Logging

Spring Bootを使用すると、アプリケーションのロギングを簡単に設定できます。デフォルトでは、Spring Bootは `java.util.logging`（JUL）ロギングフレームワークを使用するようにアプリケーションを設定します。プロジェクトに適切なスタータ依存関係を追加して、Log4j2、Logback、またはslf4jを使用するように変更できます。

この記事では、Spring Bootでロギングを設定する方法について説明します。基本的な例から始めて、詳細項目に移動します。

## 基本設定

Spring Bootでロギングを設定する最も簡単な方法は、 `application.properties`ファイルに `logging.level`属性を追加することです。ロギングレベルは、特定のパッケージまたは特定のロガーに対して設定できます。たとえば、次の設定はパッケージ `com.example` のロギングレベルを `DEBUG` に設定します。

```
logging.level.com.example=DEBUG
```

すべてのパッケージのロギングレベルを設定するには、 `root`ロガーを使用できます。たとえば、次の設定では、すべてのパッケージのロギングレベルを 'INFO'に設定します。

```
logging.level.root=INFO
```

##ロガー

ロギングレベルの設定に加えて、ログ出力形式を設定することもできます。デフォルトでは、Spring Bootは `%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n` 形式でログメッセージを出力します。

`logging.pattern.console`属性を設定してフォーマットを変更できます。たとえば、次の設定では、ログメッセージを `%d [%thread] %-5level %logger{36} - %msg%n` 形式で出力します。

```
logging.pattern.console=%d [%thread] %-5level %logger{36} - %msg%n
```

##アフェンダー

コンソールに加えて、Spring Bootはファイルにログインすることもできます。デフォルトでは、ログメッセージは `tmp`ディレクトリの `spring.log`ファイルに出力されます。 `logging.file`属性を設定してファイルの場所を変更できます。たとえば、次の設定はログメッセージを `/var/log/spring.log` ファイルに出力します。

```
logging.file=/var/log/spring.log
```

##カスタムロガー

カスタムロガーを作成するには、 `logging.config`属性を使用してlog4j2.xmlファイルの場所を指定できます。たとえば、次の設定はログメッセージを `/var/log/spring.log` ファイルに出力します。

```
logging.config=log4j2.xml
```

## 高度な設定

基本設定に加えて、Spring Bootはいくつかの高度な機能を提供します。たとえば、ログメッセージを複数のファイルに出力するようにロガーを設定できます。特定のクラスのログレベルを設定することもできます。

## 複数のファイルへのロギング

`logging.file.name`と`logging.file.max-size`属性を設定して、ログメッセージを複数のファイルに出力するようにロガーを設定できます。たとえば、次の設定は `tmp` ディレクトリの `spring.log` と `spring.log.1` ファイルにログメッセージを出力します。

```
logging.file.name=spring.log
logging.file.max-size=10MB
```

## クラスのロギングレベル

`logging.level.{class}`属性を設定して、特定のクラスのロギングレベルを設定できます。たとえば、次の設定はクラス `com.example.MyClass` のロギングレベルを `DEBUG` に設定します。

```
logging.level.com.example.MyClass=DEBUG
```

##結論

この記事では、Spring Bootでロギングを設定する方法について説明しました。ロギングレベルを設定する方法とログ出力形式を変更する方法を見てきました。また、複数のファイルにログメッセージを出力する方法と、特定のクラスのロギングレベルを設定する方法についても説明しました。