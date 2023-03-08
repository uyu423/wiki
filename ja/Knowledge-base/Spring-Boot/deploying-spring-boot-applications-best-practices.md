---
title: Spring Boot アプリケーションのデプロイ: ベスト プラクティス
description: 
published: true
date: 2023-02-17T18:02:43.635Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:59:25.894Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Deploying Spring Boot Applications: Best Practices***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/deploying-spring-boot-applications-best-practices)
{.links-list}
 


# Spring Boot アプリケーションのデプロイ: ベスト プラクティス

Spring Boot は、プロダクション グレードのスタンドアロンの Spring ベース アプリケーションを簡単に作成できる、人気のある Java Web フレームワークです。この記事では、Spring Boot アプリケーションをデプロイするためのベスト プラクティスのいくつかについて説明します。

＃＃ 目次

1. [Spring Boot アプリケーションの作成](#creating-a-spring-boot-application)
2. [Spring Boot アプリケーションのデプロイ](#deploying-a-spring-boot-application)
    1. [アーキテクチャ](#アーキテクチャ)
    2. [ウェブサーバー](#web-servers)
3. [結論](#結論)

## Spring Boot アプリケーションの作成

Spring Boot アプリケーションの作成は簡単です。必要なのは、Java とテキスト エディターだけです。 Spring Boot アプリケーションは通常、jar ファイルとしてパッケージ化され、「java -jar」コマンドを使用して実行できます。たとえば、次のコマンドは、ポート 8080 で実行されている Spring Boot アプリケーションを開始します。

ジャバ
java -jar my-spring-boot-app.jar
```java
java -jar my-spring-boot-app.jar
```
mvn spring-boot:run
```

Spring Initializr を使用して Spring Boot アプリケーションを作成することもできます。 Spring Initializr は、選択に基づいて Spring Boot アプリケーションを生成できる Web アプリケーションです。必要な依存関係を選択するだけで、Initializr はそれらの依存関係を持つプロジェクトを生成します。

## Spring Boot アプリケーションのデプロイ

Spring Boot アプリケーションのデプロイは簡単です。従来の Java Web アプリケーションとは異なり、サーブレット コンテナーやアプリケーション サーバーを構成する必要はありません。ただし、Spring Boot アプリケーションをデプロイする際に留意すべき点がいくつかあります。

＃＃＃ 建築

Spring Boot アプリケーションは通常、スタンドアロンの jar ファイルとしてデプロイされます。これにより、Java をサポートする任意のプラットフォームで Spring Boot アプリケーションを簡単にデプロイして実行できます。

Spring Boot アプリケーションは、war ファイルとしてデプロイすることもできます。ただし、アプリケーションを実行するにはサーブレット コンテナーまたはアプリケーション サーバーが必要になるため、これは推奨される展開方法ではありません。

### ウェブサーバー

Spring Boot アプリケーションは、さまざまな Web サーバーにデプロイできます。最も一般的なオプションは、Apache Tomcat と Jetty です。

Tomcat は、Java アプリケーションで最も広く使用されている Web サーバーです。 Tomcat はサーブレット コンテナーであり、War ファイルを実行できます。 Tomcat は、スタンドアロン サーバーと組み込み可能なサーブレット コンテナーの両方として利用できます。

Jetty は、広く使用されているオープン ソース Web サーバーです。 Jetty はサーブレット コンテナーであり、War ファイルを実行できます。 Jetty は、スタンドアロン サーバーと組み込み可能なサーブレット コンテナーの両方として利用できます。

＃＃ 結論

Spring Boot アプリケーションのデプロイは簡単です。 Spring Boot アプリケーションは、さまざまな Web サーバーにデプロイでき、サーブレット コンテナーやアプリケーション サーバーを必要としません。