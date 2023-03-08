---
title: 004: Flujo de control en Kotlin: declaraciones if-else, bucles y expresiones when
description: 
published: true
date: 2023-02-16T01:33:00.836Z
tags: 
editor: markdown
dateCreated: 2023-02-16T01:32:59.169Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [004: Control Flow in Kotlin: if-else Statements, Loops, and When Expressions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/004-control-flow-in-kotlin-if-else-statements-loops-and-when-expressions)
{.links-list}


# Flujo de control en Kotlin: declaraciones if-else, bucles y expresiones when

Kotlin proporciona un conjunto integral de construcciones de flujo de control. En esta publicación, veremos cómo usar declaraciones if-else, bucles y expresiones when en Kotlin.

## Declaraciones if-else

Las declaraciones if-else se utilizan para ejecutar un determinado bloque de código solo si se cumple una determinada condición. La forma general de una declaración if-else en Kotlin es la siguiente:

```kotlin
if (condition) {
    // Execute this block if the condition is true
} else {
    // Execute this block if the condition is false
}
```

Veamos algunos ejemplos de cómo usar declaraciones if-else en Kotlin.

### Ejemplo 1

En este ejemplo, usaremos una instrucción if-else para imprimir si un número es positivo o negativo.

```kotlin
fun main(args: Array<String>) {
    val num = 5

    if (num > 0) {
        println("$num is positive")
    } else {
        println("$num is negative")
    }
}
```

Producción:

```
5 is positive
```

### Ejemplo 2

En este ejemplo, usaremos una instrucción if-else para imprimir el mayor de dos números.

```kotlin
fun main(args: Array<String>) {
    val num1 = 5
    val num2 = 10

    if (num1 > num2) {
        println("$num1 is larger than $num2")
    } else {
        println("$num2 is larger than $num1")
    }
}
```

Producción:

```
10 is larger than 5
```

## Bucles

Los bucles se utilizan para ejecutar un determinado bloque de código varias veces. Kotlin proporciona tres tipos diferentes de bucles: bucles for, bucles while y bucles do-while.

### para bucles

Los bucles for se utilizan para iterar sobre un rango de valores o una matriz de valores. La forma general de un bucle for en Kotlin es la siguiente:

```kotlin
for (variable in range) {
    // Execute this block for each value in the range
}
```

Veamos algunos ejemplos de cómo usar bucles for en Kotlin.

### Ejemplo 1

En este ejemplo, usaremos un ciclo for para imprimir los primeros 10 números naturales.

```kotlin
fun main(args: Array<String>) {
    for (i in 1..10) {
        println(i)
    }
}
```

Producción:

```
1
2
3
4
5
6
7
8
9
10
```

### Ejemplo 2

En este ejemplo, usaremos un bucle for para imprimir los elementos de una matriz.

```kotlin
fun main(args: Array<String>) {
    val array = arrayOf(1, 2, 3, 4, 5)

    for (element in array) {
        println(element)
    }
}
```

Producción:

```
1
2
3
4
5
```

### bucles while

Los bucles while se utilizan para ejecutar un determinado bloque de código varias veces hasta que se cumpla una determinada condición. La forma general de un ciclo while en Kotlin es la siguiente:

```kotlin
while (condition) {
    // Execute this block while the condition is true
}
```

Veamos algunos ejemplos de cómo usar bucles while en Kotlin.

### Ejemplo 1

En este ejemplo, usaremos un ciclo while para imprimir los primeros 10 números naturales.

```kotlin
fun main(args: Array<String>) {
    var i = 1

    while (i <= 10) {
        println(i)
        i++
    }
}
```

Producción:

```
1
2
3
4
5
6
7
8
9
10
```

### Ejemplo 2

En este ejemplo, usaremos un ciclo while para sumar los primeros 10 números naturales.

```kotlin
fun main(args: Array<String>) {
    var i = 1
    var sum = 0

    while (i <= 10) {
        sum += i
        i++
    }

    println("The sum of the first 10 natural numbers is $sum")
}
```

Producción:

```
The sum of the first 10 natural numbers is 55
```

### bucles do-while

Los bucles do-while se utilizan para ejecutar un determinado bloque de código varias veces hasta que se cumpla una determinada condición. La forma general de un bucle do-while en Kotlin es la siguiente:

```kotlin
do {
    // Execute this block at least once
} while (condition)
```

Veamos algunos ejemplos de cómo usar bucles do-while en Kotlin.

### Ejemplo 1

En este ejemplo, usaremos un bucle do-while para imprimir los primeros 10 números naturales.

```kotlin
fun main(args: Array<String>) {
    var i = 1

    do {
        println(i)
        i++
    } while (i <= 10)
}
```

Producción:

```
1
2
3
4
5
6
7
8
9
10
```

### Ejemplo 2

En este ejemplo, usaremos un bucle do-while para sumar los primeros 10 números naturales.

```kotlin
fun main(args: Array<String>) {
    var i = 1
    var sum = 0

    do {
        sum += i
        i++
    } while (i <= 10)

    println("The sum of the first 10 natural numbers is $sum")
}
```

Producción:

```
The sum of the first 10 natural numbers is 55
```

## Cuando Expresiones

Cuando se utilizan expresiones para ejecutar un determinado bloque de código en función de un determinado valor. La forma general de una expresión when en Kotlin es la siguiente:

```kotlin
when (value) {
    value1 -> {
        // Execute this block when the value is value1
    }
    value2 -> {
        // Execute this block when the value is value2
    }
    // ...
    else -> {
        // Execute this block when the value is none of the above
    }
}
```

Veamos algunos ejemplos de cómo usar las expresiones when en Kotlin.

### Ejemplo 1

En este ejemplo, usaremos una expresión when para imprimir el significado de un determinado color.

```kotlin
fun main(args: Array<String>) {
    val color = "red"

    when (color) {
        "red" -> println("Red is the color of blood")
        "blue" -> println("Blue is the color of the sky")
        "green" -> println("Green is the color of grass")
        else -> println("I don't know the meaning of that color")
    }
}
```

Producción:

```
Red is the color of blood
```

### Ejemplo 2

En este ejemplo, usaremos una expresión when para imprimir la calificación de un estudiante en función de su puntuación.

```kotlin
fun main(args: Array<String>) {
    val score = 95

    when (score) {
        in 90..100 -> println("You got an A!")
        in 80..89 -> println("You got a B!")
        in 70..79 -> println("You got a C!")
        in 60..69 -> println("You got a D!")
        else -> println("You got an F!")
    }
}
```

Producción:

```
You got an A!
```

## Conclusión

En esta publicación, hemos visto cómo usar declaraciones if-else, bucles y expresiones when en Kotlin. Todas estas son construcciones de flujo de control importantes que necesitará saber para escribir programas de Kotlin.