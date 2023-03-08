---
title: 074: The Proxy Pattern in Kotlin: Providing a Surrogate or Placeholder for Another Object
description: 
published: true
date: 2023-01-31T12:17:36.283Z
tags: 
editor: markdown
dateCreated: 2023-01-31T12:17:32.699Z
---

- [074: Kotlin의 프록시 패턴: 다른 개체에 대리자 또는 자리 표시자 제공***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/074-the-proxy-pattern-in-kotlin-providing-a-surrogate-or-placeholder-for-another-object)
{.links-list}
- [074: Kotlin のプロキシ パターン: 別のオブジェクトのサロゲートまたはプレースホルダーを提供する***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/074-the-proxy-pattern-in-kotlin-providing-a-surrogate-or-placeholder-for-another-object)
{.links-list}
- [074：Kotlin 中的代理模式：为另一个对象提供代理项或占位符***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/074-the-proxy-pattern-in-kotlin-providing-a-surrogate-or-placeholder-for-another-object)
{.links-list}


  Add a link to the original article in the "Resources" section.

# 074: The Proxy Pattern in Kotlin: Providing a Surrogate or Placeholder for Another Object

The Proxy Pattern is a software design pattern that provides a surrogate or placeholder object for another. In proxy pattern, a class represents functionality of another class. This type of design pattern comes under structural patterns.

There are four types of proxy patterns:

- Virtual Proxy: A virtual proxy is an object that represents another object. For example, an icon that represents a real object.
- Remote Proxy: A remote proxy provides a local representative for an object that resides in a different address space. For example, accessing a web service.
- Protective Proxy: A protective proxy controls access to a sensitive master object. The "surrogate" object checks that the real subject is accessible before it is accessed.
- Smart Proxy: A smart proxy adds additional logic to a proxy. For example, reference counting.

In this article, we will focus on the Virtual Proxy pattern.

## What is the Virtual Proxy Pattern?

A virtual proxy is an object that represents another object. The real object is only created when it is needed. For example, an image that is loading from a remote server. The image is represented by a proxy object. The proxy object handles the request for the image. When the image is loaded, the proxy object replaces itself with the real image object.

A virtual proxy can be used to:

- Improve performance by deferring the creation of expensive objects.
- Hide the complexity of an object.
- Provide a placeholder for an object that is not yet available.

## How to implement the Virtual Proxy Pattern in Kotlin?

We will use the following example to demonstrate the Virtual Proxy pattern. We have a User class that represents a user. The User class has a name and an avatar. The avatar is an image. We will use a virtual proxy to represent the avatar image.

```kotlin
class User(val name: String, val avatar: Image)
```

The Image class represents an image. The Image class has a width and a height.

```kotlin
class Image(val width: Int, val height: Int)
```

The ImageProxy class is a proxy for the Image class. The ImageProxy class has a reference to the Image class. The ImageProxy class also has a loading flag. The loading flag is used to track whether the Image class is loading or not.

```kotlin
class ImageProxy(val image: Image) {
    val loading = false
}
```

The loadImage() function is used to load the Image class. The loadImage() function takes an image URL and a callback function. The callback function is called when the image is loaded.

```kotlin
fun loadImage(imageUrl: String, callback: (Image) -> Unit) {
    // TODO: load image from URL
}
```

The main() function creates a User object with an ImageProxy object. The ImageProxy object represents the avatar image. The loadImage() function is used to load the avatar image. When the image is loaded, the ImageProxy object is replaced with the Image object.

```kotlin
fun main() {
    val user = User("Alice", ImageProxy(null))

    loadImage("avatar.jpg") { image ->
        user.avatar = image
    }
}
```

## When to use the Virtual Proxy Pattern?

The Virtual Proxy pattern should be used when:

- Creating an object is expensive.
- The object is not used frequently.
- The object is not available immediately.

## Advantages of the Virtual Proxy Pattern

The Virtual Proxy pattern has the following advantages:

- It improves performance by deferring the creation of expensive objects.
- It hides the complexity of an object.

## Disadvantages of the Virtual Proxy Pattern

The Virtual Proxy pattern has the following disadvantages:

- It can introduce complexity.

## Resources

- [Wikipedia](https://en.wikipedia.org/wiki/Proxy_pattern)
- [Source Making](https://sourcemaking.com/design_patterns/proxy)