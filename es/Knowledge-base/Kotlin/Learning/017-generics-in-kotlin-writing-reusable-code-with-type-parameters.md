---
title: 017: Genéricos en Kotlin: escribir código reutilizable con parámetros de tipo
description: 
published: true
date: 2023-02-02T02:57:44.940Z
tags: 
editor: markdown
dateCreated: 2023-02-02T02:57:43.262Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [017: Generics in Kotlin: Writing Reusable Code with Type Parameters***English** document is available*](/en/Knowledge-base/Kotlin/Learning/017-generics-in-kotlin-writing-reusable-code-with-type-parameters)
{.links-list}


# Genéricos en Kotlin: escribir código reutilizable con parámetros de tipo

El sistema de tipos de Kotlin está diseñado para ayudarte a hacer más con menos código. Una de las formas en que lo hace es permitiéndole escribir código genérico o reutilizable en una variedad de tipos. En esta publicación, veremos cómo funcionan los genéricos en Kotlin y cómo puedes usarlos para escribir código más conciso y expresivo.

## ¿Qué son los genéricos?

Los genéricos son una característica de muchos lenguajes de programación que le permiten escribir código que puede funcionar con varios tipos. Esto se opone al código que es específico de un tipo, como `Int` o `String`.

Uno de los ejemplos más comunes de genéricos es el tipo `Lista`. Una `Lista` puede contener elementos de cualquier tipo, por lo que se dice que es _genérica_. En Kotlin, podemos crear una `Lista` de `Int`s como esta:

```kotlin
val list: List<Int> = listOf(1, 2, 3)
```

También podemos crear una `Lista` de `String`s:

```kotlin
val list: List<String> = listOf("a", "b", "c")
```

Como puede ver, lo único que cambia entre estas dos 'Listas' es el tipo de elementos que contienen. El tipo `Lista` en sí mismo es genérico.

## ¿Por qué usar genéricos?

Los genéricos son útiles porque le permiten escribir código que se puede usar con varios tipos. Esto puede hacer que su código sea más conciso y expresivo.

Por ejemplo, considere el siguiente código que imprime los elementos de una `Lista`:

```kotlin
fun printList(list: List<Any>) {
    for (element in list) {
        println(element)
    }
}
```

Este código funcionará con cualquier `Lista`, independientemente del tipo de sus elementos. Podemos usarlo para imprimir una `Lista` de `Int`s:

```kotlin
val list: List<Int> = listOf(1, 2, 3)
printList(list)
```

Y podemos usarlo para imprimir una `Lista` de `String`s:

```kotlin
val list: List<String> = listOf("a", "b", "c")
printList(list)
```

Si no usáramos genéricos, tendríamos que escribir dos funciones diferentes, una para `List`s de `Int`s y otra para `List`s de `String`s. Los genéricos nos permiten escribir una función que se puede usar con varios tipos.

## ¿Cómo funcionan los genéricos?

Los genéricos en Kotlin se implementan mediante _tipo de parámetros_. Un parámetro de tipo es un marcador de posición para un tipo específico. Cuando crea un tipo genérico, especifica uno o más parámetros de tipo. Por ejemplo, el tipo `Lista` tiene un parámetro de tipo llamado `T`.

Cuando crea una instancia de un tipo genérico, especifica el tipo por el que se debe reemplazar el parámetro de tipo. Por ejemplo, cuando creamos una `List<Int>`, estamos especificando que el parámetro de tipo `T` debería ser reemplazado por el tipo `Int`.

## Uso de parámetros de tipo

Los parámetros de tipo se pueden utilizar de varias formas. El más común es especificar el tipo de los elementos de una colección. Por ejemplo, el tipo `Lista` tiene un parámetro de tipo que especifica el tipo de los elementos en la `Lista`.

Ya hemos visto cómo usar parámetros de tipo para especificar el tipo de los elementos en una `Lista`. También podemos usar parámetros de tipo para especificar el tipo de claves y valores en un `Mapa`:

```kotlin
val map: Map<String, Int> = mapOf("a" to 1, "b" to 2, "c" to 3)
```

En este ejemplo, hemos especificado que el tipo de las claves en el 'Mapa' debe ser 'Cadena' y el tipo de los valores debe ser 'Int'.

Los parámetros de tipo también se pueden usar para especificar el tipo de los valores en un tipo `Anulable`:

```kotlin
val nullable: String? = null
```

En este ejemplo, hemos especificado que el tipo del valor en el tipo `Nullable` debería ser `String`.

## Declaración de parámetros de tipo

Cuando crea un tipo genérico, especifica uno o más parámetros de tipo. Por ejemplo, el tipo `Lista` tiene un parámetro de tipo llamado `T`.

Puede declarar parámetros de tipo utilizando la palabra clave `typeparam`. Por ejemplo, podemos crear un tipo genérico llamado `MyType` con un parámetro de tipo llamado `T` como este:

```kotlin
typealias MyType<T> = T
```

## Límites

A veces, es posible que desee restringir los tipos que se pueden usar como parámetro de tipo. Por ejemplo, es posible que desee especificar que el parámetro de tipo debe ser un subtipo de `Cualquiera`. Kotlin llama a esto un _límite superior_.

Puede especificar un límite superior utilizando la palabra clave `where`. Por ejemplo, podemos crear un tipo genérico llamado "MiTipo" con un parámetro de tipo llamado "T" que tiene un límite superior de "Cualquiera" como este:

```kotlin
typealias MyType<T> where T : Any
```

En este ejemplo, hemos especificado que el parámetro de tipo `T` debe ser un subtipo de `Any`. Esto significa que podemos usar cualquier tipo como parámetro de tipo `T`, incluidos `Int`, `String`, `List`, etc.

También podemos especificar un límite inferior usando la palabra clave `where`. Por ejemplo, podemos crear un tipo genérico llamado "MiTipo" con un parámetro de tipo llamado "T" que tiene un límite inferior de "Cualquiera" como este:

```kotlin
typealias MyType<T> where T : Any
```

En este ejemplo, especificamos que el parámetro de tipo `T` debe ser un supertipo de `Any`. Esto significa que podemos usar cualquier tipo como parámetro de tipo `T`, incluidos `Any`, `Any?`, etc.

## Comodines

En ocasiones, es posible que desee utilizar un parámetro de tipo sin especificar su tipo. Por ejemplo, es posible que desee crear una función que pueda imprimir los elementos de cualquier 'Lista'.

En Kotlin, puedes usar un _comodín_ para especificar que un parámetro de tipo puede ser de cualquier tipo. Por ejemplo, podemos crear una función que imprima los elementos de cualquier `Lista` como esta:

```kotlin
fun printList(list: List<*>) {
    for (element in list) {
        println(element)
    }
}
```

En este ejemplo, hemos usado un comodín para especificar que el parámetro de tipo `T` puede ser de cualquier tipo. Esto significa que podemos usar la función `imprimirLista` con cualquier `Lista`, independientemente del tipo de sus elementos.

## Conclusión

En esta publicación, echamos un vistazo a cómo funcionan los genéricos en Kotlin. Hemos visto cómo usar parámetros de tipo para escribir código más conciso y expresivo. También hemos visto cómo declarar parámetros de tipo y cómo usar límites y comodines.