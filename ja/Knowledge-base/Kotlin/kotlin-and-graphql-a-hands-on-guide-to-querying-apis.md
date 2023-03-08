---
title: Kotlin と GraphQL: API クエリのハンズオン ガイド
description: 
published: true
date: 2023-02-17T18:03:30.148Z
tags: 
editor: markdown
dateCreated: 2023-01-30T11:16:17.751Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Kotlin and GraphQL: A Hands-on Guide to Querying APIs***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-graphql-a-hands-on-guide-to-querying-apis)
{.links-list}


# Kotlin and GraphQL: API クエリ実習ガイド

この記事では、KotlinとGraphQLを使用してAPIを照会する方法を直接見ていきます。 GraphQLとKotlinのいくつかの基本を見て、すぐにAPIクエリを見てみましょう。

## GraphQLとは？

GraphQLはAPI用のクエリ言語です。 2012年にFacebookで作成され、2015年にオープンソースとして公開されました。 GraphQLは、APIからデータを照会する構造化された方法を提供します。また、既存のクライアントを損なうことなく、時間の経過とともにAPIが進化する可能性があります。

##コトリンとは？

Kotlin は、JVM で実行される静的型のプログラミング言語です。 2011年にJetBrainsで作成され、2012年にオープンソースとして公開されました。 KotlinはJavaと完全に相互運用できる簡潔で読みやすい言語です。

##はじめに

開始するには、KotlinコンパイラとGraphQLライブラリをインストールする必要があります。

### Kotlinコンパイラのインストール

Kotlinコンパイラは、[Kotlin Webサイト]（https://kotlinlang.org/）からダウンロードできます。最新バージョンをダウンロードし、必要なディレクトリに解凍するだけです。

### GraphQLライブラリのインストール

GraphQLライブラリは、[GraphQL Webサイト]（https://graphql.org/）からダウンロードできます。最新バージョンをダウンロードし、必要なディレクトリに解凍するだけです。

## APIクエリ

これでKotlinコンパイラとGraphQLライブラリがインストールされたので、APIクエリを開始する準備が整いました。

API を照会するには、まず GraphQL 照会を生成する必要があります。 GraphQLクエリは、クエリするフィールドを指定する文字列です。たとえば、次のクエリはユーザーの `id`、 `name`、および `email`フィールドを取得します。

```graphql
query {
  user {
    id
    名前
    email
  }
}
```

その後、Kotlinコンパイラを使用してクエリをコンパイルし、APIに対して実行できます。次の例は、これを行う方法を示しています。

```kotlin
import com.graphql.client.GraphQL

fun main() {
  val query = "query { user { id name email } }"
  val result = GraphQL.execute(query)
  println(result)
}
```

`execute`メソッドは、APIから返されたデータを含む `Result`オブジェクトを返します。この場合、 `Result`オブジェクトにはユーザーの `id`、 `name`、および `email`フィールドが含まれます。

##結論

この記事では、KotlinとGraphQLを使用してAPIを照会する方法を直接見てきました。私たちはGraphQLとKotlinのいくつかの基本を見て、すぐにAPIクエリに飛び込みました。