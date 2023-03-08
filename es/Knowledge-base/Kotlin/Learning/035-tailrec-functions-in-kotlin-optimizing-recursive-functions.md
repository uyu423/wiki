---
title: 035: Funciones Tailrec en Kotlin: Optimización de funciones recursivas
description: 
published: true
date: 2023-02-16T09:32:34.425Z
tags: 
editor: markdown
dateCreated: 2023-02-16T09:32:26.423Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [035: Tailrec Functions in Kotlin: Optimizing Recursive Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/035-tailrec-functions-in-kotlin-optimizing-recursive-functions)
{.links-list}


# 035: Funciones Tailrec en Kotlin: Optimizando Funciones Recursivas

En esta publicación, veremos cómo usar las funciones tailrec en Kotlin para optimizar las funciones recursivas.

Las funciones recursivas son aquellas que se autodenominan, ya sea directa o indirectamente. Una función tailrec es un tipo especial de función recursiva en la que la última instrucción de la función es la llamada recursiva.

Las funciones de Tailrec son más eficientes que las funciones recursivas normales porque están compiladas para usar un bucle en lugar de realizar múltiples llamadas a funciones. Esto puede resultar en una mejora significativa del rendimiento, especialmente para las funciones recursivas que se llaman muchas veces.

Para crear una función tailrec en Kotlin, usamos la palabra clave tailrec antes del nombre de la función. Por ejemplo, aquí hay una función tailrec que calcula el factorial de un número dado:

```kotlin
tailrec fun factorial(n: Int, result: Int = 1): Int {
    if (n == 1) return result
    return factorial(n - 1, n * result)
}
```

En este ejemplo, usamos la palabra clave tailrec antes de la palabra clave fun. También hemos especificado el tipo de retorno de la función (Int) y le hemos dado a la función dos parámetros: n y resultado.

El parámetro de resultado tiene un valor predeterminado de 1, que se utiliza cuando se llama a la función por primera vez.

La función se llama a sí misma recursivamente hasta que el valor de n es 1. En ese punto, la función devuelve el valor de resultado.

Puedes ver cómo funciona esta función llamándola con diferentes valores:

```kotlin
factorial(5) // 120
factorial(10) // 3628800
```

Como puede ver, la función tailrec es una forma más eficiente de calcular el factorial de un número.

Existen algunas restricciones en las funciones de tailrec:

- La función debe ser miembro de una clase o un objeto.
- La función debe estar marcada con la palabra clave tailrec
- La función debe tener un solo parámetro
- La función debe llamarse a sí misma recursivamente
- La función debe devolver el mismo tipo que el parámetro

Si intenta crear una función tailrec que no cumpla con estos criterios, obtendrá un error de compilación.

## Información adicional

Aquí hay algunos recursos adicionales que pueden resultarle útiles:

- [Recursión de cola en Kotlin](https://kotlinlang.org/docs/reference/tail-recursion.html)
- [Optimización de llamadas de cola en Kotlin] (https://kotlinlang.org/docs/reference/tail-call-optimization.html)