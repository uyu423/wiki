---
title: Kotlin y Hashing: Protección de contraseñas y datos confidenciales
description: 
published: true
date: 2023-02-06T14:17:39.236Z
tags: 
editor: markdown
dateCreated: 2023-02-06T14:17:33.596Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin and Hashing: Securing Passwords and Sensitive Data***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-hashing-securing-passwords-and-sensitive-data)
{.links-list}


# Kotlin y Hashing: Protección de contraseñas y datos confidenciales

Con el auge de Kotlin como lenguaje para el desarrollo de Android, es importante saber cómo proteger adecuadamente las contraseñas y los datos confidenciales en sus aplicaciones. En este artículo, discutiremos cómo usar hash para proteger esta información.

## ¿Qué es Hashing?

Hashing es un proceso de mapeo de datos de tamaño arbitrario a datos de un tamaño fijo. Los datos de tamaño fijo se denominan valor hash, código hash, resumen hash o simplemente hash. El valor hash se genera utilizando un algoritmo hash, que puede ser un algoritmo simple como sumar los bytes de los datos o un algoritmo más complejo como SHA-256.

## ¿Por qué usar hashing?

Hashing es un proceso unidireccional, lo que significa que no es posible revertir el proceso para recuperar los datos originales. Esto es importante para la seguridad porque significa que incluso si alguien obtiene el valor hash, no podrá determinar cuáles eran los datos originales.

## Cómo usar hash en Kotlin

Kotlin proporciona una función hash integrada llamada `hashCode()`. Esta función toma un objeto arbitrario y devuelve un valor hash `Int`. Por ejemplo, podemos codificar un `String` como este:

```kotlin
val hashValue = "password".hashCode()
```

La función `hashCode()` no es adecuada para propósitos criptográficos porque es posible generar el mismo valor hash para diferentes datos. Por ejemplo, las cadenas "contraseña" y "CONTRASEÑA" tienen el mismo valor hash.

Si necesitamos generar un valor hash criptográfico, podemos usar la clase `MessageDigest` de la biblioteca Java Cryptography Extension (JCE). Kotlin proporciona una función de extensión para `MessageDigest` llamada `digest()` que facilita su uso:

```kotlin
import java.security.MessageDigest

fun MessageDigest.digest(data: ByteArray): ByteArray {
    update(data)
    return digest()
}
```

Con esta función, podemos calcular un hash SHA-256 como este:

```kotlin
val data = "password".toByteArray()
val sha256 = MessageDigest.getInstance("SHA-256")
val hashValue = sha256.digest(data)
```

## Cómo almacenar hashes

Es importante almacenar hashes de forma segura para evitar que los atacantes puedan determinar cuáles eran los datos originales. Una forma de hacer esto es usar una sal, que es una cadena aleatoria que se agrega a los datos antes de que se conviertan en hash. La sal se almacena junto con el valor hash y se usa para verificar si una contraseña determinada es correcta.

La clase `MessageDigest` tiene una función `update(salt: ByteArray)` que se puede usar para agregar una sal a los datos antes de que se conviertan en hash. Por ejemplo:

```kotlin
val data = "password".toByteArray()
val salt = "somesalt".toByteArray()

val sha256 = MessageDigest.getInstance("SHA-256")
sha256.update(salt)
val hashValue = sha256.digest(data)
```

## Cómo comprobar si una contraseña es correcta

Para verificar si una contraseña determinada es correcta, debemos calcular el hash de la contraseña y compararlo con el valor hash almacenado. Si coinciden, entonces la contraseña es correcta.

Una forma de hacer esto es usar la clase `MessageDigest` nuevamente. Podemos calcular el hash de la contraseña de esta manera:

```kotlin
val password = "password"
val hashValue = "hashValue".toByteArray()

val sha256 = MessageDigest.getInstance("SHA-256")
sha256.update(hashValue)
val passwordHash = sha256.digest(password.toByteArray())
```

Luego, podemos comparar `passwordHash` con el valor hash almacenado para ver si coinciden.

Otra forma de hacer esto es usar la función `hashCode()`. Podemos calcular el hash de la contraseña de esta manera:

```kotlin
val password = "password"
val hashValue = "hashValue".toByteArray()

val passwordHash = password.hashCode()
```

Luego, podemos comparar `passwordHash` con el valor hash almacenado para ver si coinciden.

## Conclusión

En este artículo, hemos discutido cómo usar hash para proteger contraseñas y datos confidenciales en las aplicaciones de Kotlin. Hemos visto cómo calcular hashes usando las funciones `hashCode()` y `MessageDigest` y cómo almacenar y verificar hashes usando un salt.