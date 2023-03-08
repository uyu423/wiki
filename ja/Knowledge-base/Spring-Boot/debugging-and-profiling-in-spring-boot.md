---
title: Spring Boot でのデバッグとプロファイリング
description: 
published: true
date: 2023-02-17T18:02:51.783Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:24:04.895Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Debugging and Profiling in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/debugging-and-profiling-in-spring-boot)
{.links-list}



# Spring Bootでのデバッグとプロファイリング

ソフトウェア開発は困難で時間がかかる場合があります。プロセスをできるだけスムーズにするのに役立つツールを用意することが重要です。この記事では、デバッグとプロファイリングの2つのツールを見てみましょう。

デバッグは、ソフトウェアのエラーを見つけて修正するプロセスです。コードとデータの両方でエラーを見つけるために使用できます。プロファイリングは、ソフトウェアを最適化するために使用できるテクノロジです。ボトルネックを見つけ、パフォーマンスを向上させるために使用できます。

Spring Bootは、Webアプリケーションの開発に広く使用されているフレームワークです。 「単に実行」できるスタンドアロンのプロダクションクラスSpringベースのアプリケーションを簡単に作成できます。また、デバッグとプロファイリングに役立つさまざまなツールを提供しています。

## Spring Bootアプリケーションのデバッグ

Spring Bootアプリケーションをデバッグする方法はいくつかあります。このセクションでは、最も人気のある2つのspring-boot-devtoolsモジュールの使用方法とリモートデバッグの使用方法について説明します。

### spring-boot-devtools モジュールの使用

spring-boot-devtoolsモジュールを使用してデバッグ環境を改善できます。自動再起動、ライブリロード、リモートデバッグなどの機能を提供します。

spring-boot-devtoolsモジュールを使用するには、プロジェクトに依存関係として追加します。

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
  </dependency>
</dependencies>
```

これを完了したら、application.propertiesファイルに次の属性を追加してモジュールの機能を有効にできます。

```
spring.devtools.restart.enabled=true
spring.devtools.livereload.enabled=true
spring.devtools.remote.debug.local=false
```

最初の属性 spring.devtools.restart.enabled は自動再起動機能を有効にします。この機能は、クラスパスのファイルが変更されるとアプリケーションを自動的に再起動します。 2番目の属性、spring.devtools.livereload.enabledは、リアルタイムリロード機能を有効にします。この機能は、アプリケーションを再起動せずに変更されたリソースを再ロードします。

3 番目の属性 spring.devtools.remote.debug.local はリモートデバッグを有効にします。この機能により、リモートIDEでアプリケーションをデバッグできます。この機能を使用するには、プロパティ値をtrueに設定し、次のプロパティを追加する必要があります。

```
spring.devtools.remote.debug.port=8000
```

このプロパティは、リモートデバッグに使用するポートを設定します。これを完了すると、デバッグモードでアプリケーションを起動できます。 IntelliJ IDEAでは、[実行] - > [構成の編集]に移動してこれを実行できます。設定の編集ダイアログボックスで+ボタンをクリックし、リモートを選択します。 [リモート設定]ダイアログボックスで、ポートを8000に設定して[適用]をクリックします。

IntelliJ IDEAでアプリケーションをデバッグできるようになりました。これを行うには、デバッグツールウィンドウを開き、+ボタンをクリックします。 「構成の追加」ダイアログ・ボックスで「リモート」を選択し、「OK」をクリックします。 [リモート設定]ダイアログボックスで、ポートを8000に設定し、[デバッグ]をクリックします。

### リモートデバッグを有効にする

別のIDEを使用している場合は、リモートデバッグを引き続き使用できます。これを行うには、デバッグモードでアプリケーションを起動し、デバッグに使用するポートを指定する必要があります。 IntelliJ IDEAでは、[実行] - > [構成の編集]に移動してこれを実行できます。設定の編集ダイアログボックスで+ボタンをクリックし、リモートを選択します。 [リモート設定]ダイアログボックスで、ポートを8000に設定して[適用]をクリックします。

IntelliJ IDEAでアプリケーションをデバッグできるようになりました。これを行うには、デバッグツールウィンドウを開き、+ボタンをクリックします。 [構成の追加]ダイアログボックスで[リモート]を選択し、[OK]をクリックします。 [リモート設定]ダイアログボックスで、ポートを8000に設定し、[デバッグ]をクリックします。

## Spring Bootアプリケーションのプロファイリング

プロファイリングは、ソフトウェアを最適化するために使用できるテクノロジです。ボトルネックを見つけ、パフォーマンスを向上させるために使用できます。 Spring Bootアプリケーションをプロファイリングする方法はいくつかあります。このセクションでは、最も人気のある2つの方法、Spring Boot Actuatorの使用とJProfilerの使用について説明します。

### スプリングブートアクチュエータの使用

Spring Boot Actuatorは、Spring Bootアプリケーションを監視および管理するために使用できる一連のツールです。 Webインターフェイス、アプリケーションの監視と管理のためのエンドポイント、プロファイリング情報の収集のためのツールセットなど、さまざまな機能を提供します。

Spring Boot Actuatorを使用するには、プロジェクトに依存関係として追加します。

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
  </dependency>
</dependencies>
```

完了したら、http://localhost:8080/actuator にアクセスして Web インターフェイスにアクセスできます。 Webインターフェースは、アプリケーションを監視および管理するためのさまざまなツールを提供します。また、プロファイリング情報を収集するための一連のツールも提供します。

プロファイリングツールを使用するには、application.propertiesファイルに次の属性を追加する必要があります。

```
management.endpoints.web.exposure.include=*
```

このプロパティはアクチュエータのすべてのエンドポイントを公開します。完了すると、/ profilerエンドポイントにアクセスできます。このエンドポイントを使用すると、プロファイリング情報を収集して表示できます。

### JProfilerの使用

JProfilerはJavaプロファイリングツールです。スレッド情報、メモリ情報、SQL情報など、さまざまな種類の情報を収集するために使用できます。また、呼び出しツリービュー、ホットスポットビュー、ライブメモリビューなど、さまざまなビューを提供します。

JProfilerを使用するには、JProfilerをインストールしてプロジェクトに依存関係として追加する必要があります。 JProfiler Webサイトにアクセスして最新バージョンをダウンロードしてください。これを完了したら、プロジェクトに依存関係として追加できます。

```xml
<dependencies>
  <dependency>
    <groupId>org.jprofiler</groupId>
    <artifactId>jprofiler</artifactId>
    <version> 11.0.2 </version>
  </dependency>
</dependencies>
```

完了したら、プロファイルモードでアプリケーションを起動できます。 IntelliJ IDEAでは、[実行] - > [構成の編集]に移動してこれを実行できます。設定の編集ダイアログボックスで+ボタンをクリックし、プロファイルを選択します。 「プロファイル構成」ダイアログ・ボックスで「JProfiler」オプションを選択し、「適用」をクリックします。

IntelliJ IDEAでアプリケーションをプロファイリングできるようになりました。これを行うには、プロファイルツールウィンドウを開き、使用するプロファイリングセッションを選択します。セッションで収集するデータと使用するビューを選択できます。