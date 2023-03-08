---
title: Kotlin 和哈希：保护密码和敏感数据
description: 
published: true
date: 2023-02-06T14:17:39.236Z
tags: 
editor: markdown
dateCreated: 2023-02-06T14:17:33.593Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kotlin and Hashing: Securing Passwords and Sensitive Data***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-hashing-securing-passwords-and-sensitive-data)
{.links-list}


# Kotlin 和哈希：保护密码和敏感数据

随着 Kotlin 作为 Android 开发语言的兴起，了解如何正确保护应用程序中的密码和敏感数据非常重要。在本文中，我们将讨论如何使用哈希来保护这些信息。

## 什么是哈希？

哈希是将任意大小的数据映射到固定大小的数据的过程。固定大小的数据称为散列值、散列码、散列摘要或简称为散列。哈希值是使用哈希算法生成的，该算法可以是简单的算法，如对数据字节求和，也可以是更复杂的算法，如 SHA-256。

## 为什么要使用哈希？

散列是一种单向过程，这意味着不可能通过反转过程来取回原始数据。这对安全性很重要，因为这意味着即使有人掌握了哈希值，他们也无法确定原始数据是什么。

## 如何在 Kotlin 中使用哈希

Kotlin 提供了一个名为“hashCode()”的内置哈希函数。该函数接受一个任意对象并返回一个“Int”散列值。例如，我们可以像这样散列一个 String ：

```kotlin
val hashValue = "password".hashCode()
```

`hashCode()` 函数不适用于加密目的，因为它可能为不同的数据生成相同的哈希值。例如，字符串“password”和“PASSWORD”具有相同的哈希值。

如果我们需要生成加密哈希值，我们可以使用 Java 加密扩展 (JCE) 库中的“MessageDigest”类。 Kotlin 为 `MessageDigest` 提供了一个名为 `digest()` 的扩展函数，使其易于使用：

```kotlin
import java.security.MessageDigest

fun MessageDigest.digest(data: ByteArray): ByteArray {
    update(data)
    return digest()
}
```

使用此函数，我们可以像这样计算 SHA-256 哈希值：

```kotlin
val data = "password".toByteArray()
val sha256 = MessageDigest.getInstance("SHA-256")
val hashValue = sha256.digest(data)
```

## 如何存储哈希

以安全的方式存储哈希非常重要，以防止攻击者能够确定原始数据是什么。一种方法是使用盐，这是一个随机字符串，在散列之前添加到数据中。盐与哈希值一起存储，并在检查给定密码是否正确时使用。

`MessageDigest` 类有一个 `update(salt: ByteArray)` 函数，可用于在数据散列之前向数据添加盐。例如：

```kotlin
val data = "password".toByteArray()
val salt = "somesalt".toByteArray()

val sha256 = MessageDigest.getInstance("SHA-256")
sha256.update(salt)
val hashValue = sha256.digest(data)
```

## 如何检查密码是否正确

要检查给定的密码是否正确，我们需要计算密码的哈希值并将其与存储的哈希值进行比较。如果匹配，则密码正确。

一种方法是再次使用“MessageDigest”类。我们可以像这样计算密码的哈希值：

```kotlin
val password = "password"
val hashValue = "hashValue".toByteArray()

val sha256 = MessageDigest.getInstance("SHA-256")
sha256.update(hashValue)
val passwordHash = sha256.digest(password.toByteArray())
```

然后，我们可以将 passwordHash 与存储的哈希值进行比较，看它们是否匹配。

另一种方法是使用 `hashCode()` 函数。我们可以像这样计算密码的哈希值：

```kotlin
val password = "password"
val hashValue = "hashValue".toByteArray()

val passwordHash = password.hashCode()
```

然后，我们可以将 passwordHash 与存储的哈希值进行比较，看它们是否匹配。

## 结论

在本文中，我们讨论了如何使用哈希来保护 Kotlin 应用程序中的密码和敏感数据。我们已经了解了如何使用 `hashCode()` 和 `MessageDigest` 函数计算哈希值，以及如何使用盐存储和检查哈希值。