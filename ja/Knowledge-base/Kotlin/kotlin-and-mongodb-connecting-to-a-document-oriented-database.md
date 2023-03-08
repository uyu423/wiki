---
title: Kotlin と MongoDB: ドキュメント指向データベースへの接続
description: 
published: true
date: 2023-02-17T18:11:03.248Z
tags: 
editor: markdown
dateCreated: 2023-01-30T18:17:29.591Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Kotlin and MongoDB: Connecting to a Document-Oriented Database***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-mongodb-connecting-to-a-document-oriented-database)
{.links-list}

    
# KotlinとMongoDB：ドキュメント指向データベースに接続する

この記事では、KotlinからMongoDBデータベースに接続する方法について説明します。 MongoDBは、スキーマとともにJSONに似たドキュメントを使用するオープンソースのドキュメント指向のデータベースシステムです。 Webアプリケーションに広く使用されており、多くのKotlinアプリケーションにデータを保存するのにも適しています。

MongoDBのインストール方法を見てみましょう。次に、Kotlinプロジェクトを作成してMongoDBデータベースに接続します。 Kotlinでデータベースを照会する方法を見てみましょう。

## モンゴルDBのインストール

MongoDBは、Windows、MacOS、Linuxで利用できます。 [MongoDB Webサイト]（https://www.mongodb.com/download-center#community）からダウンロードできます。オペレーティングシステムと一致するバージョンをダウンロードします。

MongoDBをダウンロードしたら、アーカイブを解凍して目的の場所にコンテンツを抽出します。この記事では `C:\mongodb` に抽出します。

次に、MongoDB用のデータディレクトリを作成する必要があります。データディレクトリは、MongoDBがデータファイルを保存する場所です。 MongoDBインストールディレクトリに `data`という新しいディレクトリを作成します。

これでデータディレクトリがあるので、MongoDBを起動できます。ターミナルウィンドウを開き、MongoDBインストールディレクトリに移動します。次に、次のコマンドを実行します。

```
mongod --dbpath C:\mongodb\data
```

このコマンドはMongoDBサーバーを起動し、 `data`ディレクトリをデータディレクトリとして使用するように指示します。 MongoDBはバックグラウンドで実行されます。この端末ウィンドウは再び不要なので、開いたままにしたり閉じたりすることができます。

##コートリンプロジェクトの作成

これでKotlinアプリケーションの開発を開始する準備が整いました。このプロジェクトでは、[Gradle]（https://gradle.org/）ビルドシステムを使用します。プロジェクトの新しいディレクトリを作成し、ターミナルウィンドウでそのディレクトリに移動します。次に、次のコマンドを実行して新しいGradleプロジェクトを作成します。

```
gradle init --type kotlin-library
```

このコマンドは`kotlin-library`プラグインで新しいKotlinプロジェクトを作成します。このプラグインはKotlinライブラリの開発に使用されます。私たちはプロジェクトにこのプラグインを使用しませんが、必要な`kotlin-stdlib`依存関係が含まれているので、とにかく使用します。

## モンゴルDBに接続する

これでプロジェクトが設定されたので、依存関係の追加を開始できます。必要な最初の依存関係はMongoDBドライバです。 MongoDB Driverは、KotlinがMongoDBに接続してクエリできるようにするライブラリです。 [Maven Central Repository]（https://mvnrepository.com/artifact/org.mongodb/mongodb-driver）で最新バージョンのMongoDBドライバを見つけることができます。

`build.gradle`ファイルに以下を追加します。

「groovy
repositories {
    jcenter()
}

dependencies {
    implementation "org.mongodb:mongodb-driver:3.12.4"
}
```

最初の行はプロジェクトにJCenterリポジトリを追加します。 JCenter は、広く使用されている多くの Java ライブラリをホストするリポジトリです。 2行目はMongoDBドライバの依存関係を追加します。 「3.12.4」を最新バージョンのMongoDBドライバに置き換えます。

MongoDBドライバの依存関係があるので、コードを書くことができます。 MongoDBデータベースを表す `Database`オブジェクトを作成することから始めましょう。 `main.kt`ファイルに次のコードを追加します。

```kotlin
val database: Database = Database("mongodb://localhost:27017/test")
```

このコードは、MongoDBサーバーから `test`データベースを表す `Database`オブジェクトを生成します。 `mongodb`プロトコルは、私たちがMongoDBに接続していることを指定します。 `localhost`部分はMongoDBサーバーのホスト名を指定します。 `27017`はMongoDBが実行されているポートです。 `test`部分は、接続したいデータベースの名前です。

## モンゴルDBクエリ

これで`Database`オブジェクトがあるので、データベースクエリを開始できます。データベース内のすべての文書を照会することから始めましょう。 `main.kt`ファイルに次のコードを追加します。

```kotlin
val documents: List<Document> = database.find()
```

このコードはすべての文書に対してデータベースを照会し、文書を `Document`オブジェクトのリストとして返します。

特定の文書を照会することもできます。たとえば、値が「1」のフィールド「_id」を持つすべての文書を照会できます。 `main.kt`ファイルに次のコードを追加します。

```kotlin
val document: Document? = database.findOne(Document("_id", 1))
```

このコードは、「_id」フィールドが「1」の文書をデータベースに照会し、それを「Document」オブジェクトとして返します。そのドキュメントがない場合は `null` を返します。

データベースに文書を挿入することもできます。たとえば、「_id」フィールドが「1」で、「name」フィールドが「John」の文書を挿入できます。 `main.kt`ファイルに次のコードを追加します。

```kotlin
database.insertOne(Document("_id", 1).append("name", "John"))
```

このコードは、「_id」フィールドが「1」で、「name」フィールドが「John」の文書をデータベースに挿入します。

データベースから文書を更新することもできます。たとえば、挿入したばかりのドキュメントを更新して、「name」フィールドの値が「Jane」になるようにすることができます。 `main.kt`ファイルに次のコードを追加します。

```kotlin
database.updateOne(Document("_id", 1), Document("\$set", Document("name", "Jane"))))
```

このコードは、`name`フィールドの値が`Jane`になるように`_id`フィールドが`1`であるドキュメントを更新します。

##結論

この記事では、KotlinからMongoDBデータベースに接続する方法について説明しました。また、データベース内の文書を照会して更新する方法も見てきました。詳細については、[MongoDBドライバのドキュメント]（https://mongodb.github.io/mongo-java-driver/）を参照してください。