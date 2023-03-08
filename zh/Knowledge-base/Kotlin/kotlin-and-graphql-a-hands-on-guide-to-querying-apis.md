---
title: Kotlin 和 GraphQL：查询 API 的实用指南
description: 
published: true
date: 2023-02-17T18:03:32.172Z
tags: 
editor: markdown
dateCreated: 2023-01-30T11:16:17.752Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Kotlin and GraphQL: A Hands-on Guide to Querying APIs***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-graphql-a-hands-on-guide-to-querying-apis)
{.links-list}


# Kotlin 和 GraphQL：查询 API 的实用指南

在本文中，我们将亲身体验使用 Kotlin 和 GraphQL 查询 API。我们将介绍 GraphQL 和 Kotlin 的一些基础知识，然后直接进入 API 查询。

## 什么是 GraphQL？

GraphQL 是 API 的查询语言。它由 Facebook 于 2012 年创建，并于 2015 年开源。GraphQL 提供了一种从 API 查询数据的结构化方式。它还允许 API 在不破坏现有客户端的情况下随着时间的推移而发展。

## 什么是科特林？

Kotlin 是一种在 JVM 上运行的静态类型编程语言。它由 JetBrains 于 2011 年创建，并于 2012 年开源。Kotlin 是一种简洁易读的语言，可与 Java 完全互操作。

## 入门

首先，我们需要安装 Kotlin 编译器和 GraphQL 库。

### 安装 Kotlin 编译器

Kotlin 编译器可从 [Kotlin 网站](https://kotlinlang.org/) 下载。只需下载最新版本并将其解压缩到您选择的目录即可。

### 安装 GraphQL 库

GraphQL 库可从 [GraphQL 网站](https://graphql.org/) 下载。只需下载最新版本并将其解压缩到您选择的目录即可。

## 查询 API

现在我们已经安装了 Kotlin 编译器和 GraphQL 库，我们可以开始查询 API。

要查询 API，我们首先需要创建一个 GraphQL 查询。 GraphQL 查询是一个字符串，它指定您要查询的字段。例如，以下查询将获取用户的“id”、“name”和“email”字段：

```graphql
query {
  user {
    id
    name
    email
  }
}
```

然后我们可以使用 Kotlin 编译器编译查询并针对 API 执行它。以下示例显示了如何执行此操作：

```kotlin
import com.graphql.client.GraphQL

fun main() {
  val query = "query { user { id name email } }"
  val result = GraphQL.execute(query)
  println(result)
}
```

`execute` 方法将返回一个 `Result` 对象，其中包含 API 返回的数据。在这种情况下，“Result”对象将包含用户的“id”、“name”和“email”字段。

## 结论

在本文中，我们亲身体验了使用 Kotlin 和 GraphQL 查询 API。我们介绍了 GraphQL 和 Kotlin 的一些基础知识，然后直接开始查询 API。