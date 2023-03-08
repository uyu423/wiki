---
title: Kotlin and AES: Encrypting and Decrypting Data
description: 
published: true
date: 2023-02-08T00:17:39.491Z
tags: 
editor: markdown
dateCreated: 2023-02-08T00:17:33.536Z
---

- [Kotlin y AES: Cifrado y descifrado de datos***Spanish** document is available*](/es/Knowledge-base/Kotlin/kotlin-and-aes-encrypting-and-decrypting-data)
{.links-list}
- [Kotlin 和 AES：加密和解密数据***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/kotlin-and-aes-encrypting-and-decrypting-data)
{.links-list}
- [Kotlin 및 AES: 데이터 암호화 및 복호화***Korean** document is available*](/ko/Knowledge-base/Kotlin/kotlin-and-aes-encrypting-and-decrypting-data)
{.links-list}


# Kotlin and AES: Encrypting and Decrypting Data

Kotlin is a powerful and versatile programming language that can be used for a wide range of tasks, including encrypting and decrypting data. In this article, we'll take a look at how to use Kotlin and the Advanced Encryption Standard (AES) to encrypt and decrypt data.

## What is AES?

AES is a symmetric-key algorithm that can be used to encrypt and decrypt data. AES is a widely used standard and is considered to be very secure.

## Encrypting data with Kotlin

To encrypt data with Kotlin, we'll use the ```javax.crypto.Cipher``` class. This class provides the functionality for encrypting and decrypting data.

We'll start by creating a ```Cipher``` instance. We'll use the ```getInstance()``` method, which takes the name of the algorithm to use as a parameter. For AES, we'll use the ```"AES/ECB/PKCS5Padding"``` algorithm. We'll also need to specify the mode and padding scheme to use.

Next, we'll create a ```SecretKey``` instance. AES requires a key that is 16, 24, or 32 bytes long. We'll use a 16-byte key for this example.

Once we have a ```Cipher``` and a ```SecretKey```, we can initialize the cipher for encryption by calling the ```init()``` method, passing in the ```Cipher.ENCRYPT_MODE``` parameter.

Now we're ready to encrypt our data. We'll call the ```doFinal()``` method, passing in the data to be encrypted. This method returns an array of bytes that contains the encrypted data.

Here's an example of how to encrypt data with Kotlin:

```kotlin
fun encrypt(data: String, key: String): ByteArray {
    val cipher = Cipher.getInstance("AES/ECB/PKCS5Padding")
    val secretKey = SecretKeySpec(key.toByteArray(), "AES")
    cipher.init(Cipher.ENCRYPT_MODE, secretKey)
    return cipher.doFinal(data.toByteArray())
}
```

## Decrypting data with Kotlin

To decrypt data with Kotlin, we'll use the same ```Cipher``` class that we used to encrypt the data.

First, we'll create a ```Cipher``` instance and a ```SecretKey``` instance, just as we did when we were encrypting the data.

Next, we'll initialize the cipher for decryption by calling the ```init()``` method, passing in the ```Cipher.DECRYPT_MODE``` parameter.

Now we're ready to decrypt our data. We'll call the ```doFinal()``` method, passing in the encrypted data. This method returns an array of bytes that contains the decrypted data.

Here's an example of how to decrypt data with Kotlin:

```kotlin
fun decrypt(data: ByteArray, key: String): String {
    val cipher = Cipher.getInstance("AES/ECB/PKCS5Padding")
    val secretKey = SecretKeySpec(key.toByteArray(), "AES")
    cipher.init(Cipher.DECRYPT_MODE, secretKey)
    return String(cipher.doFinal(data))
}
```

## AES in action

Now that we've seen how to encrypt and decrypt data with Kotlin and AES, let's put it into action with a simple example.

We'll start by creating a ```main()``` function. In this function, we'll create a ```String``` that contains the data that we want to encrypt. We'll also create a ```String``` that contains the key that we'll use to encrypt and decrypt the data.

Next, we'll call the ```encrypt()``` function that we created earlier, passing in the data and key. This function will return an array of bytes that contains the encrypted data.

Finally, we'll call the ```decrypt()``` function, passing in the encrypted data and key. This function will return a ```String``` that contains the decrypted data.

Here's the complete example:

```kotlin
fun main() {
    val data = "This is the data to encrypt"
    val key = "0123456789abcdef"
    val encryptedData = encrypt(data, key)
    val decryptedData = decrypt(encryptedData, key)
    println(decryptedData)
}
```

When we run this code, we'll see the following output:

```
This is the data to encrypt
```

## Conclusion

In this article, we've seen how to use Kotlin and AES to encrypt and decrypt data. We've also seen how to put it into action with a simple example.