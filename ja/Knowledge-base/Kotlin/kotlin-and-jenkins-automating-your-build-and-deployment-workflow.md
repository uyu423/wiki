---
title: Kotlin と Jenkins: ビルドとデプロイのワークフローを自動化する
description: 
published: true
date: 2023-01-31T16:24:40.994Z
tags: 
editor: markdown
dateCreated: 2023-01-31T16:24:39.380Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Kotlin and Jenkins: Automating Your Build and Deployment Workflow***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-jenkins-automating-your-build-and-deployment-workflow)
{.links-list}




Kotlinは、IntelliJ IDEA Java IDEを作成した会社であるJetBrainsによって作成されたJVMベースの言語です。コンパイラがコンテキストで変数の型を推論できることを意味する型推論機能を持つ静的に型指定された言語。 KotlinはJavaと完全に互換性があり、サーバー側、クライアント側、およびAndroid開発に使用できます。

Jenkinsは、連続連携（CI）および連続配信（CD）ワークフローでよく使用される一般的なオープンソース自動化サーバーです。 Kotlinアプリケーションのビルドおよびデプロイプロセスを自動化するために使用できます。

この記事では、CI / CD用のJenkinsでKotlinプロジェクトを設定する方法について説明します。ビルドおよびデプロイプロセスのデモンストレーションに使用できるサンプルKotlinアプリケーションも提供しています。

## Kotlinプロジェクトの設定

最初にすべきことは、Kotlinプロジェクトを作成することです。この例では、IntelliJ IDEA Kotlinプロジェクトテンプレートを使用しています。

IntelliJ IDEAを開き、「新規プロジェクトの作成」を選択します。 「Kotlin/JVM」プロジェクトタイプを選択し、「次へ」をクリックします。

![新しいプロジェクトを作成](https://i.imgur.com/EuYLb4z.png)

プロジェクトに名前を付け、プロジェクトファイルの場所を選択します。また、プロジェクトのJDKを選択する必要があります。 Kotlinと互換性のあるJDKバージョンを選択する必要があります。

![プロジェクト設定](https://i.imgur.com/fvYg4UO.png)

「完了」をクリックしてプロジェクトを作成します。

##サンプルKotlinアプリケーションの追加

これでKotlinプロジェクトがあるので、サンプルKotlinアプリケーションを追加できます。この例では、単純な「Hello、World!」アプリケーション。

次のコードを使用して、プロジェクトに新しいKotlinファイルを作成します。

```kotlin
fun main(args: Array<String>) {
    println("Hello, World!")
}
```

このコードは「Hello, World!」を印刷します。実行時にコンソールに。

## Jenkinsの設定

これでKotlinプロジェクトが設定されたので、CI / CDワークフロー用にJenkinsを設定できます。

KotlinプロジェクトにJenkinsを設定するために必要な作業はいくつかあります。

- Kotlinプラグインのインストール
- Jenkinsジョブの設定

### Kotlinプラグインのインストール

Jenkins用のKotlinプラグインは、Kotlinプロジェクトのビルドのサポートを追加します。プラグインをインストールするには、Jenkins Webインターフェイスの[プラグインの管理]ページに移動して[利用可能]タブを選択します。 「kotlin」を検索し、結果リストから「Kotlin Plugin」を選択します。プラグインをインストールするには、「再起動せずにインストール」をクリックします。

![コトリンプラグイン](https://i.imgur.com/GtLbC5z.png)

### Jenkinsジョブの設定

次に、Kotlinプロジェクト用のJenkinsジョブを作成する必要があります。これを行うには、Jenkins Webインターフェイスの「新しいアイテム」ページに移動して「フリースタイルプロジェクト」オプションを選択します。

![新しい項目](https://i.imgur.com/SVxH7jy.png)

ジョブ名を指定して「OK」を選択します。

[ジョブの構成]ページには、ジョブを設定するために実行する必要があるいくつかのタスクがあります。

- KotlinプロジェクトのGitリポジトリを追加
- Kotlinコードをコンパイルするビルドステップを追加する
- Kotlinアプリケーションを実行するためのビルドステップを追加する

#### Gitリポジトリの追加

「ソースコードの管理」セクションの「SCM」ドロップダウンメニューから「Git」を選択します。 [Repositories]フィールドにKotlinプロジェクトのGitリポジトリURLを入力します。

![scm-設定](https://i.imgur.com/Vkzc0jA.png)

#### Kotlinコードをコンパイルするビルドステップを追加する

「ビルド」セクションで「ビルドステップの追加」を選択し、オプションのリストから「Kotlinコンパイラの呼び出し」を選択します。

[ソースファイル]フィールドに、プロジェクトのKotlinソースファイルパスを入力します。 「Classpath」フィールドにKotlin標準ライブラリへのパスを入力します。

![ビルド設定](https://i.imgur.com/W0m7Ncu.png)

#### Kotlinアプリケーションを実行するためのビルドステップを追加する

「ビルド」セクションで「ビルドステップの追加」を選択し、オプションのリストから「コートされたスクリプトの実行」を選択します。

[スクリプト]フィールドに次のコードを入力します。

```kotlin
println("Hello, World!")
```

このコードは「Hello, World!」を印刷します。実行時にコンソールに。

![実行設定](https://i.imgur.com/O0PFY0z.png)

ジョブ構成を保存するには、「保存」をクリックします。

## Jenkinsジョブの実行

これでJenkinsを設定したので、タスクを実行できます。これを行うには、Jenkins Webインターフェイスの[今すぐビルド]ページに移動します。

![今ビルド](https://i.imgur.com/pVk4U0N.png)

ビルドプロセスを開始するには、「今すぐビルド」をクリックします。

ビルドが完了したら「Hello、World！」コンソール出力に印刷されたメッセージ。

![ビルド出力](https://i.imgur.com/Vkzc0jA.png)

##結論

この記事では、Jenkinsを使用してCI / CD用のKotlinプロジェクトを設定する方法について説明しました。ビルドおよびデプロイプロセスを実証するために使用できるサンプルKotlinアプリケーションも提供しました。