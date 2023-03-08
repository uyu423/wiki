---
title: Kotlin 和 AES：加密和解密数据
description: 
published: true
date: 2023-02-08T00:17:35.150Z
tags: 
editor: markdown
dateCreated: 2023-02-08T00:17:33.533Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kotlin and AES: Encrypting and Decrypting Data***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-aes-encrypting-and-decrypting-data)
{.links-list}


# Kotlin 和 AES：加密和解密数据

Kotlin 是一种功能强大且用途广泛的编程语言，可用于执行各种任务，包括加密和解密数据。在本文中，我们将了解如何使用 Kotlin 和高级加密标准 (AES) 来加密和解密数据。

## 什么是 AES？

AES 是一种对称密钥算法，可用于加密和解密数据。 AES 是一种广泛使用的标准，被认为非常安全。

## 使用 Kotlin 加密数据

要使用 Kotlin 加密数据，我们将使用 ```javax.crypto.Cipher``` 类。此类提供加密和解密数据的功能。

我们将从创建一个```Cipher```实例开始。我们将使用 ```getInstance()``` 方法，它将算法的名称用作参数。对于 AES，我们将使用```"AES/ECB/PKCS5Padding"``` 算法。我们还需要指定要使用的模式和填充方案。

接下来，我们将创建一个```SecretKey``` 实例。 AES 需要长度为 16、24 或 32 字节的密钥。我们将在此示例中使用 16 字节的密钥。

一旦我们有了一个```Cipher``` 和一个```SecretKey```，我们就可以通过调用```init()``` 方法来初始化用于加密的密码，传入```Cipher. ENCRYPT_MODE``` 参数。

现在我们准备好加密我们的数据了。我们将调用```doFinal()``` 方法，传入要加密的数据。此方法返回包含加密数据的字节数组。

以下是如何使用 Kotlin 加密数据的示例：

```kotlin
fun encrypt(data: String, key: String): ByteArray {
    val cipher = Cipher.getInstance("AES/ECB/PKCS5Padding")
    val secretKey = SecretKeySpec(key.toByteArray(), "AES")
    cipher.init(Cipher.ENCRYPT_MODE, secretKey)
    return cipher.doFinal(data.toByteArray())
}
```

## 使用 Kotlin 解密数据

要使用 Kotlin 解密数据，我们将使用与加密数据相同的“Cipher”类。

首先，我们将创建一个```Cipher``` 实例和一个```SecretKey``` 实例，就像我们在加密数据时所做的那样。

接下来，我们将通过调用 ```init()``` 方法并传入 ```Cipher.DECRYPT_MODE``` 参数来初始化用于解密的密码。

现在我们准备解密我们的数据。我们将调用```doFinal()``` 方法，传入加密数据。此方法返回包含解密数据的字节数组。

以下是如何使用 Kotlin 解密数据的示例：

```kotlin
fun decrypt(data: ByteArray, key: String): String {
    val cipher = Cipher.getInstance("AES/ECB/PKCS5Padding")
    val secretKey = SecretKeySpec(key.toByteArray(), "AES")
    cipher.init(Cipher.DECRYPT_MODE, secretKey)
    return String(cipher.doFinal(data))
}
```

## AES 在行动

现在我们已经了解了如何使用 Kotlin 和 AES 加密和解密数据，让我们通过一个简单的示例来付诸实践。

我们将从创建一个 ```main()``` 函数开始。在这个函数中，我们将创建一个包含我们要加密的数据的```String```。我们还将创建一个```String```，其中包含我们将用于加密和解密数据的密钥。

接下来，我们将调用我们之前创建的 ```encrypt()``` 函数，传入数据和密钥。此函数将返回包含加密数据的字节数组。

最后，我们将调用```decrypt()``` 函数，传入加密数据和密钥。这个函数将返回一个包含解密数据的```String```。

这是完整的例子：

```kotlin
fun main() {
    val data = "This is the data to encrypt"
    val key = "0123456789abcdef"
    val encryptedData = encrypt(data, key)
    val decryptedData = decrypt(encryptedData, key)
    println(decryptedData)
}
```

当我们运行这段代码时，我们将看到以下输出：

```
This is the data to encrypt
```

## 结论

在本文中，我们了解了如何使用 Kotlin 和 AES 来加密和解密数据。我们还通过一个简单的示例了解了如何将其付诸实践。