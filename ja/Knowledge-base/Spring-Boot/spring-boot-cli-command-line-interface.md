---
title: Spring Boot CLI コマンドライン インターフェイス
description: 
published: true
date: 2023-02-17T18:15:02.943Z
tags: 
editor: markdown
dateCreated: 2023-01-30T22:23:38.607Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Spring Boot CLI Command Line Interface***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-cli-command-line-interface)
{.links-list}



# Spring Boot CLIコマンドラインインタフェース

Spring Boot CLIは、Springベースのアプリケーションをすばやく構築するために使用されるコマンドラインインターフェイスです。必要なすべての依存関係を持つSpringプロジェクトを作成する簡単な方法を提供します。

Spring Boot CLIは、Springをすばやく起動して実行したい開発者にとって重要なツールです。この記事では、Spring Boot CLIを使用してSpringプロジェクトをすばやく作成する方法について説明します。また、Spring Boot CLIが提供するいくつかの機能についても説明します。

##はじめに

Spring Boot CLIを使用するには、次のものをインストールする必要があります。

* Java 8以上
* Apache Maven 3.3.9以上

次のコマンドを実行してインストールされていることを確認できます。

```
java -version
mvn -version
```

インストールされていない場合は、こちら（https://spring.io/guides/gs/getting-started-maven/）の指示に従うことができます。

インストールが完了したら、[このリンク]（https://repo.spring.io/release/org/springframework/boot/spring-boot-cli/2.3.1.RELEASE/にアクセスしてSpring Boot CLIをダウンロードできます。 . spring-boot-cli-2.3.1.RELEASE-bin.zip).

Spring Boot CLIをダウンロードしたら、解凍して `bin`ディレクトリを `PATH`に追加する必要があります。これにより、すべてのディレクトリで `spring` コマンドを実行できます。

## Springプロジェクトの作成

私はSpring Boot CLIをインストールしたので、それを使ってSpringプロジェクトを作成しましょう。 [Web]（https://start.spring.io/#dependencies=web）と[JPA]（https://start.spring.io/#dependencies=data-jpa）を使用するプロジェクトを作成します。依存関係。

これには `spring init` コマンドを使用します。このコマンドは、指定された依存関係を使用してSpringプロジェクトを作成します。 `-d`フラグは、プロジェクトに含める依存関係を指定するために使用されます。私たちの場合、WebとJPAの依存関係を含めたいと思います。また、[bootstrap]（https：//getbootstrap.com/）依存関係を使用したいことを示すために`-b`フラグを指定します。

```
spring init -d=web,data-jpa -b
```

これにより、次の構造で `my-project`というディレクトリが作成されます。

```
my-project
├── pom.xml
└── src
    ├── main
    │   ├── java
    │   │   └── com
    │   │   └── example
    │   │   └── myproject
    │   │   └── MyprojectApplication.java
    │   └── resources
    │   └── application.properties
    └── test
        └── java
            └── com
                └── example
                    └── myproject
                        └── MyprojectApplicationTests.java
```

`pom.xml`ファイルにはプロジェクトの依存関係が含まれています。 `src/main/java`ディレクトリにはプロジェクトのJavaソースコードが含まれています。 `src/test/java`ディレクトリにはプロジェクトのテストが含まれています。 `src/main/resources` ディレクトリには、プロパティファイルなどのプロジェクトリソースが含まれています。

## アプリケーションの実行

さて、Springプロジェクトができたので、実行して何をするのか見てみましょう。これには `spring run` コマンドを使用します。このコマンドはアプリケーションをコンパイルして実行します。

```
spring run src/main/java/com/example/myproject/MyprojectApplication.java
```

これにより、ポート8080でアプリケーションが起動します。 [http://localhost:8080](http://localhost:8080)にアクセスしてアプリケーションを表示できます。

## SpringBoot CLIコマンド

`spring run`コマンドはアプリケーションをすばやく実行するのに役立ちますが、Spring Boot CLIはさまざまなタスクに使用できる他の多くのコマンドを提供します。以下で最も役に立ついくつかのコマンドについて簡単に説明します。

### `スプリングブート`

`spring boot`コマンドを使って新しいSpring Bootアプリケーションを作成できます。このコマンドは、指定された依存関係を持つ新しいプロジェクトを作成します。これは、前のセクションでプロジェクトの作成に使用したのと同じコマンドです。

### `春の大掃除`

`spring clean`コマンドを使用してプロジェクトのビルドディレクトリをクリーンアップできます。これは、不要なコンパイル済みファイルやその他の成果物を削除したい場合に便利です。

### `スプリングラン`

`spring run`コマンドを使用してアプリケーションをコンパイルして実行できます。これは、前のセクションでアプリケーションの実行に使用したのと同じコマンドです。

### `スプリングテスト`

`spring test`コマンドを使用してプロジェクトのテストを実行できます。これは、アプリケーションが正しく動作することを確認するのに役立ちます。

### `スプリングジャー`

`spring jar`コマンドを使用してアプリケーションをJARファイルにパッケージ化できます。これは、アプリケーションをサーバーにデプロイするのに役立ちます。

### `春の戦争`

`spring war`コマンドを使用してアプリケーションをWARファイルにパッケージ化できます。これは、アプリケーションをサーバーにデプロイするのに役立ちます。

### `春ヘルプ`

`spring help`コマンドを使用して、利用可能なすべてのコマンドのリストを表示できます。これは、利用可能なすべてのコマンドの簡単な概要を得るのに役立ちます。

##結論

この記事では、Spring Boot CLIを使用してSpringベースのアプリケーションをすばやく作成する方法について説明しました。また、Spring Boot CLIが提供する最も有用なコマンドのいくつかを扱いました。