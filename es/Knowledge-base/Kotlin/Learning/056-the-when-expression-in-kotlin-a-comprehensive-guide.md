---
title: 056: La expresión When en Kotlin: una guía completa
description: 
published: true
date: 2023-02-16T19:17:32.134Z
tags: 
editor: markdown
dateCreated: 2023-02-16T19:17:30.010Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [056: The When Expression in Kotlin: A Comprehensive Guide***English** document is available*](/en/Knowledge-base/Kotlin/Learning/056-the-when-expression-in-kotlin-a-comprehensive-guide)
{.links-list}


## Introducción

La expresión when de Kotlin es una herramienta poderosa que se puede usar para hacer coincidir una variedad de diferentes tipos de datos. En esta guía, veremos cómo usar la expresión when en Kotlin y exploraremos algunas de sus funciones más avanzadas.

## Uso básico

La expresión when es el equivalente de Kotlin de la instrucción switch en otros idiomas. Le permite hacer coincidir un valor y ejecutar un bloque de código basado en ese valor.

Aquí hay un ejemplo simple:

```kotlin
when (x) {
    1 -> println("x is 1")
    2 -> println("x is 2")
    else -> println("x is neither 1 nor 2")
}
```

En este ejemplo, estamos haciendo coincidir el valor de la variable `x`. Si `x` es igual a `1`, se ejecutará el bloque de código asociado con ese caso. De manera similar, si `x` es igual a `2`, se ejecutará el bloque de código asociado con ese caso. Si `x` no es ni `1` ni `2`, se ejecutará el bloque de código asociado con el caso `else`.

Es importante tener en cuenta que no se requiere el caso `else`. Si omite el caso `else`, la expresión when no coincidirá con ningún valor que no esté explícitamente enumerado en los otros casos:

```kotlin
when (x) {
    1 -> println("x is 1")
    2 -> println("x is 2")
}
```

En este ejemplo, si `x` no es ni `1` ni `2`, el bloque de código asociado con el caso `else` no se ejecutará.

## Coincidencia de tipos

Además de hacer coincidir valores, la expresión when también se puede usar para hacer coincidir tipos. Esto es particularmente útil cuando se trabaja con tipos anulables.

Considere el siguiente ejemplo:

```kotlin
fun process(value: Any) {
    when (value) {
        is String -> println(value.length)
        is Int -> println(value * 2)
        else -> println("I don't know what this is")
    }
}
```

En este ejemplo, tenemos una función que toma un tipo `Cualquiera` y lo procesa de alguna manera. Usamos la expresión when para hacer coincidir el tipo del parámetro `value`.

Si `value` es una `String`, imprimimos su longitud. Si `value` es un `Int`, imprimimos su valor multiplicado por 2. Si `value` no es ni una `String` ni un `Int`, imprimimos un mensaje que dice que no sabemos qué es .

También puede usar la expresión when para hacer coincidir los tipos que aceptan valores NULL. Esto es útil para evitar la temida `NullPointerException`.

Considere el siguiente ejemplo:

```kotlin
fun process(value: Any?) {
    when (value) {
        is String -> println(value.length)
        is Int -> println(value * 2)
        null -> println("value is null")
        else -> println("I don't know what this is")
    }
}
```

En este ejemplo, hemos cambiado el tipo del parámetro `value` de `Any` a `Any?`. Esto hace que el parámetro sea anulable, lo que significa que ahora puede tomar el valor `null`.

Hemos agregado un caso a la expresión when para manejar el valor `null`. Si `value` es `null`, imprimimos un mensaje que lo dice.

Es importante tener en cuenta que el caso `null` debe ir antes del caso `else`. Esto se debe a que el caso `else` coincidirá con cualquier valor, incluido `null`.

Si el caso `null` estuviera después del caso `else`, nunca se ejecutaría.

## Conclusión

En esta guía, hemos echado un vistazo a cómo usar la expresión when en Kotlin. Hemos visto cómo hacer coincidir valores y tipos, y también hemos visto cómo manejar tipos que aceptan valores NULL.