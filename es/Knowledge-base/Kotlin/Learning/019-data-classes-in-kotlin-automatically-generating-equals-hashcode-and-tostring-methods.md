---
title: 019: Clases de datos en Kotlin: generación automática de métodos Equals, HashCode y ToString
description: 
published: true
date: 2023-02-12T01:55:23.425Z
tags: 
editor: markdown
dateCreated: 2023-02-12T01:55:21.802Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [019: Data Classes in Kotlin: Automatically Generating Equals, HashCode, and ToString Methods***English** document is available*](/en/Knowledge-base/Kotlin/Learning/019-data-classes-in-kotlin-automatically-generating-equals-hashcode-and-tostring-methods)
{.links-list}


# Clases de datos en Kotlin: generación automática de métodos Equals, HashCode y ToString

Kotlin es un lenguaje de programación de tipo estático que se ejecuta en la máquina virtual de Java. Es un lenguaje de propósito general diseñado para ser conciso, seguro e interoperable.

Una de las características que hace que Kotlin se destaque es su soporte para clases de datos. Una clase de datos es una clase que está diseñada para contener datos. En Kotlin, las clases de datos vienen con una gran cantidad de funciones integradas, incluida la capacidad de generar métodos equals(), hashCode() y toString() automáticamente.

En esta publicación, veremos cómo usar las clases de datos en Kotlin y cómo generar automáticamente los métodos equals(), hashCode() y toString().

## Crear una clase de datos

Para crear una clase de datos, usamos la palabra clave data:

```kotlin
data class User(val name: String, val age: Int)
```

Esto crea una clase de datos con dos propiedades: nombre y edad. También podemos crear clases de datos con propiedades mutables:

```kotlin
data class User(var name: String, var age: Int)
```

Las clases de datos también pueden tener constructores secundarios:

```kotlin
data class User(val name: String, val age: Int) {
    constructor(name: String) : this(name, 0)
}
```

## Generación de métodos Equals y HashCode

De forma predeterminada, las clases de datos en Kotlin generan métodos equals() y hashCode(). Estos métodos comparan los datos en dos clases de datos y devuelven verdadero si son iguales.

Aquí hay un ejemplo de cómo funciona el método equals():

```kotlin
val user1 = User("John", 30)
val user2 = User("John", 30)

println(user1 == user2) // true
```

En este ejemplo, tenemos dos clases de datos con las mismas propiedades de nombre y edad. Cuando los comparamos usando el operador ==, se llama al método equals() y devuelve verdadero.

Si cambiamos una de las propiedades, el método equals() devolverá falso:

```kotlin
val user1 = User("John", 30)
val user2 = User("John", 31)

println(user1 == user2) // false
```

## Generando un método toString()

Las clases de datos en Kotlin también generan un método toString(). Este método se utiliza para convertir los datos de una clase de datos en una cadena.

Aquí hay un ejemplo de cómo funciona el método toString():

```kotlin
val user = User("John", 30)

println(user.toString()) // User(name=John, age=30)
```

Como puede ver, el método toString() imprime los datos de la clase de datos en un formato legible.

## Conclusión

En esta publicación, analizamos las clases de datos en Kotlin y cómo generar automáticamente los métodos equals(), hashCode() y toString(). Las clases de datos son una excelente manera de crear código conciso y seguro.