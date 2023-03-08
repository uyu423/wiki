---
title: 073：Kotlin 中的享元模式：共享对象实例以节省内存
description: 
published: true
date: 2023-02-07T06:55:43.380Z
tags: 
editor: markdown
dateCreated: 2023-02-07T06:55:41.857Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [073: The Flyweight Pattern in Kotlin: Sharing Object Instances to Save Memory***English** document is available*](/en/Knowledge-base/Kotlin/Learning/073-the-flyweight-pattern-in-kotlin-sharing-object-instances-to-save-memory)
{.links-list}


# Kotlin 中的享元模式：共享对象实例以节省内存

在开发软件时，关键的考虑因素之一是如何有效地使用内存。优化内存使用的一种方法是使用享元模式。

享元模式是一种通过共享对象实例来帮助节省内存的设计模式。当您有大量共享相似状态的对象时，这尤其有用。

在本文中，我们将了解如何在 Kotlin 中使用享元模式。我们将首先了解享元模式是什么以及它是如何工作的。然后，我们将查看一些示例，了解如何在 Kotlin 中使用享元模式。

## 享元模式是什么？

享元模式是一种通过共享对象实例来帮助节省内存的设计模式。当您有大量共享相似状态的对象时，这尤其有用。

在享元模式中，对象的状态分为两部分：

* **内在状态**：这是所有相同类型的对象共享的状态。
* **外部状态**：这是每个对象独有的状态。

内在状态存储在享元对象中。外部状态存储在享元对象之外的客户端对象中。

当客户端对象需要访问享元对象时，它会将外部状态作为参数传入。然后享元对象使用外部状态返回正确的结果。

## 享元模式是如何工作的？

享元模式通过共享对象实例来工作。当您有大量共享相似状态的对象时，这尤其有用。

在享元模式中，对象的状态分为两部分：

* **内在状态**：这是所有相同类型的对象共享的状态。
* **外部状态**：这是每个对象独有的状态。

内在状态存储在享元对象中。外部状态存储在享元对象之外的客户端对象中。

当客户端对象需要访问享元对象时，它会将外部状态作为参数传入。然后享元对象使用外部状态返回正确的结果。

## 享元模式的例子

现在我们已经了解了享元模式的工作原理，让我们看一些如何在 Kotlin 中使用享元模式的示例。

### 示例 1：创建享元对象

在这个例子中，我们将创建一个享元对象来存储用户的内在状态。


```kotlin
// The flyweight object
class User(val name: String) {

}

// The client object
class UserClient(val user: User) {

    fun doSomething() {
        // Use the user object
    }
}

// Create a flyweight object
val user = User("John Smith")

// Create a client object
val userClient = UserClient(user)

// Use the client object
userClient.doSomething()
```

在这个例子中，我们创建了一个享元对象来存储用户的内在状态。我们还创建了一个使用享元对象的客户端对象。

### 示例 2：传递外部状态

在这个例子中，我们将创建一个享元对象来存储用户的内在状态。我们还将创建一个使用享元对象的客户端对象。

当客户端对象需要使用享元对象时，它会将外部状态作为参数传入。


```kotlin
// The flyweight object
class User(val name: String) {

    fun doSomething(state: String) {
        // Use the user object
    }
}

// The client object
class UserClient(val user: User) {

    fun doSomething() {
        // Pass in the extrinsic state
        user.doSomething("John Smith")
    }
}

// Create a flyweight object
val user = User("John Smith")

// Create a client object
val userClient = UserClient(user)

// Use the client object
userClient.doSomething()
```

在这个例子中，我们创建了一个享元对象来存储用户的内在状态。我们还创建了一个使用享元对象的客户端对象。

当客户端对象需要使用享元对象时，它传入外部状态作为参数。