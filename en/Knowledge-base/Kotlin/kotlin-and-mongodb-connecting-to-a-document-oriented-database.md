---
title: Kotlin and MongoDB: Connecting to a Document-Oriented Database
description: 
published: true
date: 2023-02-17T18:10:56.223Z
tags: 
editor: markdown
dateCreated: 2023-01-30T18:17:29.591Z
---

- [Kotlin 및 MongoDB: 문서 지향 데이터베이스에 연결***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/kotlin-and-mongodb-connecting-to-a-document-oriented-database)
{.links-list}
- [Kotlin と MongoDB: ドキュメント指向データベースへの接続***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/kotlin-and-mongodb-connecting-to-a-document-oriented-database)
{.links-list}
- [Kotlin 和 MongoDB：连接到面向文档的数据库***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/kotlin-and-mongodb-connecting-to-a-document-oriented-database)
{.links-list}

    
# Kotlin and MongoDB: Connecting to a Document-Oriented Database

In this article, we'll take a look at how to connect to a MongoDB database from Kotlin. MongoDB is a open source document-oriented database system that uses JSON-like documents with schemas. It's a popular choice for web applications and is also suitable for storing data in many Kotlin applications.

We'll start by looking at how to install MongoDB. Then we'll create a Kotlin project and connect it to our MongoDB database. We'll finish by looking at how to query our database from Kotlin.

## Installing MongoDB

MongoDB is available for Windows, MacOS, and Linux. You can download it from the [MongoDB website](https://www.mongodb.com/download-center#community). Make sure to download the version that matches your operating system.

Once you've downloaded MongoDB, unzip the archive and extract the contents to a location of your choice. For this article, we'll extract it to `C:\mongodb`.

Next, we need to create a data directory for MongoDB. The data directory is where MongoDB will store its data files. Create a new directory called `data` in your MongoDB installation directory.

Now that we have our data directory, we can start MongoDB. Open a terminal window and navigate to your MongoDB installation directory. Then run the following command:

```
mongod --dbpath C:\mongodb\data
```

This command starts the MongoDB server and tells it to use our `data` directory as the data directory. MongoDB will now be running in the background. You can leave this terminal window open or close it, as we won't be needing it again.

## Creating a Kotlin Project

We're now ready to start developing our Kotlin application. We'll be using the [Gradle](https://gradle.org/) build system for this project. Create a new directory for your project and navigate to it in a terminal window. Then run the following command to create a new Gradle project:

```
gradle init --type kotlin-library
```

This command will create a new Kotlin project with the `kotlin-library` plugin. This plugin is used for developing Kotlin libraries. We won't be using this plugin for our project, but we'll be using it anyway as it includes the `kotlin-stdlib` dependency, which we need.

## Connecting to MongoDB

Now that we have our project set up, we can start adding dependencies. The first dependency we need is the MongoDB Driver. The MongoDB Driver is a library that allows us to connect to and query MongoDB from Kotlin. You can find the latest version of the MongoDB Driver on the [Maven Central Repository](https://mvnrepository.com/artifact/org.mongodb/mongodb-driver).

Add the following to your `build.gradle` file:

```groovy
repositories {
    jcenter()
}

dependencies {
    implementation "org.mongodb:mongodb-driver:3.12.4"
}
```

The first line adds the JCenter repository to our project. JCenter is a repository that hosts a lot of popular Java libraries. The second line adds the MongoDB Driver dependency. Replace `3.12.4` with the latest version of the MongoDB Driver.

Now that we have the MongoDB Driver dependency, we can start writing code. We'll start by creating a `Database` object that represents our MongoDB database. Add the following code to your `main.kt` file:

```kotlin
val database: Database = Database("mongodb://localhost:27017/test")
```

This code creates a `Database` object that represents the `test` database on our MongoDB server. The `mongodb` protocol specifies that we're connecting to MongoDB. The `localhost` part specifies the hostname of our MongoDB server. The `27017` is the port that MongoDB is running on. The `test` part is the name of the database we want to connect to.

## Querying MongoDB

Now that we have a `Database` object, we can start querying our database. We'll start by querying for all the documents in our database. Add the following code to your `main.kt` file:

```kotlin
val documents: List<Document> = database.find()
```

This code querys our database for all the documents and returns them as a list of `Document` objects.

We can also query for specific documents. For example, we can query for all the documents that have an `_id` field with the value `1`. Add the following code to your `main.kt` file:

```kotlin
val document: Document? = database.findOne(Document("_id", 1))
```

This code queries our database for a document with an `_id` field of `1` and returns it as a `Document` object. If no such document exists, it returns `null`.

We can also insert documents into our database. For example, we can insert a document with an `_id` field of `1` and a `name` field of `John`. Add the following code to your `main.kt` file:

```kotlin
database.insertOne(Document("_id", 1).append("name", "John"))
```

This code inserts a document with an `_id` field of `1` and a `name` field of `John` into our database.

We can also update documents in our database. For example, we can update the document we just inserted so that the `name` field has a value of `Jane`. Add the following code to your `main.kt` file:

```kotlin
database.updateOne(Document("_id", 1), Document("\$set", Document("name", "Jane")))
```

This code updates the document with an `_id` field of `1` so that the `name` field has a value of `Jane`.

## Conclusion

In this article, we've looked at how to connect to a MongoDB database from Kotlin. We've also seen how to query and update documents in our database. For more information, see the [MongoDB Driver documentation](https://mongodb.github.io/mongo-java-driver/).