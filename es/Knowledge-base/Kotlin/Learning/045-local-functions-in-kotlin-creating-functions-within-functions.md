---
title: 045: Funciones locales en Kotlin: creación de funciones dentro de funciones
description: 
published: true
date: 2023-02-02T01:43:44.834Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:43:43.190Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [045: Local Functions in Kotlin: Creating Functions Within Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/045-local-functions-in-kotlin-creating-functions-within-functions)
{.links-list}


# Funciones locales en Kotlin: creación de funciones dentro de funciones

Cuando estás escribiendo código en Kotlin, a menudo querrás crear una función dentro de otra función. Esto se llama una **función local**. Las funciones locales son útiles porque pueden acceder a las variables de la función externa, lo que significa que pueden usarse para simplificar código complejo.

En esta publicación, veremos cómo crear funciones locales en Kotlin. También discutiremos algunos de los beneficios de usar funciones locales.

## Definición de funciones locales

Una función local se define dentro del cuerpo de otra función. Aquí hay un ejemplo:

```kotlin
fun outerFunction() {
    fun localFunction() {
        // Code goes here
    }
}
```

Como puede ver, la función local se define dentro del cuerpo de la función externa. Es importante tener en cuenta que la función local solo se puede llamar desde la función externa. Esto significa que la función local tiene **alcance local**.

También vale la pena señalar que las funciones locales pueden acceder a las variables de la función externa. Esto se debe a que las funciones locales están **anidadas** dentro de la función externa. Aquí hay un ejemplo:

```kotlin
fun outerFunction() {
    val outerVariable = " outer"

    fun localFunction() {
        println(outerVariable) // Prints " outer"
    }
}
```

Como puede ver, la función local puede acceder a la variable `outerVariable`, que se define en la función externa.

## Llamar a funciones locales

Las funciones locales solo se pueden llamar desde dentro de la función en la que están definidas. Esto significa que tienen **alcance local**. Aquí hay un ejemplo:

```kotlin
fun outerFunction() {
    fun localFunction() {
        // Code goes here
    }

    localFunction() // Calls the local function
}
```

Como puede ver, la función local se llama desde dentro de la función externa. Si intentamos llamar a la función local desde fuera de la función externa, obtendremos un error:

```kotlin
fun outerFunction() {
    fun localFunction() {
        // Code goes here
    }
}

localFunction() // Error: localFunction is not defined
```

## Beneficios de las funciones locales

Las funciones locales son útiles porque pueden acceder a las variables de la función externa. Esto significa que se pueden usar para simplificar código complejo.

Por ejemplo, digamos que tenemos una función que calcula el factorial de un número. El factorial de un número es el producto de todos los enteros positivos menores o iguales que el número. Por ejemplo, el factorial de 5 es 5 * 4 * 3 * 2 * 1, que es 120.

Así es como podríamos escribir una función para calcular el factorial de un número en Kotlin:

```kotlin
fun factorial(n: Int): Int {
    if (n == 0) {
        return 1
    }

    return n * factorial(n - 1)
}
```

Esta función usa **recursión**, que es una técnica para escribir funciones que se llaman a sí mismas.

El problema con esta función es que **no es recursiva en la cola**. Esto significa que la función se llama a sí misma varias veces antes de devolver un resultado. Esto puede generar errores de **desbordamiento de pila**, que ocurren cuando la función se llama a sí misma tantas veces que la pila se desborda.

Podemos resolver este problema usando una función local:

```kotlin
fun factorial(n: Int): Int {
    tailrec fun factorial(acc: Int, n: Int): Int {
        if (n == 0) {
            return acc
        }

        return factorial(acc * n, n - 1)
    }

    return factorial(1, n)
}
```

Esta función es **recursiva de cola**, lo que significa que la función se llama a sí misma solo una vez antes de devolver un resultado. Esto significa que la función se puede llamar con valores grandes de `n` sin encontrarse con errores de desbordamiento de pila.

## Conclusión

En esta publicación, hemos visto cómo crear funciones locales en Kotlin. También hemos discutido algunos de los beneficios de usar funciones locales.

Las funciones locales son útiles porque pueden acceder a las variables de la función externa. Esto significa que se pueden usar para simplificar código complejo.

Si está interesado en obtener más información sobre las funciones locales, le recomiendo leer los siguientes recursos:

- La documentación de Kotlin sobre [funciones locales] (https://kotlinlang.org/docs/reference/local-functions.html)
- Una publicación de blog sobre [recursión y recursión de cola en Kotlin](https://blog.kotlin-academy.com/recursion-and-tail-recursion-in-kotlin-f79bc55a326a)
- Una publicación de blog sobre [los beneficios de las funciones locales] (https://blog.kotlin-academy.com/the-benefits-of-local-functions-f79bc55a326a)