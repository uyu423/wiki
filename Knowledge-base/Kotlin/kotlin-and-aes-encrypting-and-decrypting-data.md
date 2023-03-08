---
title: Kotlin 및 AES: 데이터 암호화 및 복호화
description: 
published: true
date: 2023-02-08T00:17:35.093Z
tags: 
editor: markdown
dateCreated: 2023-02-08T00:17:33.533Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and AES: Encrypting and Decrypting Data***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-aes-encrypting-and-decrypting-data)
{.links-list}


# Kotlin과 AES: 데이터 암호화 및 복호화

Kotlin은 데이터 암호화 및 암호 해독을 포함하여 광범위한 작업에 사용할 수 있는 강력하고 다재다능한 프로그래밍 언어입니다. 이 기사에서는 Kotlin 및 AES(Advanced Encryption Standard)를 사용하여 데이터를 암호화 및 복호화하는 방법을 살펴보겠습니다.

## AES란?

AES는 데이터를 암호화하고 해독하는 데 사용할 수 있는 대칭 키 알고리즘입니다. AES는 널리 사용되는 표준이며 매우 안전한 것으로 간주됩니다.

## Kotlin으로 데이터 암호화

Kotlin으로 데이터를 암호화하기 위해 ```javax.crypto.Cipher``` 클래스를 사용합니다. 이 클래스는 데이터를 암호화하고 해독하는 기능을 제공합니다.

```kotlin
fun encrypt(data: String, key: String): ByteArray {
    val cipher = Cipher.getInstance("AES/ECB/PKCS5Padding")
    val secretKey = SecretKeySpec(key.toByteArray(), "AES")
    cipher.init(Cipher.ENCRYPT_MODE, secretKey)
    return cipher.doFinal(data.toByteArray())
}
```SecretKey``` 인스턴스를 생성합니다. AES에는 16, 24 또는 32바이트 길이의 키가 필요합니다. 이 예에서는 16바이트 키를 사용합니다.

```kotlin
fun decrypt(data: ByteArray, key: String): String {
    val cipher = Cipher.getInstance("AES/ECB/PKCS5Padding")
    val secretKey = SecretKeySpec(key.toByteArray(), "AES")
    cipher.init(Cipher.DECRYPT_MODE, secretKey)
    return String(cipher.doFinal(data))
}
```doFinal()``` 메서드를 호출하여 암호화할 데이터를 전달합니다. 이 메서드는 암호화된 데이터가 포함된 바이트 배열을 반환합니다.

다음은 Kotlin으로 데이터를 암호화하는 방법의 예입니다.

```kotlin
fun main() {
    val data = "This is the data to encrypt"
    val key = "0123456789abcdef"
    val encryptedData = encrypt(data, key)
    val decryptedData = decrypt(encryptedData, key)
    println(decryptedData)
}
```

## Kotlin으로 데이터 복호화

Kotlin으로 데이터를 해독하기 위해 데이터를 암호화하는 데 사용한 것과 동일한 ```Cipher``` 클래스를 사용합니다.

먼저 데이터를 암호화할 때와 마찬가지로 ```Cipher``` 인스턴스와 ```SecretKey``` 인스턴스를 생성합니다.

다음으로 ```Cipher.DECRYPT_MODE``` 매개변수를 전달하여 ```init()``` 메서드를 호출하여 암호 해독을 위해 암호를 초기화합니다.

이제 데이터를 해독할 준비가 되었습니다. ```doFinal()``` 메서드를 호출하여 암호화된 데이터를 전달합니다. 이 메서드는 해독된 데이터가 포함된 바이트 배열을 반환합니다.

다음은 Kotlin으로 데이터를 복호화하는 방법의 예입니다.

```
This is the data to encrypt
```

## AES 작동 중

Kotlin과 AES로 데이터를 암호화하고 복호화하는 방법을 살펴보았으니 간단한 예를 들어 실행해 보겠습니다.

```main()``` 함수를 만드는 것으로 시작하겠습니다. 이 함수에서는 암호화하려는 데이터가 포함된 ```String```을 생성합니다. 또한 데이터를 암호화하고 해독하는 데 사용할 키가 포함된 ```String```도 생성합니다.

다음으로 이전에 생성한 ```encrypt()``` 함수를 호출하여 데이터와 키를 전달합니다. 이 함수는 암호화된 데이터가 포함된 바이트 배열을 반환합니다.

마지막으로 ```decrypt()``` 함수를 호출하여 암호화된 데이터와 키를 전달합니다. 이 함수는 해독된 데이터를 포함하는 ```String```을 반환합니다.

전체 예제는 다음과 같습니다.

```코틀린
재미있는 메인() {
    val data = "암호화할 데이터입니다."
    값 키 = "0123456789abcdef"
    val encryptionData = 암호화(데이터, 키)
    val decryptedData = decrypt(encryptedData, 키)
    println(복호화된 데이터)
}
```

이 코드를 실행하면 다음과 같은 결과가 표시됩니다.

```
암호화할 데이터입니다.
```

## 결론

이 기사에서는 Kotlin과 AES를 사용하여 데이터를 암호화하고 해독하는 방법을 살펴보았습니다. 또한 간단한 예를 통해 이를 실행에 옮기는 방법도 살펴보았습니다.