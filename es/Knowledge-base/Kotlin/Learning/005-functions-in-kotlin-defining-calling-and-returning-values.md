---
title: 005: Funciones en Kotlin: definición, llamada y devolución de valores
description: 
published: true
date: 2023-02-16T02:32:24.050Z
tags: 
editor: markdown
dateCreated: 2023-02-16T02:32:22.071Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [005: Functions in Kotlin: Defining, Calling, and Returning Values***English** document is available*](/en/Knowledge-base/Kotlin/Learning/005-functions-in-kotlin-defining-calling-and-returning-values)
{.links-list}


# Funciones en Kotlin: definición, llamada y devolución de valores

La función es un conjunto de código que realiza una tarea específica. En Kotlin, podemos definir nuestras propias funciones para que se llamen más tarde cuando necesitemos realizar esa tarea. En esta publicación, aprenderemos cómo definir funciones, llamarlas y devolver valores de ellas.

## Definición de funciones

En Kotlin, definimos funciones usando la palabra clave ```fun```. Por ejemplo, digamos que queremos definir una función que imprima un mensaje de saludo. Podemos hacerlo así:

```kotlin
fun printGreeting() {
    println("Hello, world!")
}
```

También podemos definir funciones que toman argumentos. Por ejemplo, digamos que queremos definir una función que imprima un mensaje de saludo con un nombre. Podemos hacerlo así:

```kotlin
fun printGreeting(name: String) {
    println("Hello, $name!")
}
```

También podemos definir funciones que devuelvan valores. Por ejemplo, digamos que queremos definir una función que calcule la suma de dos números. Podemos hacerlo así:

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

## Funciones de llamada

Llamamos funciones simplemente usando sus nombres seguidos de paréntesis ```()```. Por ejemplo, podemos llamar a la función ```printGreeting()``` que definimos anteriormente de esta manera:

```kotlin
printGreeting() // prints "Hello, world!"
```

Si definimos una función que toma argumentos, necesitamos pasar los argumentos entre paréntesis ```()```. Por ejemplo, podemos llamar a la función ```printGreeting(name: String)``` que definimos anteriormente de esta manera:

```kotlin
printGreeting("John") // prints "Hello, John!"
```

Si definimos una función que devuelve un valor, necesitamos almacenar el valor devuelto en una variable. Por ejemplo, podemos llamar a la función ```sum(a: Int, b: Int): Int``` que definimos anteriormente así:

```kotlin
val result = sum(1, 2) // result is 3
```

## Valores devueltos

Como vimos en la sección anterior, podemos definir funciones que devuelvan valores. En Kotlin, usamos la palabra clave ```return``` para devolver un valor de una función. Por ejemplo, digamos que queremos definir una función que calcule la suma de dos números y devuelva el resultado. Podemos hacerlo así:

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

También podemos devolver valores sin usar explícitamente la palabra clave ```return```. Por ejemplo, digamos que queremos definir una función que calcule la suma de dos números y devuelva el resultado. Podemos hacerlo así:

```kotlin
fun sum(a: Int, b: Int): Int = a + b
```

En el último ejemplo, devolvemos el valor de ```a + b``` simplemente asignándolo al nombre de función ```sum```.

¡Eso es todo por esta publicación! En resumen, aprendimos cómo definir funciones, llamarlas y devolver valores de ellas.