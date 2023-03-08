---
title: VisualVM を使用した Spring Boot プロファイリング
description: 
published: true
date: 2023-01-31T20:57:39.329Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:57:35.630Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Spring Boot Profiling with VisualVM***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-profiling-with-visualvm)
{.links-list}



# VisualVMを使用したSpringブートプロファイリング

Spring Bootは、マイクロサービスやその他のプロダクショングレードアプリケーションを構築するための優れたフレームワークです。 Spring Bootを使用する利点の1つは、Tomcatサーバーが含まれているため、アプリケーションをスタンドアロンjarとして簡単にデプロイできることです。

しかし、組み込みサーバーを使用する際の欠点の1つは、パフォーマンスの問題を解決するのが難しいことです。この記事では、VisualVMを使用してSpring Bootアプリケーションをプロファイリングする方法について説明します。

## VisualVMとは？

VisualVMは、Javaアプリケーションに関する詳細情報を表示するためのグラフィカルインタフェースを提供するツールです。 JVMで実行されているアプリケーションを監視し、問題を解決するために使用できます。

## VisualVMのインストール

VisualVMはOracle JDKに含まれているため、JDKがインストールされている場合はすでにVisualVMが存在します。 JDKがインストールされていない場合は、[Oracle Webサイト]（https://www.oracle.com/java/technologies/visualvm.html）からVisualVMをダウンロードできます。

## Spring Bootアプリケーションのプロファイリング

VisualVMをインストールしたので、Spring Bootアプリケーションをプロファイリングする方法を見てみましょう。

まず、Spring Bootアプリケーションを起動する必要があります。この例では、[Spring PetClinic]（https://github.com/spring-projects/spring-petclinic）サンプルアプリケーションを使用します。

アプリケーションが実行されたら、VisualVMを開き、実行中のアプリケーションに接続できます。これを行うには、「ファイル」メニューをクリックして「JMX接続の追加」を選択します。

![VisualVM JMX接続の追加](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-add-jmx-connection.png)

[JMX接続の追加]ダイアログボックスで、実行しているアプリケーションのホストとポートを入力します。デフォルトホストは「localhost」、デフォルトポートは「1099」です。

![VisualVM JMX接続の追加ダイアログ]（https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-add-jmx-connection-dialog.png）

実行中のアプリケーションに接続するには、[OK]をクリックします。

VisualVMが実行されているアプリケーションに接続したら、[アプリケーション]タブにアプリケーションを表示する必要があります。

![VisualVM アプリケーションタブ] (https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-applications-tab.png)

アプリケーションのプロファイリングを開始するには、[アプリケーション]タブでアプリケーションを選択し、[プロファイル]ボタンをクリックします。

![VisualVMプロファイルボタン](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-profile-button.png)

「プロファイルアプリケーション」ダイアログで「CPU」プロファイリングタイプを選択し、「開始」をクリックします。

![VisualVMプロファイルアプリケーションダイアログ]（https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-profile-application-dialog.png）

プロファイリングセッションが開始されたら、VisualVMを使用してスレッドアクティビティ、メモリ使用量、および実行中のアプリケーションに関するその他の情報を表示できます。

![VisualVM モニタータブ] (https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-monitor-tab.png)

アプリケーションのプロファイリングが完了したら、「ファイル」メニューを選択し、「終了」を選択してプロファイリングセッションを停止できます。

##結論

この記事では、VisualVMを使用してSpring Bootアプリケーションをプロファイリングする方法について説明しました。 VisualVMは、Spring Bootアプリケーションのパフォーマンスの問題を解決するために使用できる強力なツールです。