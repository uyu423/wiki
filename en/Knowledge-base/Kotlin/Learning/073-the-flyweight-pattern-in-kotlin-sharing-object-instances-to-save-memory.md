---
title: 073: The Flyweight Pattern in Kotlin: Sharing Object Instances to Save Memory
description: 
published: true
date: 2023-02-07T06:55:47.567Z
tags: 
editor: markdown
dateCreated: 2023-02-07T06:55:41.865Z
---

- [073: El patrón Flyweight en Kotlin: compartir instancias de objetos para ahorrar memoria***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/073-the-flyweight-pattern-in-kotlin-sharing-object-instances-to-save-memory)
{.links-list}
- [073：Kotlin 中的享元模式：共享对象实例以节省内存***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/073-the-flyweight-pattern-in-kotlin-sharing-object-instances-to-save-memory)
{.links-list}
- [073: Kotlin의 Flyweight 패턴: 객체 인스턴스를 공유하여 메모리 절약***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/073-the-flyweight-pattern-in-kotlin-sharing-object-instances-to-save-memory)
{.links-list}


# The Flyweight Pattern in Kotlin: Sharing Object Instances to Save Memory

When it comes to developing software, one of the key considerations is how to efficiently use memory. One way to optimize memory usage is to use the flyweight pattern.

The flyweight pattern is a design pattern that helps to save memory by sharing object instances. This is especially useful when you have a large number of objects that share similar state.

In this post, we'll take a look at how to use the flyweight pattern in Kotlin. We'll start by looking at what the flyweight pattern is and how it works. We'll then look at some examples of how to use the flyweight pattern in Kotlin.

## What is the flyweight pattern?

The flyweight pattern is a design pattern that helps to save memory by sharing object instances. This is especially useful when you have a large number of objects that share similar state.

In the flyweight pattern, an object's state is divided into two parts:

* **Intrinsic state**: This is the state that is shared by all objects of the same type.
* **Extrinsic state**: This is the state that is unique to each object.

The intrinsic state is stored in a flyweight object. The extrinsic state is stored outside of the flyweight object, in the client object.

When a client object needs to access the flyweight object, it passes in the extrinsic state as an argument. The flyweight object then uses the extrinsic state to return the correct result.

## How does the flyweight pattern work?

The flyweight pattern works by sharing object instances. This is especially useful when you have a large number of objects that share similar state.

In the flyweight pattern, an object's state is divided into two parts:

* **Intrinsic state**: This is the state that is shared by all objects of the same type.
* **Extrinsic state**: This is the state that is unique to each object.

The intrinsic state is stored in a flyweight object. The extrinsic state is stored outside of the flyweight object, in the client object.

When a client object needs to access the flyweight object, it passes in the extrinsic state as an argument. The flyweight object then uses the extrinsic state to return the correct result.

## Examples of the flyweight pattern

Now that we've seen how the flyweight pattern works, let's look at some examples of how to use the flyweight pattern in Kotlin.

### Example 1: Creating a flyweight object

In this example, we'll create a flyweight object that stores the intrinsic state of a user.


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

In this example, we've created a flyweight object that stores the intrinsic state of a user. We've also created a client object that uses the flyweight object.

### Example 2: Passing in extrinsic state

In this example, we'll create a flyweight object that stores the intrinsic state of a user. We'll also create a client object that uses the flyweight object.

When the client object needs to use the flyweight object, it will pass in the extrinsic state as an argument.


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

In this example, we've created a flyweight object that stores the intrinsic state of a user. We've also created a client object that uses the flyweight object.

When the client object needs to use the flyweight object, it passes in the extrinsic state as an argument.