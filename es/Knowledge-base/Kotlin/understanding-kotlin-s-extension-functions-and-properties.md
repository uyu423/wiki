---
title: Comprender las funciones y propiedades de extensión de Kotlin
description: 
published: true
date: 2023-02-02T03:36:28.555Z
tags: 
editor: markdown
dateCreated: 2023-02-02T03:36:26.957Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Understanding Kotlin's Extension Functions and Properties***English** document is available*](/en/Knowledge-base/Kotlin/understanding-kotlin-s-extension-functions-and-properties)
{.links-list}


# Comprender las funciones y propiedades de extensión de Kotlin

Kotlin es un poderoso lenguaje de programación que ofrece muchas características para hacer que el desarrollo sea más rápido y fácil. Una de estas características son las funciones y propiedades de extensión.

Las funciones y propiedades de extensión le permiten ampliar la funcionalidad de una clase sin tener que heredar de ella. Esto es especialmente útil cuando desea utilizar funciones de una biblioteca sin depender de esa biblioteca.

En este artículo, veremos más de cerca las funciones y propiedades de extensión en Kotlin. Aprenderemos cómo definirlos y cómo usarlos en nuestro propio código.

## Definición de funciones y propiedades de extensión

Las funciones y propiedades de extensión se definen utilizando las palabras clave `fun` y `val`, respectivamente. Se escriben después del nombre de la clase que están extendiendo, seguidos de un punto `.`:

```kotlin
// Extension function
fun String.repeat(times: Int): String {
    return this.repeat(times)
}

// Extension property
val String.length: Int
    get() = this.length
```

En el ejemplo anterior, hemos definido una función de extensión `repetir` que nos permite repetir una cadena un número determinado de veces. También hemos definido una propiedad de extensión `longitud` que nos permite obtener la longitud de una cadena.

Tenga en cuenta que las funciones y propiedades de extensión no están realmente definidas en la clase que están extendiendo. Se compilan como métodos y propiedades estáticos en la clase en la que están definidos. Esto significa que se pueden llamar desde cualquier lugar, incluso desde fuera de la clase.

## Uso de funciones y propiedades de extensión

Las funciones y propiedades de extensión se pueden usar como cualquier otra función o propiedad. En el siguiente ejemplo, usamos la función `repetir` para repetir una cadena 10 veces:

```kotlin
fun main() {
    val s = "Hello, world!".repeat(10)
    println(s)
}
```

También podemos usar la propiedad `longitud` para obtener la longitud de una cadena:

```kotlin
fun main() {
    val s = "Hello, world!"
    println(s.length)
}
```

## Anulación de funciones y propiedades de extensión

También es posible anular funciones y propiedades de extensión. Esto puede ser útil cuando desea cambiar el comportamiento de una función o propiedad en un contexto específico.

Para anular una función o propiedad de extensión, solo necesita definirla de la misma manera que lo haría con cualquier otra función o propiedad. En el siguiente ejemplo, anulamos la función `repetir` para que devuelva una cadena con el número dado de signos de exclamación:

```kotlin
fun main() {
    fun String.repeat(times: Int): String {
        return this + "!".repeat(times)
    }

    val s = "Hello, world!".repeat(10)
    println(s)
}
```

## Conclusión

Las funciones y propiedades de extensión son una característica poderosa en Kotlin que se puede usar para extender la funcionalidad de una clase sin tener que heredar de ella. Se definen usando las palabras clave `fun` y `val`, respectivamente, y se escriben después del nombre de la clase que están extendiendo, seguido de un punto `.`

Las funciones y propiedades de extensión se pueden usar como cualquier otra función o propiedad. Se compilan como métodos y propiedades estáticos, lo que significa que se pueden llamar desde cualquier lugar, incluso desde fuera de la clase.

También es posible anular funciones y propiedades de extensión. Esto puede ser útil cuando desea cambiar el comportamiento de una función o propiedad en un contexto específico.