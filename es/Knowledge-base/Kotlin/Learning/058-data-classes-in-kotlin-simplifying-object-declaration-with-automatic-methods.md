---
title: 058: Clases de datos en Kotlin: simplificación de la declaración de objetos con métodos automáticos
description: 
published: true
date: 2023-02-15T21:55:38.429Z
tags: 
editor: markdown
dateCreated: 2023-02-15T21:55:36.352Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [058: Data Classes in Kotlin: Simplifying Object Declaration with Automatic Methods***English** document is available*](/en/Knowledge-base/Kotlin/Learning/058-data-classes-in-kotlin-simplifying-object-declaration-with-automatic-methods)
{.links-list}


# Clases de datos en Kotlin: simplificación de la declaración de objetos con métodos automáticos

Kotlin es un lenguaje JVM que pretende ser una alternativa más concisa y práctica a Java. Tiene muchas características que los desarrolladores de Java encontrarán familiares, así como algunas nuevas que pueden hacer que el desarrollo sea más rápido y fácil.

Una de estas características son las clases de datos. En Kotlin, una clase de datos es una clase diseñada para contener datos. Las clases de datos tienen algunas características específicas que las diferencian de las clases regulares:

- No pueden ser abstractos, abiertos, sellados o interiores.
- No pueden tener más propiedades que las declaradas en el constructor primario.
- Pueden tener un constructor primario con hasta veintiséis parámetros.
- Todos los parámetros del constructor primario deben estar marcados como val o var.
- Las clases de datos no pueden ser genéricas.

Las clases de datos son útiles porque generan automáticamente una serie de métodos para usted. Estos métodos incluyen:

- ```toString()```: Devuelve una representación de cadena del objeto.
- ```equals()```: Compara este objeto con el objeto especificado para la igualdad.
- ```hashCode()```: Devuelve un valor de código hash para el objeto.
- ```copy()```: Crea una copia del objeto.

Además, las clases de datos también pueden generar una función ```componentN()``` para cada propiedad de la clase. Esta función se puede utilizar para acceder a las propiedades de la clase de datos de una manera más concisa.

Para crear una clase de datos, utiliza la palabra clave ```data```:

```kotlin
data class User(val id: Long, val name: String, val email: String)
```

Esto crea una clase de datos con tres propiedades: ```id```, ```name``` y ```email```. Tenga en cuenta que todas las propiedades están marcadas como ```val```, lo que significa que son inmutables. También puede marcar propiedades como ```var```, lo que significa que son mutables.

Una vez que haya creado una clase de datos, puede crear objetos de esa clase utilizando la sintaxis habitual:

```kotlin
val user = User(1, "John", "john@example.com")
```

Luego puede acceder a las propiedades del objeto utilizando las funciones ```componentN()``` generadas:

```kotlin
println(user.id) // 1
println(user.name) // John
println(user.email) // john@example.com
```

También puede utilizar las funciones generadas ```toString()```, ```equals()``` y ```hashCode()```:

```kotlin
println(user.toString()) // User(id=1, name=John, email=john@example.com)

val anotherUser = User(1, "John", "john@example.com")
println(user == anotherUser) // true

val yetAnotherUser = User(2, "John", "john@example.com")
println(user == yetAnotherUser) // false

println(user.hashCode()) // 367910362
println(anotherUser.hashCode()) // 367910362
println(yetAnotherUser.hashCode()) // 367586981
```

Finalmente, puede usar la función ```copy()``` para crear una copia de un objeto con algunas o todas las propiedades cambiadas:

```kotlin
val user2 = user.copy(id = 2)
println(user2.id) // 2
println(user2.name) // John
println(user2.email) // john@example.com

val user3 = user.copy(name = "Jane")
println(user3.id) // 1
println(user3.name) // Jane
println(user3.email) // john@example.com

val user4 = user.copy(id = 2, name = "Jane", email = "jane@example.com")
println(user4.id) // 2
println(user4.name) // Jane
println(user4.email) // jane@example.com
```

Como puede ver, las clases de datos pueden ser una forma muy conveniente de crear y trabajar con objetos en Kotlin. No solo le evitan escribir una gran cantidad de código repetitivo, sino que también proporcionan una serie de métodos útiles de forma gratuita.