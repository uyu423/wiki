---
title: 016: Manejo de excepciones en Kotlin: lanzar y capturar excepciones
description: 
published: true
date: 2023-02-05T10:17:20.882Z
tags: 
editor: markdown
dateCreated: 2023-02-05T10:17:19.269Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [016: Exception Handling in Kotlin: Throwing and Catching Exceptions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/016-exception-handling-in-kotlin-throwing-and-catching-exceptions)
{.links-list}


# Manejo de excepciones en Kotlin: lanzar y capturar excepciones

Las excepciones son eventos que ocurren durante la ejecución de un programa que interrumpen el flujo normal de instrucciones. Cuando se lanza una excepción, crea un objeto de excepción que contiene información sobre el error, como el tipo de excepción y el estado del programa cuando ocurrió el error.

Las excepciones pueden deberse a muchas cosas, incluidas, entre otras, las siguientes:

- Un error en el código.
- Entrada de usuario no válida
- Una falla de hardware

Hay dos tipos de excepciones en Kotlin: no verificadas y verificadas. Las excepciones no verificadas son aquellas que extienden la clase ```RuntimeException```, y las excepciones verificadas son aquellas que extienden la clase ```Exception```.

## Lanzamiento de excepciones

Las excepciones se pueden lanzar manualmente usando la palabra clave ```throw```. Esto es útil cuando desea abortar la ejecución de un programa debido a un error. Por ejemplo, digamos que tenemos una función que calcula el promedio de dos números. Si el usuario pasa una entrada no válida, queremos lanzar una excepción.

```kotlin
fun average(a: Int, b: Int): Double {
    if (a < 0 || b < 0) {
        throw IllegalArgumentException("Numbers must be positive.")
    }
    return (a + b) / 2.0
}
```

En el código anterior, lanzamos una ```IllegalArgumentException``` si las entradas son negativas. Ahora, si tratamos de llamar a la función ```promedio``` con números negativos, se lanzará una excepción y el programa se cancelará.

```kotlin
average(-1, 2) // Throws an IllegalArgumentException
```

## Captura de excepciones

Las excepciones se pueden detectar utilizando las palabras clave ```try```/```catch```. Esto es útil para manejar correctamente los errores y continuar con la ejecución del programa. Por ejemplo, digamos que queremos atrapar la excepción lanzada por nuestra función ```promedio``` e imprimir un mensaje de error al usuario.

```kotlin
fun average(a: Int, b: Int): Double {
    if (a < 0 || b < 0) {
        throw IllegalArgumentException("Numbers must be positive.")
    }
    return (a + b) / 2.0
}

fun main(args: Array<String>) {
    val a = -1
    val b = 2
    try {
        val avg = average(a, b)
        println("The average of $a and $b is $avg")
    } catch (e: IllegalArgumentException) {
        println("Error: ${e.message}")
    }
}
```

En el código anterior, captamos la ```IllegalArgumentException``` lanzada por nuestra función ```average```. Luego imprimimos un mensaje de error al usuario.

## Información adicional

- Las excepciones se pueden detectar utilizando las palabras clave ```try```/```catch```.
- Las excepciones se pueden lanzar manualmente usando la palabra clave ```throw```.
- Las excepciones no verificadas son aquellas que extienden la clase ```RuntimeException```.
- Las excepciones marcadas son aquellas que extienden la clase ```Exception```.