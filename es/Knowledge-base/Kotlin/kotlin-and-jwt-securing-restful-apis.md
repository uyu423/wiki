---
title: Kotlin y JWT: Protección de las API RESTful
description: 
published: true
date: 2023-02-13T15:17:46.683Z
tags: 
editor: markdown
dateCreated: 2023-02-13T15:17:44.941Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin and JWT: Securing RESTful APIs***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-jwt-securing-restful-apis)
{.links-list}


# Kotlin y JWT: Protección de las API RESTful

Con el auge de Kotlin como un lenguaje de primera clase para desarrollar aplicaciones de Android, no sorprende que cada vez más desarrolladores estén interesados en usar Kotlin también para el desarrollo del lado del servidor. En este artículo, veremos cómo usar Kotlin y el marco Java Web Tokens (JWT) para asegurar una API RESTful.

JWT es un estándar para crear tokens de acceso que permiten a los servidores verificar la identidad de los clientes. Esto es especialmente importante en una API RESTful, donde los clientes pueden ser cualquier cosa, desde una aplicación móvil hasta una extensión de navegador. Al usar JWT, podemos estar seguros de que solo los clientes autorizados pueden acceder a nuestra API.

Para usar JWT con Kotlin, necesitaremos instalar la biblioteca kotlin-jwt. Esta biblioteca proporciona un conjunto de funciones para crear y verificar tokens JWT.

Una vez que tengamos instalada la biblioteca kotlin-jwt, podemos usarla para crear un token JWT como este:

```kotlin
val jwt = JWT.create()
    .withSubject("user@example.com")
    .withExpiresAt(Date())
    .sign(algorithm)
```

donde `algorithm` es una instancia de `Algorithm` que especifica el algoritmo de firma a utilizar. Por ejemplo, podríamos usar el algoritmo `HMAC256` así:

```kotlin
val algorithm = Algorithm.HMAC256("secret")
```

Entonces podemos usar la variable `jwt` para generar un token:

```kotlin
val token = jwt.generate()
```

Ahora que tenemos un token, podemos usarlo para proteger nuestra API. Por ejemplo, podemos agregarlo al encabezado `Autorización` de nuestras solicitudes HTTP:

```kotlin
val request = Request.Builder()
    .url("https://example.com/api/v1/users")
    .header("Authorization", "Bearer $token")
    .build()
```

El servidor puede usar la función `verificar` para verificar el token:

```kotlin
val jwt = JWT.require(algorithm)
    .build()

val verifiedToken = jwt.verify(token)
```

Si el token es válido, la variable `verifiedToken` contendrá el token decodificado. Luego podemos usar la función `getSubject` para obtener la dirección de correo electrónico del usuario:

```kotlin
val userEmail = verifiedToken.getSubject()
```

Ahora que sabemos cómo usar Kotlin y JWT para asegurar una API RESTful, veamos algunos recursos para leer más.

## Recursos

- [Tokens web JSON](https://jwt.io/)
- [kotlin-jwt](https://github.com/kotlinc-es/kotlin-jwt)
- [Seguridad de Kotlin](https://kotlinlang.org/docs/reference/security.html)