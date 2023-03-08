---
title: 100: Sistema de Tipos Avanzado en Kotlin: Explorando las Funciones Avanzadas del Sistema de Tipos de Kotlin.
description: 
published: true
date: 2023-02-06T13:18:00.521Z
tags: 
editor: markdown
dateCreated: 2023-02-06T13:17:54.916Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [100: Advanced Type System in Kotlin: Exploring the Advanced Features of the Kotlin Type System.***English** document is available*](/en/Knowledge-base/Kotlin/Learning/100-advanced-type-system-in-kotlin-exploring-the-advanced-features-of-the-kotlin-type-system-)
{.links-list}


Kotlin es un lenguaje de programación de tipo estático que se ejecuta en la máquina virtual de Java. Es un lenguaje de propósito general que se puede usar para desarrollar aplicaciones de Android, aplicaciones del lado del servidor y mucho más. El sistema de tipos de Kotlin está diseñado para ser flexible y ampliable, y es compatible con una serie de funciones avanzadas, como seguridad nula, inferencia de tipos y genéricos.

En esta publicación, exploraremos algunas de las funciones avanzadas del sistema de tipos de Kotlin. Aprenderemos sobre seguridad nula, inferencia de tipos, genéricos y constructores de seguridad de tipos. Al final de esta publicación, comprenderá bien el sistema de tipos de Kotlin y cómo usar sus funciones avanzadas para escribir código seguro y legible.

## Seguridad nula

Una de las características más importantes del sistema de tipo Kotlin es la seguridad nula. El sistema de seguridad nulo de Kotlin está diseñado para evitar que ocurran excepciones de puntero nulo. En Kotlin, todos los tipos no aceptan valores NULL de forma predeterminada. Esto significa que no puede asignar un valor nulo a una variable de ningún tipo. Si intenta hacerlo, obtendrá un error de compilación.

Para hacer que un tipo sea anulable, debe usar el modificador de tipo anulable. Por ejemplo, el siguiente código define una variable de cadena anulable:

```kotlin
var s: String? = "foo"
```

Ahora, la variable s puede contener un valor de cadena no nulo o un valor nulo. Si intenta asignar un valor nulo a una variable que no acepta valores NULL, volverá a obtener un error del compilador.

Para verificar si una variable anulable es nula, puede usar la función `isNullOrEmpty()`:

```kotlin
if (s.isNullOrEmpty()) {
    // s is null or empty
}
```

Si desea acceder al valor de una variable anulable, debe utilizar el operador `?.`. Este operador comprobará si la variable es nula antes de acceder a su valor. Por ejemplo, el siguiente código imprimirá "foo" si s no es nulo y "bar" si s es nulo:

```kotlin
println(s?.length ?: "bar")
```

También puede usar el operador `!!` para forzar el desenvolvimiento de una variable anulable. Esto lanzará una excepción si la variable es nula. Por ejemplo, el siguiente código generará una excepción si s es nulo:

```kotlin
println(s!!.length)
```

## Tipo de inferencia

El sistema de inferencia de tipos de Kotlin está diseñado para inferir automáticamente el tipo de una variable a partir de su expresión inicializadora. Por ejemplo, el siguiente código define una variable de tipo Int:

```kotlin
val x = 1
```

Aquí, se deduce que el tipo de la variable x es Int de la expresión del inicializador. El sistema de inferencia de tipos de Kotlin es muy potente y, a menudo, puede inferir el tipo de una variable incluso cuando la expresión inicializadora es compleja.

## Genéricos

Los genéricos son una característica poderosa del sistema de tipos de Kotlin que le permite definir código seguro para tipos. Los genéricos le permiten parametrizar tipos, de modo que pueda escribir código que funcione con cualquier tipo. Por ejemplo, el siguiente código define una función genérica que toma una lista de cualquier tipo e imprime sus elementos:

```kotlin
fun <T> printList(list: List<T>) {
    for (element in list) {
        println(element)
    }
}
```

Aquí, el parámetro de tipo T se utiliza para parametrizar el tipo de la lista. Esta función se puede utilizar para imprimir una lista de cualquier tipo, por ejemplo, una lista de Ints:

```kotlin
val list = listOf(1, 2, 3)
printList(list)
```

Kotlin también te permite definir tus propios tipos genéricos. Por ejemplo, el siguiente código define una clase genérica que se puede usar para crear una lista de cualquier tipo:

```kotlin
class List<T> {
    fun add(element: T) {
        // ...
    }

    fun get(index: Int): T {
        // ...
    }
}
```

Esta clase se puede utilizar para crear una lista de cualquier tipo, por ejemplo, una lista de cadenas:

```kotlin
val list = List<String>()
list.add("foo")
list.add("bar")
println(list.get(0)) // prints "foo"
```

## Constructores de tipo seguro

Los constructores con seguridad de tipos de Kotlin son una característica poderosa que le permite escribir código con seguridad de tipos al crear estructuras de datos complejas. Por ejemplo, el siguiente código define un constructor con seguridad de tipos para una lista de cadenas:

```kotlin
fun buildStringList(builder: StringListBuilder.() -> Unit): List<String> {
    val stringListBuilder = StringListBuilder()
    stringListBuilder.builder()
    return stringListBuilder.toList()
}

class StringListBuilder {
    private val list = mutableListOf<String>()

    fun add(string: String) {
        list.add(string)
    }

    fun toList(): List<String> {
        return list
    }
}
```

Este constructor se puede utilizar para crear una lista de cadenas de la siguiente manera:

```kotlin
val list = buildStringList {
    add("foo")
    add("bar")
}
```

Los constructores con seguridad de tipos de Kotlin son una excelente manera de escribir código seguro y legible al crear estructuras de datos complejas.