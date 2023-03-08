---
title: 015: Tipos anulables y seguridad nula en Kotlin: manejo de valores nulos
description: 
published: true
date: 2023-02-16T04:32:56.531Z
tags: 
editor: markdown
dateCreated: 2023-02-16T04:32:54.824Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [015: Nullable Types and Null Safety in Kotlin: Dealing with Null Values***English** document is available*](/en/Knowledge-base/Kotlin/Learning/015-nullable-types-and-null-safety-in-kotlin-dealing-with-null-values)
{.links-list}


## Introducción

Kotlin es un lenguaje de programación de tipo estático que se ejecuta en la máquina virtual de Java. Es un lenguaje de propósito general diseñado para ser conciso, seguro e interoperable.

Una de las características clave de Kotlin es la seguridad nula. La seguridad nula es un mecanismo para evitar excepciones de puntero nulo. El sistema de tipos de Kotlin está diseñado para eliminar la posibilidad de referencias nulas del código.

Los tipos anulables son una forma de representar tipos que pueden ser nulos. En Kotlin, todos los tipos no aceptan valores NULL de forma predeterminada. Esto significa que una variable de tipo no nulo no puede contener un valor nulo.

Para crear un tipo anulable, usamos el signo de interrogación (?) después del nombre del tipo. Por ejemplo, el siguiente código define una variable de cadena anulable:

```kotlin
var str: String? = "Hello"
```

Ahora, la variable str puede contener un valor de cadena o un valor nulo.

Si intentamos asignar un valor nulo a una variable de tipo no nulo, obtendremos un error de compilación:

```kotlin
var str: String = "Hello"
str = null // error: null can not be a value of a non-null type String
```

Para arreglar esto, podemos cambiar el tipo de la variable str a un tipo anulable o usar una aserción no nula. Una aserción no nula es un operador que le dice al compilador que una variable no es nula. Lo usamos así:

```kotlin
var str: String = "Hello"
str = null // error: null can not be a value of a non-null type String

str!!.length // non-null assertion
```

El operador de aserción no nulo es un signo de exclamación doble (!!). Debe usarse solo cuando estamos seguros de que una variable no es nula. De lo contrario, obtendremos una excepción de tiempo de ejecución.

## Comprobación de nulo

En Kotlin, podemos verificar si una variable es nula usando la función `isNullOrEmpty()`:

```kotlin
fun main() {
    var str: String? = "Hello"
    if (str.isNullOrEmpty()) {
        println("str is null or empty")
    } else {
        println(str.length)
    }
}
```

La función `isNullOrEmpty()` devuelve verdadero si la cadena es nula o está vacía. De lo contrario, devuelve falso.

También podemos usar el operador `?` para verificar si una variable es nula:

```kotlin
fun main() {
    var str: String? = "Hello"
    val length = str?.length // str is not null, so length is not null
    println(length)
}
```

El operador `?` se denomina operador de llamada segura. Comprueba si la variable es nula antes de llamar a la propiedad de longitud. Si la variable es nula, devuelve nulo. De lo contrario, devuelve la longitud de la cadena.

Podemos usar el operador `?` para llamar a una función en una variable anulable:

```kotlin
fun main() {
    var str: String? = "Hello"
    str?.let {
        println(it.length) // it is not null, so we can call the length property
    }
}
```

La función `let` es una función de orden superior que toma una lambda como argumento. La lambda solo se ejecuta si la variable no es nula.

También podemos usar el operador `?` para ejecutar un bloque de código si una variable no es nula:

```kotlin
fun main() {
    var str: String? = "Hello"
    str?.let {
        println(it.length) // it is not null, so we can call the length property
    }
}
```

El operador `?` se denomina operador de llamada segura. Comprueba si la variable es nula antes de ejecutar la lambda. Si la variable es nula, no hace nada. De lo contrario, ejecuta la lambda.

## El operador Elvis

El operador Elvis es una forma de asignar un valor predeterminado a una variable anulable. Lo usamos así:

```kotlin
fun main() {
    var str: String? = "Hello"
    val length = str?.length ?: 0 // if str is null, length is 0
    println(length)
}
```

Si la variable `str` es nula, a la variable `longitud` se le asigna el valor 0. De lo contrario, se le asigna el valor de `str.length`.

El operador Elvis se usa a menudo con la función `let`:

```kotlin
fun main() {
    var str: String? = "Hello"
    str?.let {
        println(it.length) // it is not null, so we can call the length property
    } ?: println("str is null") // if str is null, print "str is null"
}
```

Si la variable `str` es nula, se ejecuta la sentencia `println("str is null")`. De lo contrario, se ejecuta la sentencia `println(it.length)`.

## El operador de aserción no nulo

El operador de aserción no nulo es una forma de decirle al compilador que una variable no es nula. Lo usamos así:

```kotlin
fun main() {
    var str: String? = "Hello"
    str!!.length // str is not null, so we can call the length property
}
```

El operador de aserción no nulo es un signo de exclamación doble (!!). Debe usarse solo cuando estamos seguros de que una variable no es nula. De lo contrario, obtendremos una excepción de tiempo de ejecución.

## El !! Operador

El !! El operador es una forma de decirle al compilador que una variable no es nula. Lo usamos así:

```kotlin
fun main() {
    var str: String? = "Hello"
    str!!.length // str is not null, so we can call the length property
}
```

El !! El operador es un signo de exclamación doble (!!). Debe usarse solo cuando estamos seguros de que una variable no es nula. De lo contrario, obtendremos una excepción de tiempo de ejecución.

## Conclusión

En este artículo, hemos aprendido sobre la seguridad nula en Kotlin. Hemos visto cómo usar tipos anulables y las diferentes formas de verificar valores nulos. También hemos visto cómo usar el operador Elvis y el operador de afirmación no nula.