---
title: Kotlin and Hashing: Securing Passwords and Sensitive Data
description: 
published: true
date: 2023-02-06T14:17:35.235Z
tags: 
editor: markdown
dateCreated: 2023-02-06T14:17:33.599Z
---

- [Kotlin y Hashing: Protección de contraseñas y datos confidenciales***Spanish** document is available*](/es/Knowledge-base/Kotlin/kotlin-and-hashing-securing-passwords-and-sensitive-data)
{.links-list}
- [Kotlin 和哈希：保护密码和敏感数据***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/kotlin-and-hashing-securing-passwords-and-sensitive-data)
{.links-list}
- [Kotlin 및 해싱: 암호 및 민감한 데이터 보호***Korean** document is available*](/ko/Knowledge-base/Kotlin/kotlin-and-hashing-securing-passwords-and-sensitive-data)
{.links-list}


# Kotlin and Hashing: Securing Passwords and Sensitive Data

With the rise of Kotlin as a language for Android development, it's important to know how to properly secure passwords and sensitive data in your applications. In this article, we'll discuss how to use hashing to protect this information.

## What is Hashing?

Hashing is a process of mapping data of arbitrary size to data of a fixed size. The fixed-size data is called a hash value, hash code, hash digest, or simply hash. The hash value is generated using a hashing algorithm, which can be a simple algorithm like summing the bytes of the data or a more complex algorithm like SHA-256.

## Why Use Hashing?

Hashing is a one-way process, which means that it's not possible to reverse the process to get the original data back. This is important for security because it means that even if someone gets ahold of the hash value, they won't be able to determine what the original data was.

## How to Use Hashing in Kotlin

Kotlin provides a built-in hashing function called `hashCode()`. This function takes an arbitrary object and returns an `Int` hash value. For example, we can hash a `String` like this:

```kotlin
val hashValue = "password".hashCode()
```

The `hashCode()` function is not suitable for cryptographic purposes because it's possible to generate the same hash value for different data. For example, the strings "password" and "PASSWORD" have the same hash value.

If we need to generate a cryptographic hash value, we can use the `MessageDigest` class from the Java Cryptography Extension (JCE) library. Kotlin provides an extension function for `MessageDigest` called `digest()` that makes it easy to use:

```kotlin
import java.security.MessageDigest

fun MessageDigest.digest(data: ByteArray): ByteArray {
    update(data)
    return digest()
}
```

With this function, we can compute a SHA-256 hash like this:

```kotlin
val data = "password".toByteArray()
val sha256 = MessageDigest.getInstance("SHA-256")
val hashValue = sha256.digest(data)
```

## How to Store Hashes

It's important to store hashes in a secure manner to prevent attackers from being able to determine what the original data was. One way to do this is to use a salt, which is a random string that is added to the data before it's hashed. The salt is stored along with the hash value, and it's used when checking if a given password is correct.

The `MessageDigest` class has a `update(salt: ByteArray)` function that can be used to add a salt to the data before it's hashed. For example:

```kotlin
val data = "password".toByteArray()
val salt = "somesalt".toByteArray()

val sha256 = MessageDigest.getInstance("SHA-256")
sha256.update(salt)
val hashValue = sha256.digest(data)
```

## How to Check if a Password is Correct

To check if a given password is correct, we need to compute the hash of the password and compare it to the stored hash value. If they match, then the password is correct.

One way to do this is to use the `MessageDigest` class again. We can compute the hash of the password like this:

```kotlin
val password = "password"
val hashValue = "hashValue".toByteArray()

val sha256 = MessageDigest.getInstance("SHA-256")
sha256.update(hashValue)
val passwordHash = sha256.digest(password.toByteArray())
```

Then, we can compare the `passwordHash` to the stored hash value to see if they match.

Another way to do this is to use the `hashCode()` function. We can compute the hash of the password like this:

```kotlin
val password = "password"
val hashValue = "hashValue".toByteArray()

val passwordHash = password.hashCode()
```

Then, we can compare the `passwordHash` to the stored hash value to see if they match.

## Conclusion

In this article, we've discussed how to use hashing to secure passwords and sensitive data in Kotlin applications. We've seen how to compute hashes using the `hashCode()` and `MessageDigest` functions and how to store and check hashes using a salt.