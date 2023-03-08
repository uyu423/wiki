---
title: Kotlin 和 MongoDB：连接到面向文档的数据库
description: 
published: true
date: 2023-02-17T18:11:09.944Z
tags: 
editor: markdown
dateCreated: 2023-01-30T18:17:29.596Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Kotlin and MongoDB: Connecting to a Document-Oriented Database***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-mongodb-connecting-to-a-document-oriented-database)
{.links-list}

    
# Kotlin 和 MongoDB：连接到面向文档的数据库

在本文中，我们将了解如何从 Kotlin 连接到 MongoDB 数据库。 MongoDB 是一个开源的面向文档的数据库系统，它使用带有模式的类似 JSON 的文档。它是 Web 应用程序的热门选择，也适用于在许多 Kotlin 应用程序中存储数据。

我们将从了解如何安装 MongoDB 开始。然后我们将创建一个 Kotlin 项目并将其连接到我们的 MongoDB 数据库。最后，我们将了解如何从 Kotlin 查询我们的数据库。

## 安装 MongoDB

MongoDB 适用于 Windows、MacOS 和 Linux。您可以从 [MongoDB 网站](https://www.mongodb.com/download-center#community) 下载它。确保下载与您的操作系统匹配的版本。

下载 MongoDB 后，解压缩存档并将内容提取到您选择的位置。对于本文，我们将其解压缩到“C:\mongodb”。

接下来，我们需要为 MongoDB 创建一个数据目录。数据目录是 MongoDB 将存储其数据文件的地方。在您的 MongoDB 安装目录中创建一个名为“data”的新目录。

现在我们有了我们的数据目录，我们可以启动 MongoDB。打开一个终端窗口并导航到您的 MongoDB 安装目录。然后运行以下命令：

```
mongod --dbpath C:\mongodb\data
```

此命令启动 MongoDB 服务器并告诉它使用我们的 `data` 目录作为数据目录。 MongoDB 现在将在后台运行。您可以打开或关闭此终端窗口，因为我们将不再需要它。

## 创建一个 Kotlin 项目

我们现在准备开始开发我们的 Kotlin 应用程序。我们将为此项目使用 [Gradle](https://gradle.org/) 构建系统。为您的项目创建一个新目录，并在终端窗口中导航到该目录。然后运行以下命令创建一个新的 Gradle 项目：

```
gradle init --type kotlin-library
```

此命令将使用 `kotlin-library` 插件创建一个新的 Kotlin 项目。此插件用于开发 Kotlin 库。我们不会在我们的项目中使用这个插件，但无论如何我们都会使用它，因为它包含我们需要的 `kotlin-stdlib` 依赖项。

## 连接到 MongoDB

现在我们已经设置了项目，我们可以开始添加依赖项了。我们需要的第一个依赖项是 MongoDB 驱动程序。 MongoDB 驱动程序是一个允许我们从 Kotlin 连接和查询 MongoDB 的库。您可以在 [Maven 中央存储库](https://mvnrepository.com/artifact/org.mongodb/mongodb-driver) 上找到最新版本的 MongoDB 驱动程序。

将以下内容添加到您的 `build.gradle` 文件中：

```groovy
repositories {
    jcenter()
}

dependencies {
    implementation "org.mongodb:mongodb-driver:3.12.4"
}
```

第一行将 JCenter 存储库添加到我们的项目中。 JCenter 是一个存储库，其中包含许多流行的 Java 库。第二行添加 MongoDB Driver 依赖。将 `3.12.4` 替换为最新版本的 MongoDB 驱动程序。

现在我们有了 MongoDB Driver 依赖，我们可以开始编写代码了。我们将从创建代表我们的 MongoDB 数据库的“数据库”对象开始。将以下代码添加到您的 `main.kt` 文件中：

```kotlin
val database: Database = Database("mongodb://localhost:27017/test")
```

此代码创建一个“数据库”对象，代表我们 MongoDB 服务器上的“测试”数据库。 `mongodb` 协议指定我们要连接到 MongoDB。 `localhost` 部分指定我们的 MongoDB 服务器的主机名。 `27017` 是运行 MongoDB 的端口。 `test` 部分是我们要连接的数据库的名称。

## 查询 MongoDB

现在我们有了一个“数据库”对象，我们可以开始查询我们的数据库了。我们将从查询数据库中的所有文档开始。将以下代码添加到您的 `main.kt` 文件中：

```kotlin
val documents: List<Document> = database.find()
```

此代码在我们的数据库中查询所有文档，并将它们作为“Document”对象列表返回。

我们还可以查询特定的文件。例如，我们可以查询所有 _id 字段值为 1 的文档。将以下代码添加到您的 `main.kt` 文件中：

```kotlin
val document: Document? = database.findOne(Document("_id", 1))
```

此代码在我们的数据库中查询 _id 字段为 1 的文档，并将其作为 Document 对象返回。如果不存在这样的文档，则返回“null”。

我们还可以将文档插入到我们的数据库中。例如，我们可以插入一个 _id 字段为 1 且 name 字段为 John 的文档。将以下代码添加到您的 `main.kt` 文件中：

```kotlin
database.insertOne(Document("_id", 1).append("name", "John"))
```

此代码将“_id”字段为“1”且“name”字段为“John”的文档插入到我们的数据库中。

我们还可以更新数据库中的文档。例如，我们可以更新刚刚插入的文档，使“name”字段的值为“Jane”。将以下代码添加到您的 `main.kt` 文件中：

```kotlin
database.updateOne(Document("_id", 1), Document("\$set", Document("name", "Jane")))
```

此代码使用“1”的“_id”字段更新文档，以便“name”字段的值为“Jane”。

## 结论

在本文中，我们了解了如何从 Kotlin 连接到 MongoDB 数据库。我们还了解了如何查询和更新数据库中的文档。有关详细信息，请参阅 [MongoDB 驱动程序文档](https://mongodb.github.io/mongo-java-driver/)。