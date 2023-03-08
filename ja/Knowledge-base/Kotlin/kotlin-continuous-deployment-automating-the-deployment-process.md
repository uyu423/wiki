---
title: Kotlin 継続的デプロイ: デプロイ プロセスの自動化
description: 
published: true
date: 2023-01-31T21:36:42.734Z
tags: 
editor: markdown
dateCreated: 2023-01-31T21:36:41.113Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Kotlin Continuous Deployment: Automating the Deployment Process***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-continuous-deployment-automating-the-deployment-process)
{.links-list}



#Kotlin継続的展開：展開プロセスの自動化

開発者は常にソフトウェア開発プロセスを自動化する方法を探しています。ソフトウェア開発で最も重要で時間のかかる作業の1つは展開です。デプロイメントは、ローカル開発環境からコードを取得して本番環境にプッシュするプロセスです。このプロセスは手動でも自動でもかまいません。

展開プロセスを自動化することには多くの利点があります。展開を自動化すると、時間を節約し、一貫性を向上させ、人的エラーの可能性を減らすことができます。この記事では、Kotlinを使用して展開プロセスを自動化する方法に焦点を当てます。

##なぜコトリンですか？

Kotlinは、Java Virtual Machine（JVM）で実行される静的に型指定されたプログラミング言語です。 KotlinはJavaと100％相互運用可能なので、Javaに慣れている開発者にとって魅力的なオプションです。 Kotlinは簡潔な言語でも、読みやすくメンテナンスが容易なコードにつながる可能性があります。

## Kotlinプロジェクトの設定

展開プロセスの自動化を開始するには、まずKotlinプロジェクトを設定する必要があります。私たちはGradleビルドツールを使用してプロジェクトの依存関係を管理し、プロジェクトをビルドします。

プロジェクトのルートディレクトリに `build.gradle.kts`というファイルを作成する必要があります。 `build.gradle.kts`ファイルはGradleビルドを設定するために使用されます。

```kotlin
plugins {
    id("org.jetbrains.kotlin.jvm") version "1.3.72"
}

group="com.example"
version="0.0.1"

repositories {
    jcenter()
}

dependencies {
    implementation("org.jetbrains.kotlin:kotlin-stdlib-jdk8")
}

tasks.withType<org.jetbrains.kotlin.gradle.tasks.KotlinCompile> {
    kotlinOptions.jvmTarget = "1.8"
}
```

`build.gradle.kts`ファイルは`build.gradle`ファイルと似ていますが、Kotlinで書かれています。 `build.gradle.kts`ファイルでKotlinプログラミング言語用のプラグインを定義し、使用するKotlinのバージョンを指定しました。また、プロジェクトのグループとバージョンも定義しました。

また、プロジェクトの依存関係が解決されるリポジトリも定義しました。この場合、JCenterリポジトリを使用しています。最後に、Kotlin標準ライブラリへの依存関係を定義しました。

Kotlin標準ライブラリは、Kotlinアプリケーションの開発に必要な一連のコアライブラリを提供します。また、プロジェクトをJava 8用にコンパイルするように指定しました。

## デプロイプロセスの自動化

これでKotlinプロジェクトが設定されたので、展開プロセスの自動化を開始できます。 Gradleビルドツールを使用して展開プロセスを自動化します。

最初にすべきことは、プロジェクトのルートディレクトリに `deploy.gradle`というファイルを作成することです。 `deploy.gradle`ファイルには、デプロイプロセスの設定が含まれています。

```kotlin
plugins {
    id("com.bmuschko.gradle.plugins.tooling-api") version "2.3.3"
}

apply(plugin = "com.bmuschko.tomcat")

group="com.example"
version="0.0.1"

repositories {
    jcenter()
}

dependencies {
    tomcat "org.apache.tomcat.embed:tomcat-embed-core:9.0.33"
    tomcat "org.apache.tomcat.embed:tomcat-embed-logging-juli:9.0.33"
    tomcat "org.apache.tomcat.embed:tomcat-embed-jasper:9.0.33"
}

tomcat {
    httpPort = 8080
    ajpPort = 8009
    enableSSL = false
    keystoreFile = file("src/main/resources/keystore.jks")
    keystorePass="secret"
    keyAlias = "tomcat"
}

tasks.withType<org.jetbrains.kotlin.gradle.tasks.KotlinCompile> {
    kotlinOptions.jvmTarget = "1.8"
}
```

`deploy.gradle`ファイルでTomcat Webサーバー用のプラグインを定義しました。また、プロジェクトのグループとバージョンも指定しました。

また、プロジェクトの依存関係が解決されるリポジトリも定義しました。この場合、JCenterリポジトリを使用しています。最後に、Tomcatライブラリへの依存関係を定義しました。

Tomcatライブラリは、KotlinアプリケーションをTomcat Webサーバーにデプロイするために必要です。 TomcatがHTTP要求をリッスンするために使用する必要があるポートも指定しました。

TomcatがAJP要求をリッスンするために使用する必要があるポートも指定しました。 AJPは、Webサーバーとアプリケーションサーバー間の通信に使用されるプロトコルです。また、アプリケーションでSSLを無効にすることを指定しました。

最後に、キーストアファイルの場所とキーストアのパスワードを指定しました。キーストアは、データを暗号化および復号化するために使用される暗号化キーを含むファイルです。

## アプリケーションのデプロイ

これでデプロイプロセスが自動化され、アプリケーションをデプロイできます。 Gradle Tomcatプラグインを使用してアプリケーションをデプロイします。

アプリケーションをデプロイするには、`gradle tomcatRun`コマンドを実行する必要があります。このコマンドはTomcat Webサーバーを起動し、ここにアプリケーションをデプロイします。

Tomcat Webサーバーが起動すると、http://localhost：8080からアプリケーションにアクセスできます。