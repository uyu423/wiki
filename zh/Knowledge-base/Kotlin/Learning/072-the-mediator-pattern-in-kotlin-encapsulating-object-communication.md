---
title: 072：Kotlin 中的中介模式：封装对象通信
description: 
published: true
date: 2023-02-03T15:17:29.734Z
tags: 
editor: markdown
dateCreated: 2023-02-03T15:17:28.144Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [072: The Mediator Pattern in Kotlin: Encapsulating Object Communication***English** document is available*](/en/Knowledge-base/Kotlin/Learning/072-the-mediator-pattern-in-kotlin-encapsulating-object-communication)
{.links-list}


# 072：Kotlin 中的中介模式：封装对象通信

中介者模式是一种行为软件设计模式，它可以实现对象之间的通信，而无需它们相互了解。这在需要集中控制或减少对象之间的依赖性的情况下很有用。

在这篇文章中，我们将了解如何在 Kotlin 中实现中介者模式。我们将从看一个简单的示例开始，该示例说明如何使用该模式来解耦对象。然后，我们将查看一个使用 Kotlin 标准库的更真实的示例。

## 一个简单的例子

假设我们有一个代表聊天室的类：

```kotlin
class ChatRoom {
    fun showMessage(user: User, message: String) {
        println("${user.name}: $message")
    }
}
```

还有一个代表用户的类：

```kotlin
class User(val name: String) {
    fun sendMessage(message: String) {
        ChatRoom.showMessage(this, message)
    }
}
```

在这个简单的示例中，“ChatRoom”类充当“User”对象之间的中介。 `User` 对象彼此不知道，它们只知道 `ChatRoom` 对象。

## 一个更现实的例子

在一个更现实的例子中，我们可能希望将 User 类与 ChatRoom 类分离。我们可以使用中介者模式来做到这一点。

首先，我们将创建一个“ChatRoom”界面：

```kotlin
interface ChatRoom {
    fun showMessage(user: User, message: String)
}
```

然后我们将创建一个“用户”界面：

```kotlin
interface User {
    fun sendMessage(message: String)
}
```

现在我们可以创建一个“ChatRoom”实现：

```kotlin
class DefaultChatRoom : ChatRoom {
    override fun showMessage(user: User, message: String) {
        println("${user.name}: $message")
    }
}
```

和一个“用户”实现：

```kotlin
class DefaultUser(override val name: String) : User {
    override fun sendMessage(message: String) {
        DefaultChatRoom.showMessage(this, message)
    }
}
```

在此示例中，“DefaultChatRoom”和“DefaultUser”类彼此分离。他们只通过他们实现的接口了解彼此。

## 结论

中介者模式是一种用于将对象彼此解耦的有用模式。它可用于集中控制或减少对象之间的依赖性。在 Kotlin 中，模式可以使用接口来实现。