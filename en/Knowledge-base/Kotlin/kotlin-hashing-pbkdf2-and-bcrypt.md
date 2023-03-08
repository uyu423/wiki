---
title: Kotlin Hashing: PBKDF2 and Bcrypt
description: 
published: true
date: 2023-02-18T02:06:28.305Z
tags: 
editor: markdown
dateCreated: 2023-02-18T02:06:21.604Z
---

- [코틀린 해싱: PBKDF2 및 Bcrypt***Korean** document is available*](/ko/Knowledge-base/Kotlin/kotlin-hashing-pbkdf2-and-bcrypt)
{.links-list}


# Kotlin Hashing

Kotlin is a powerful programming language that offers many features for developing secure applications. One of the most important security features is hashing. Hashing is a process of transforming data into a fixed-length value that is difficult to reverse. This makes it ideal for storing sensitive data such as passwords and for verifying the integrity of data.

Kotlin offers two hashing algorithms: PBKDF2 and bcrypt.

## PBKDF2

PBKDF2 is a standard algorithm for hashing passwords. It is specified in [RFC 2898](https://tools.ietf.org/html/rfc2898). PBKDF2 uses a pseudorandom function (PRF) and a salt to generate a hash. The PRF is a cryptographic function that takes a secret key and some input data and produces a pseudorandom output. PBKDF2 is computationally intensive, which makes it more resistant to brute-force attacks.

The following example shows how to hash a password using PBKDF2 in Kotlin:

```kotlin
import java.security.spec.KeySpec
import javax.crypto.SecretKeyFactory
import javax.crypto.spec.PBEKeySpec

fun main(args: Array<String>) {
    // The password to hash
    val password = "secret"

    // The salt
    val salt = byteArrayOf(0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f)

    // The number of iterations
    val iterations = 10000

    // The size of the derived key in bits
    val keySize = 256

    try {
        // Get the instance of the SecretKeyFactory
        val keyFactory = SecretKeyFactory.getInstance("PBKDF2WithHmacSHA1")

        // Generate the key
        val keySpec = PBEKeySpec(password.toCharArray(), salt, iterations, keySize)
        val secretKey = keyFactory.generateSecret(keySpec)

        // Get the key bytes
        val keyBytes = secretKey.encoded

        // Print the key
        println(keyBytes.toHexString())
    } catch (e: Exception) {
        println(e)
    }
}
```

## bcrypt

bcrypt is a hashing algorithm designed for passwords. It is based on the Blowfish cipher and uses a salt to make the hashes more difficult to crack. bcrypt is more computationally intensive than PBKDF2, which makes it even more resistant to brute-force attacks.

The following example shows how to hash a password using bcrypt in Kotlin:

```kotlin
import org.mindrot.jbcrypt.BCrypt

fun main(args: Array<String>) {
    // The password to hash
    val password = "secret"

    // The number of rounds
    val rounds = 10

    // The salt
    val salt = BCrypt.gensalt(rounds)

    // The hash
    val hash = BCrypt.hashpw(password, salt)

    // Print the hash
    println(hash)
}
```

## External resources

- [Kotlin cryptographic functions](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.crypto/-crypto-functions/)
- [Kotlin standard library](https://kotlinlang.org/api/latest/jvm/stdlib/)
- [Kotlin PBKDF2WithHmacSHA1](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.security/-p-b-k-d-f-2-with-hmac-s-h-a-1/)
- [Kotlin bcrypt](https://kotlinlang.org/api/latest/jvm/stdlib/org.mindrot/-bcrypt/)
- [bcrypt on Wikipedia](https://en.wikipedia.org/wiki/Bcrypt)
- [PBKDF2 on Wikipedia](https://en.wikipedia.org/wiki/PBKDF2)