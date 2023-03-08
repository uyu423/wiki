---
title: 034: funciones vararg en Kotlin: creación de funciones que aceptan un número variable de argumentos
description: 
published: true
date: 2023-02-13T18:55:41.900Z
tags: 
editor: markdown
dateCreated: 2023-02-13T18:55:40.244Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [034: vararg Functions in Kotlin: Creating Functions that Accept a Variable Number of Arguments***English** document is available*](/en/Knowledge-base/Kotlin/Learning/034-vararg-functions-in-kotlin-creating-functions-that-accept-a-variable-number-of-arguments)
{.links-list}


# Funciones vararg en Kotlin: creación de funciones que aceptan un número variable de argumentos

La palabra clave vararg de Kotlin nos permite crear funciones que aceptan un número variable de argumentos. Esto puede ser útil cuando queremos escribir una función que pueda tomar cualquier cantidad de argumentos, sin tener que especificar explícitamente la cantidad de argumentos en la definición de la función.

En esta publicación, aprenderemos cómo crear funciones vararg en Kotlin y cómo usarlas en nuestro código. También veremos algunos ejemplos de cómo se pueden usar las funciones vararg para simplificar nuestro código.

## Crear una función Vararg

Para crear una función vararg en Kotlin, usamos la palabra clave vararg antes del nombre del parámetro en la definición de la función. Por ejemplo, supongamos que queremos crear una función que tome un número variable de cadenas y las imprima. Podríamos hacer esto con la siguiente definición de función:

```kotlin
fun printStrings(vararg strings: String) {
    for (string in strings) {
        println(string)
    }
}
```

Observe que hemos colocado la palabra clave vararg antes del parámetro de cadenas. Esto le dice a Kotlin que la función puede tomar cualquier cantidad de argumentos de cadena.

Podemos llamar a esta función con cualquier cantidad de argumentos de cadena, y todos se imprimirán:

```kotlin
printStrings("Hello", "World") // Prints "Hello" and "World"
printStrings("Kotlin", "is", "awesome") // Prints "Kotlin", "is", and "awesome"
```

También podemos llamar a la función sin argumentos, en cuyo caso no se imprimirá nada:

```kotlin
printStrings() // Prints nothing
```

## Acceso a los parámetros de Vararg

Cuando creamos una función vararg, podemos acceder a los parámetros vararg en el cuerpo de la función como cualquier otro parámetro. En la función printStrings() anterior, accedimos al parámetro de cadenas en un bucle for para imprimir todas las cadenas.

También podemos acceder a los parámetros vararg fuera del cuerpo de la función. Para hacer esto, usamos el operador * antes del nombre del parámetro cuando llamamos a la función. Por ejemplo, digamos que tenemos una función vararg que toma un número variable de enteros y los imprime:

```kotlin
fun printInts(vararg ints: Int) {
    for (int in ints) {
        println(int)
    }
}
```

Podemos llamar a esta función con cualquier cantidad de argumentos enteros, y todos se imprimirán:

```kotlin
printInts(1, 2, 3) // Prints 1, 2, and 3
printInts(4, 5, 6, 7, 8) // Prints 4, 5, 6, 7, and 8
```

También podemos llamar a la función sin argumentos, en cuyo caso no se imprimirá nada:

```kotlin
printInts() // Prints nothing
```

Ahora digamos que tenemos una matriz de números enteros y queremos imprimirlos todos usando la función printInts(). Podemos hacer esto usando el operador * para "descomprimir" la matriz en argumentos individuales:

```kotlin
val intArray = intArrayOf(1, 2, 3)
printInts(*intArray) // Prints 1, 2, and 3
```

## Parámetros Vararg y Non-Vararg

También podemos crear funciones vararg que tengan parámetros vararg y no vararg. Por ejemplo, digamos que queremos crear una función que tome un número variable de cadenas y un número entero, e imprima las cadenas una cantidad de veces igual al número entero:

```kotlin
fun printStringsNTimes(n: Int, vararg strings: String) {
    for (i in 1..n) {
        for (string in strings) {
            println(string)
        }
    }
}
```

En esta función, tenemos un parámetro no vararg (n) y un parámetro vararg (cadenas). Podemos llamar a esta función con cualquier cantidad de argumentos de cadena, y todos se imprimirán n veces:

```kotlin
printStringsNTimes(3, "Hello", "World") // Prints "Hello" and "World" three times
printStringsNTimes(5, "Kotlin", "is", "awesome") // Prints "Kotlin", "is", and "awesome" five times
```

También podemos llamar a la función sin argumentos de cadena, en cuyo caso no se imprimirá nada:

```kotlin
printStringsNTimes(3) // Prints nothing
```

## Conclusión

En esta publicación, aprendimos cómo crear funciones vararg en Kotlin y cómo usarlas en nuestro código. También vimos algunos ejemplos de cómo se pueden usar las funciones vararg para simplificar nuestro código.

Si desea obtener más información sobre Kotlin, consulte la documentación de Kotlin.