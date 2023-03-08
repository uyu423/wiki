---
title: 051: La biblioteca estándar de Kotlin: uso de las funciones y clases integradas
description: 
published: true
date: 2023-02-16T17:33:09.967Z
tags: 
editor: markdown
dateCreated: 2023-02-16T17:33:07.860Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [051: The Kotlin Standard Library: Utilizing the Built-in Functions and Classes***English** document is available*](/en/Knowledge-base/Kotlin/Learning/051-the-kotlin-standard-library-utilizing-the-built-in-functions-and-classes)
{.links-list}


# La biblioteca estándar de Kotlin: uso de las funciones y clases integradas

Kotlin es un poderoso lenguaje de programación que se ejecuta en la máquina virtual de Java. Es un lenguaje de tipo estático que combina características de programación funcional y orientada a objetos. Kotlin es conocido por su interoperabilidad con Java, lo que lo convierte en una excelente opción para desarrollar aplicaciones de Android.

Una de las características más atractivas de Kotlin es su Biblioteca estándar, que contiene un amplio conjunto de funciones y clases que se pueden usar en su código de Kotlin. En esta publicación, veremos algunas de las funciones y clases más útiles en la biblioteca estándar de Kotlin.

## Colecciones Kotlin

Las colecciones de Kotlin son inmutables de forma predeterminada, lo que significa que no se pueden modificar una vez creadas. Esta es una gran característica porque ayuda a evitar errores que pueden ocurrir al modificar estructuras de datos. Kotlin también proporciona muchas funciones útiles para trabajar con colecciones, como `filter`, `map` y `reduce`.

Digamos que tenemos una lista de números y queremos filtrar los números pares. Podemos hacer esto con la función `filter`:

```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

val evenNumbers = numbers.filter { it % 2 == 0 }

println(evenNumbers) // prints [2, 4, 6, 8, 10]
```

También podemos usar la función `map` para transformar los elementos de una colección. Por ejemplo, si tenemos una lista de cadenas y queremos convertirlas a mayúsculas, podemos usar la función `mapa`:

```kotlin
val strings = listOf("a", "b", "c", "d", "e")

val uppercaseStrings = strings.map { it.toUpperCase() }

println(uppercaseStrings) // prints [A, B, C, D, E]
```

Finalmente, la función `reduce` se puede usar para combinar los elementos de una colección en un solo valor. Por ejemplo, si tenemos una lista de números y queremos calcular la suma de todos los números, podemos usar la función `reducir`:

```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

val sum = numbers.reduce { a, b -> a + b }

println(sum) // prints 55
```

Estas son solo algunas de las funciones útiles que están disponibles para trabajar con las colecciones de Kotlin. Para obtener una lista completa de funciones, consulte la [documentación de la biblioteca estándar de Kotlin] (https://kotlinlang.org/api/latest/jvm/stdlib/index.html).

## Cadenas Kotlin

Kotlin proporciona muchas funciones útiles para trabajar con cadenas. Por ejemplo, la función `trim` se puede usar para eliminar los espacios en blanco iniciales y finales de una cadena:

```kotlin
val s = "  hello world!  "

val trimmedString = s.trim()

println(trimmedString) // prints "hello world!"
```

La función `split` se puede usar para dividir una cadena en una lista de subcadenas, usando un delimitador específico:

```kotlin
val s = "a,b,c,d,e"

val substrings = s.split(",")

println(substrings) // prints ["a", "b", "c", "d", "e"]
```

La función `reemplazar` se puede usar para reemplazar todas las apariciones de una cadena específica con otra cadena:

```kotlin
val s = "hello world"

val replacedString = s.replace("hello", "goodbye")

println(replacedString) // prints "goodbye world"
```

Estas son solo algunas de las funciones útiles que están disponibles para trabajar con cadenas de Kotlin. Para obtener una lista completa de funciones, consulte la [documentación de la biblioteca estándar de Kotlin] (https://kotlinlang.org/api/latest/jvm/stdlib/index.html).

## Matemáticas Kotlin

La biblioteca estándar de Kotlin también proporciona algunas funciones matemáticas básicas. Por ejemplo, la función `abs` se puede utilizar para calcular el valor absoluto de un número:

```kotlin
val x = -10

val absoluteValue = kotlin.math.abs(x)

println(absoluteValue) // prints 10
```

Las funciones `max` y `min` se pueden utilizar para calcular el máximo y el mínimo de dos números, respectivamente:

```kotlin
val x = 10
val y = 20

val maximum = kotlin.math.max(x, y)
val minimum = kotlin.math.min(x, y)

println(maximum) // prints 20
println(minimum) // prints 10
```

Finalmente, la función `pow` se puede usar para calcular un número elevado a una potencia específica:

```kotlin
val x = 2.0
val y = 10

val xToTheY = kotlin.math.pow(x, y)

println(xToTheY) // prints 1024.0
```

Estas son solo algunas de las funciones útiles que están disponibles para trabajar con las matemáticas de Kotlin. Para obtener una lista completa de funciones, consulte la [documentación de la biblioteca estándar de Kotlin] (https://kotlinlang.org/api/latest/jvm/stdlib/index.html).

## Fechas y horarios de Kotlin

Kotlin proporciona un conjunto integral de funciones y clases para trabajar con fechas y horas. Por ejemplo, la función `ahora` se puede utilizar para obtener la fecha y la hora actuales:

```kotlin
val now = LocalDateTime.now()

println(now) // prints 2020-03-27T12:34:56.789
```

La función `parse` se puede usar para analizar una cadena en un objeto `LocalDate`:

```kotlin
val dateString = "2020-03-27"

val date = LocalDate.parse(dateString)

println(date) // prints 2020-03-27
```

La función `plusDays` se puede usar para agregar un número específico de días a un objeto `LocalDate`:

```kotlin
val date = LocalDate.now()

val tomorrow = date.plusDays(1)

println(tomorrow) // prints 2020-03-28
```

Estas son solo algunas de las funciones útiles que están disponibles para trabajar con fechas y horas de Kotlin. Para obtener una lista completa de funciones, consulte la [documentación de la biblioteca estándar de Kotlin] (https://kotlinlang.org/api/latest/jvm/stdlib/index.html).

## Conclusión

En esta publicación, echamos un vistazo a algunas de las funciones y clases más útiles en la biblioteca estándar de Kotlin. Hemos visto cómo las colecciones de Kotlin se pueden filtrar, mapear y reducir; cómo se pueden recortar, dividir y reemplazar las cadenas de Kotlin; y cómo se pueden usar las funciones matemáticas de Kotlin para calcular el valor absoluto, el máximo, el mínimo y la potencia de los números. También hemos visto cómo se pueden analizar, formatear y manipular las fechas y horas de Kotlin.

Para obtener más información sobre la biblioteca estándar de Kotlin, asegúrese de consultar la [documentación de la biblioteca estándar de Kotlin] (https://kotlinlang.org/api/latest/jvm/stdlib/index.html).