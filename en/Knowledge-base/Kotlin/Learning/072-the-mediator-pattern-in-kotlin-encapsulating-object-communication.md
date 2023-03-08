---
title: 072: The Mediator Pattern in Kotlin: Encapsulating Object Communication
description: 
published: true
date: 2023-02-03T15:17:33.249Z
tags: 
editor: markdown
dateCreated: 2023-02-03T15:17:28.153Z
---

- [072: El patrón mediador en Kotlin: encapsulando la comunicación de objetos***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/072-the-mediator-pattern-in-kotlin-encapsulating-object-communication)
{.links-list}
- [072：Kotlin 中的中介模式：封装对象通信***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/072-the-mediator-pattern-in-kotlin-encapsulating-object-communication)
{.links-list}
- [072: Kotlin의 중재자 패턴: 개체 통신 캡슐화***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/072-the-mediator-pattern-in-kotlin-encapsulating-object-communication)
{.links-list}


# 072: The Mediator Pattern in Kotlin: Encapsulating Object Communication

The mediator pattern is a behavioral software design pattern that enables communication between objects without them needing to be aware of each other. This can be useful in situations where there is a need to centralize control or reduce the dependencies between objects.

In this post, we'll take a look at how the mediator pattern can be implemented in Kotlin. We'll start by looking at a simple example of how the pattern can be used to decouple objects. We'll then look at a more realistic example that makes use of the Kotlin Standard Library.

## A Simple Example

Suppose we have a class that represents a chat room:

```kotlin
class ChatRoom {
    fun showMessage(user: User, message: String) {
        println("${user.name}: $message")
    }
}
```

And a class that represents a user:

```kotlin
class User(val name: String) {
    fun sendMessage(message: String) {
        ChatRoom.showMessage(this, message)
    }
}
```

In this simple example, the `ChatRoom` class is acting as a mediator between the `User` objects. The `User` objects are not aware of each other, they only know about the `ChatRoom` object.

## A More Realistic Example

In a more realistic example, we might want to decouple the `User` class from the `ChatRoom` class. We can do this by using the mediator pattern.

First, we'll create a `ChatRoom` interface:

```kotlin
interface ChatRoom {
    fun showMessage(user: User, message: String)
}
```

Then we'll create a `User` interface:

```kotlin
interface User {
    fun sendMessage(message: String)
}
```

Now we can create a `ChatRoom` implementation:

```kotlin
class DefaultChatRoom : ChatRoom {
    override fun showMessage(user: User, message: String) {
        println("${user.name}: $message")
    }
}
```

And a `User` implementation:

```kotlin
class DefaultUser(override val name: String) : User {
    override fun sendMessage(message: String) {
        DefaultChatRoom.showMessage(this, message)
    }
}
```

In this example, the `DefaultChatRoom` and `DefaultUser` classes are decoupled from each other. They only know about each other through the interfaces they implement.

## Conclusion

The mediator pattern is a useful pattern for decoupling objects from each other. It can be used to centralize control or reduce dependencies between objects. In Kotlin, the pattern can be implemented using interfaces.