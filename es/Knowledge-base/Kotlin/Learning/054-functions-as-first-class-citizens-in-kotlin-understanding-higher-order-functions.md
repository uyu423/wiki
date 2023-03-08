---
title: 054: Funciones como ciudadanos de primera clase en Kotlin: comprensión de las funciones de orden superior
description: 
published: true
date: 2023-02-16T18:33:04.065Z
tags: 
editor: markdown
dateCreated: 2023-02-16T18:32:55.841Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [054: Functions as First-Class Citizens in Kotlin: Understanding Higher-Order Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/054-functions-as-first-class-citizens-in-kotlin-understanding-higher-order-functions)
{.links-list}


## Introducción

Kotlin es un lenguaje de programación moderno que se ejecuta en la máquina virtual de Java. Es un lenguaje de tipo estático que combina las mejores características de la programación funcional y orientada a objetos.

Kotlin es un ciudadano de primera clase en JVM, lo que significa que se puede usar para desarrollar cualquier tipo de aplicación Java, desde simples programas de línea de comandos hasta aplicaciones web complejas.

Una de las características más importantes de Kotlin es que admite funciones de orden superior. En este artículo, aprenderemos qué son las funciones de orden superior y cómo usarlas en Kotlin.

## ¿Qué es una función de orden superior?

Una función de orden superior es una función que toma una o más funciones como argumentos y devuelve una función como resultado.

En Kotlin, las funciones de orden superior están representadas por el tipo ```Function<T, R>```. Este tipo tiene dos parámetros de tipo:

- ```T``` es el tipo de argumento de la función.
- ```R``` es el tipo del resultado de la función.

El tipo ```Function<T, R>``` se puede usar para representar cualquier función que tome un argumento de tipo ```T``` y devuelva un resultado de tipo ```R```.

## Cómo usar funciones de orden superior en Kotlin

Hay muchas funciones integradas de orden superior en Kotlin que están disponibles para su uso. En esta sección, aprenderemos cómo usar algunas de las funciones de orden superior más utilizadas.

### La función ```mapa```

La función ```map``` es una función de orden superior que toma una función como argumento y la aplica a cada elemento de una lista.

Por ejemplo, supongamos que tenemos una lista de cadenas y queremos convertirlas a mayúsculas. Podemos hacer esto usando la función ```map```:

```kotlin
val list = listOf("a", "b", "c")

val upperCaseList = list.map { it.toUpperCase() }

// upperCaseList is now a list of strings: ["A", "B", "C"]
```

En el ejemplo anterior, tenemos una lista de cadenas y usamos la función ```map``` para aplicar la función ```toUpperCase()``` a cada elemento de la lista.

La función ```map``` se puede usar con cualquier tipo de lista, no solo con listas de cadenas. Por ejemplo, podemos usar ```map``` con una lista de enteros:

```kotlin
val list = listOf(1, 2, 3)

val doubleList = list.map { it * 2 }

// doubleList is now a list of integers: [2, 4, 6]
```

### La función ```filtro```

La función ```filter``` es una función de orden superior que toma una función como argumento y la aplica a cada elemento de una lista. La función debe devolver ```verdadero``` o ```falso```.

La función ```filter``` devolverá una nueva lista que contiene solo los elementos para los que la función devuelve ```true```.

Por ejemplo, supongamos que tenemos una lista de cadenas y queremos filtrar todas las cadenas que tienen más de tres caracteres. Podemos hacer esto usando la función ```filter```:

```kotlin
val list = listOf("a", "ab", "abc", "abcd")

val filteredList = list.filter { it.length <= 3 }

// filteredList is now a list of strings: ["a", "ab", "abc"]
```

En el ejemplo anterior, tenemos una lista de cadenas y usamos la función ```filter``` para eliminar todas las cadenas que tienen más de tres caracteres.

La función ```filter``` se puede usar con cualquier tipo de lista, no solo con listas de cadenas. Por ejemplo, podemos usar ```filter``` con una lista de enteros:

```kotlin
val list = listOf(1, 2, 3, 4, 5)

val filteredList = list.filter { it % 2 == 0 }

// filteredList is now a list of integers: [2, 4]
```

En el ejemplo anterior, tenemos una lista de números enteros y usamos la función ```filter``` para eliminar todos los números impares.

### La función ```reduce```

La función ```reduce``` es una función de orden superior que toma una función como argumento y la aplica a cada elemento de una lista. La función debe tomar dos argumentos y devolver un solo valor.

La función ```reduce``` devolverá un único valor que es el resultado de aplicar la función a cada elemento de la lista.

Por ejemplo, supongamos que tenemos una lista de números enteros y queremos encontrar la suma de todos los elementos de la lista. Podemos hacer esto usando la función ```reduce```:

```kotlin
val list = listOf(1, 2, 3, 4, 5)

val sum = list.reduce { a, b -> a + b }

// sum is now 15
```

En el ejemplo anterior, tenemos una lista de enteros y usamos la función ```reduce``` para encontrar la suma de todos los elementos de la lista.

La función ```reduce``` se puede usar con cualquier tipo de lista, no solo con listas de enteros. Por ejemplo, podemos usar ```reduce``` con una lista de cadenas:

```kotlin
val list = listOf("a", "b", "c")

val concatenatedString = list.reduce { a, b -> a + b }

// concatenatedString is now "abc"
```

En el ejemplo anterior, tenemos una lista de cadenas y usamos la función ```reduce``` para concatenar todas las cadenas en una sola cadena.

## Conclusión

En este artículo, hemos aprendido qué son las funciones de orden superior y cómo usarlas en Kotlin. Hemos visto cómo usar las funciones ```map```, ```filter``` y ```reduce``` para transformar y manipular listas.

Las funciones de orden superior son una herramienta poderosa que se puede utilizar para escribir código conciso y legible. Si eres nuevo en Kotlin, te animo a experimentar con funciones de orden superior y ver qué se te ocurre.