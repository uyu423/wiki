---
title: Hashing de Kotlin y PBKDF2: temas avanzados
description: 
published: true
date: 2023-02-04T22:17:21.175Z
tags: 
editor: markdown
dateCreated: 2023-02-04T22:17:19.558Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin and PBKDF2 Hashing: Advanced Topics***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-pbkdf2-hashing-advanced-topics)
{.links-list}


# Hashing de Kotlin y PBKDF2: temas avanzados

En este artículo, analizaremos el hash de Kotlin y PBKDF2 con más profundidad. Cubriremos temas como qué es PBKDF2, cómo funciona y cómo usarlo en Kotlin. También proporcionaremos algunos ejemplos de código para ilustrar estos conceptos.

## ¿Qué es PBKDF2?

PBKDF2 (Función de derivación de clave basada en contraseña 2) es una función de derivación de clave que forma parte de la serie de estándares criptográficos de clave pública (PKCS) de RSA Laboratories. Fue publicado en 2000 como PKCS # 5 v2.0.

PBKDF2 es una forma segura de derivar una clave de una contraseña. Toma como entrada una contraseña, una sal y una serie de iteraciones. Luego ejecuta la contraseña a través de una función hash, como SHA-256, varias veces. El número de iteraciones es configurable y se puede aumentar para que el cálculo sea más costoso y, por lo tanto, más seguro.

La salida de PBKDF2 es una matriz de bytes que se puede usar como clave para el cifrado u otros fines.

## ¿Cómo funciona PBKDF2?

La idea básica detrás de PBKDF2 es ejecutar la contraseña a través de una función hash varias veces. Esto hace que sea más costoso de computar y, por lo tanto, más seguro.

 PBKDF2 se define en RFC 2898, que se puede encontrar aquí: https://tools.ietf.org/html/rfc2898.

El algoritmo es como sigue:

```
PBKDF2(P, S, c, dkLen)

Input:

P: The password, as a byte array.

S: A salt, as a byte array.

c: The number of iterations to perform.

dkLen: The length of the derived key, in bytes.

Output:

A derived key, as a byte array.

1. Initialize a byte array D with the dkLen bytes set to 0.

2. Set U0 = PRF(P, S || 0x00), where PRF is a pseudorandom function.

3. For i = 1, 2, ..., c:

   Set Ui = PRF(P, Ui-1).

   Set D = D || Ui.

4. Return D.
```

## Cómo usar PBKDF2 en Kotlin

Kotlin no tiene una biblioteca integrada para PBKDF2, pero hay varias bibliotecas de terceros que se pueden usar. En este ejemplo, usaremos la biblioteca "KotlinPBKDF2", que se puede encontrar aquí: https://github.com/ajalt/kotlin-pbkdf2

Para usar esta biblioteca, agregue la siguiente dependencia a su archivo build.gradle:

```
compile 'com.github.ajalt:kotlin-pbkdf2:1.0.0'
```

Luego, puede usar la función PBKDF2 de la siguiente manera:

```kotlin
val password = "password"
val salt = "salt"
val iterations = 1000
val keyLength = 32

val derivedKey = PBKDF2(password, salt, iterations, keyLength)
```

## Conclusión

En este artículo, hemos discutido el hashing de Kotlin y PBKDF2 con más profundidad. Hemos cubierto temas como qué es PBKDF2, cómo funciona y cómo usarlo en Kotlin. También proporcionamos algunos ejemplos de código para ilustrar estos conceptos.