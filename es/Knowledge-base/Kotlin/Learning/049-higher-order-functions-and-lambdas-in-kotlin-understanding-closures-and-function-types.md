---
title: 049: Funciones de orden superior y Lambdas en Kotlin: comprensión de cierres y tipos de funciones
description: 
published: true
date: 2023-02-16T15:32:43.720Z
tags: 
editor: markdown
dateCreated: 2023-02-16T15:32:41.059Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [049: Higher-Order Functions and Lambdas in Kotlin: Understanding Closures and Function Types***English** document is available*](/en/Knowledge-base/Kotlin/Learning/049-higher-order-functions-and-lambdas-in-kotlin-understanding-closures-and-function-types)
{.links-list}


# 049: Funciones de orden superior y Lambdas en Kotlin: comprensión de cierres y tipos de funciones

En esta publicación, veremos funciones de orden superior y lambdas en Kotlin. Aprenderemos qué son y cómo usarlos, así como también comprenderemos algunos de los conceptos detrás de ellos, como cierres y tipos de funciones.

## ¿Qué son las funciones de orden superior y las lambdas?

En Kotlin, una función de orden superior es una función que toma una o más funciones como argumentos o devuelve una función como resultado. Las lambdas son un tipo de función anónima, lo que significa que no tienen nombre.

Echemos un vistazo a un ejemplo simple de una función de orden superior que toma una lambda como argumento. Esta función toma una lambda que toma un Int y devuelve un valor booleano, y devuelve una lista de todos los Ints que devuelven verdadero cuando se pasan a la lambda:

```kotlin
fun filter(predicate: (Int) -> Boolean): List<Int> {
    val list = mutableListOf<Int>()
    for (i in 1..10) {
        if (predicate(i)) {
            list.add(i)
        }
    }
    return list
}
```

Podemos llamar a esta función así:

```kotlin
val evenNumbers = filter { it % 2 == 0 }
```

La palabra clave it en la lambda es un marcador de posición para el argumento que se pasa a la lambda. En este caso, representa el Int que se pasa a la función de filtro.

## ¿Qué son los cierres?

Un cierre es una función que captura el estado de su entorno circundante. En otras palabras, puede acceder a variables desde el ámbito en el que se definió.

Aquí hay un ejemplo simple de un cierre en Kotlin. Tenemos una variable llamada contador y una función que incrementa el contador y devuelve el nuevo valor. Esta función es un cierre porque captura el estado de la variable contador:

```kotlin
var counter = 0
fun incrementCounter(): Int {
    return ++counter
}
```

Si llamamos a la función incrementCounter varias veces, realizará un seguimiento del valor actual de la variable contador y devolverá el nuevo valor cada vez:

```kotlin
incrementCounter() // returns 1
incrementCounter() // returns 2
incrementCounter() // returns 3
```

## ¿Qué son los tipos de funciones?

En Kotlin, cada función tiene un tipo. El tipo de una función se compone de los tipos de argumentos que toma la función y el tipo del valor que devuelve la función.

Por ejemplo, el tipo de la función incrementCounter de la sección anterior es (() -> Int). Esto se puede leer como "una función que no toma argumentos y devuelve un Int".

El tipo de función de filtro de la primera sección es ((Int) -> Boolean) -> List<Int>. Esto se puede leer como "una función que toma una función que toma un Int y devuelve un Boolean, y devuelve una Lista de Ints".

Los tipos de funciones son importantes en Kotlin porque nos permiten especificar con qué tipo de funciones queremos trabajar. Por ejemplo, podemos escribir una función de orden superior que tome una función con el tipo (Int) -> Boolean y devuelva una lista de todos los Ints que devuelven verdadero cuando se pasan a la función:

```kotlin
fun filter(predicate: (Int) -> Boolean): List<Int> {
    val list = mutableListOf<Int>()
    for (i in 1..10) {
        if (predicate(i)) {
            list.add(i)
        }
    }
    return list
}
```

Podemos llamar a esta función así:

```kotlin
val evenNumbers = filter { it % 2 == 0 }
```

La palabra clave it en la lambda es un marcador de posición para el argumento que se pasa a la lambda. En este caso, representa el Int que se pasa a la función de filtro.

## Conclusión

En esta publicación, hemos aprendido sobre funciones de orden superior y lambdas en Kotlin. Hemos visto cómo usarlos y también hemos aprendido sobre algunos de los conceptos detrás de ellos, como cierres y tipos de funciones.