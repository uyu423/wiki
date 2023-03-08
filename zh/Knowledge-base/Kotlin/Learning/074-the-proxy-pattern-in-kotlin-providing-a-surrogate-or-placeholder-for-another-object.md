---
title: 074：Kotlin 中的代理模式：为另一个对象提供代理项或占位符
description: 
published: true
date: 2023-01-31T12:17:34.349Z
tags: 
editor: markdown
dateCreated: 2023-01-31T12:17:32.702Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [074: The Proxy Pattern in Kotlin: Providing a Surrogate or Placeholder for Another Object***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/074-the-proxy-pattern-in-kotlin-providing-a-surrogate-or-placeholder-for-another-object)
{.links-list}


  在“资源”部分添加指向原始文章的链接。

# 074：Kotlin 中的代理模式：为另一个对象提供代理项或占位符

代理模式是一种软件设计模式，它为另一个提供代理或占位符对象。在代理模式中，一个类代表另一个类的功能。这种类型的设计模式属于结构模式。

有四种类型的代理模式：

- 虚拟代理：虚拟代理是代表另一个对象的对象。例如，代表真实对象的图标。
- 远程代理：远程代理为驻留在不同地址空间中的对象提供本地代表。例如，访问 Web 服务。
- 保护代理：保护代理控制对敏感主对象的访问。 “代理”对象在访问之前检查真实主题是否可访问。
- 智能代理：智能代理向代理添加额外的逻辑。例如，引用计数。

在本文中，我们将重点关注虚拟代理模式。

## 什么是虚拟代理模式？

虚拟代理是代表另一个对象的对象。真正的对象只在需要的时候创建。例如，从远程服务器加载的图像。图像由代理对象表示。代理对象处理图像请求。加载图像时，代理对象将自己替换为真实图像对象。

虚拟代理可用于：

- 通过推迟昂贵对象的创建来提高性能。
- 隐藏对象的复杂性。
- 为尚不可用的对象提供占位符。

## 如何在 Kotlin 中实现虚拟代理模式？

我们将使用以下示例来演示虚拟代理模式。我们有一个代表用户的 User 类。 User 类有一个名字和一个头像。化身是图像。我们将使用虚拟代理来表示头像图像。

```kotlin
class User(val name: String, val avatar: Image)
```

Image 类表示图像。 Image 类具有宽度和高度。

```kotlin
class Image(val width: Int, val height: Int)
```

ImageProxy 类是 Image 类的代理。 ImageProxy 类引用了 Image 类。 ImageProxy 类也有一个加载标志。加载标志用于跟踪 Image 类是否正在加载。

```kotlin
class ImageProxy(val image: Image) {
    val loading = false
}
```

loadImage() 函数用于加载 Image 类。 loadImage() 函数接受一个图像 URL 和一个回调函数。加载图像时调用回调函数。

```kotlin
fun loadImage(imageUrl: String, callback: (Image) -> Unit) {
    // TODO: load image from URL
}
```

main() 函数创建一个带有 ImageProxy 对象的 User 对象。 ImageProxy 对象表示头像图像。 loadImage() 函数用于加载头像图像。加载图像时，ImageProxy 对象将替换为 Image 对象。

```kotlin
fun main() {
    val user = User("Alice", ImageProxy(null))

    loadImage("avatar.jpg") { image ->
        user.avatar = image
    }
}
```

## 什么时候使用虚拟代理模式？

在以下情况下应使用虚拟代理模式：

- 创建一个对象是昂贵的。
- 对象不经常使用。
- 该对象不是立即可用的。

## 虚拟代理模式的优势

虚拟代理模式具有以下优点：

- 它通过推迟昂贵对象的创建来提高性能。
- 它隐藏了对象的复杂性。

## 虚拟代理模式的缺点

虚拟代理模式有以下缺点：

- 它会引入复杂性。

## 资源

- [维基百科](https://en.wikipedia.org/wiki/Proxy_pattern)
- [来源制作](https://sourcemaking.com/design_patterns/proxy)