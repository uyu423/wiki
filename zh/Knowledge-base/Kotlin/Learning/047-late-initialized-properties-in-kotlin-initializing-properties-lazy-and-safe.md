---
title: 047：Kotlin 中的延迟初始化属性：惰性且安全地初始化属性
description: 
published: true
date: 2023-02-16T14:32:27.359Z
tags: 
editor: markdown
dateCreated: 2023-02-16T14:32:19.414Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [047: Late-initialized Properties in Kotlin: Initializing Properties Lazy and Safe***English** document is available*](/en/Knowledge-base/Kotlin/Learning/047-late-initialized-properties-in-kotlin-initializing-properties-lazy-and-safe)
{.links-list}


# Kotlin 中的延迟初始化属性：惰性且安全地初始化属性

Kotlin 的延迟初始化属性是一种惰性且安全地初始化属性的好方法。在这篇文章中，我们将看看如何使用延迟初始化的属性来发挥我们的优势。

## 什么是延迟初始化的属性？

后期初始化属性是在对象构造期间未初始化的属性。相反，它们在第一次访问属性时被初始化。这对于初始化成本高或不经常使用的属性很有用。

## 如何使用延迟初始化的属性

要使用延迟初始化的属性，我们首先需要使用 ```lateinit``` 关键字声明它：

```kotlin
lateinit var property: Type
```

然后我们可以在第一次访问它时初始化该属性：

```kotlin
property = value
```

## 延迟初始化属性的优点

使用延迟初始化的属性有两个主要优点：性能和安全性。

### 表现

延迟初始化的属性可以提高性能，因为它们在首次访问之前不会被初始化。这意味着我们可以避免初始化不经常使用的属性。

### 安全

延迟初始化的属性也可以安全使用。这是因为它们在首次访问之前不会被初始化。这意味着我们可以避免使用尚未初始化的属性。

## 延迟初始化属性的缺点

使用延迟初始化的属性有两个主要缺点：可读性和调试。

### 可读性

延迟初始化的属性可能更难阅读，因为它们在首次访问之前不会被初始化。这意味着我们需要在使用它们之前小心地初始化属性。

### 调试

延迟初始化的属性也可能更难调试，因为它们在首次访问之前不会被初始化。这意味着我们需要在使用它们之前小心地初始化属性。