---
title: 038: Tipos cosificados en Kotlin: Acceso a tipos en tiempo de ejecución
description: 
published: true
date: 2023-02-02T01:57:39.033Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:57:37.405Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [038: Reified Types in Kotlin: Accessing Types at Runtime***English** document is available*](/en/Knowledge-base/Kotlin/Learning/038-reified-types-in-kotlin-accessing-types-at-runtime)
{.links-list}


# Introducción

Kotlin es un lenguaje de tipo estático que se ejecuta en la JVM. Tiene una excelente interoperabilidad con Java y es una excelente opción para desarrollar aplicaciones de Android.

Una de las características más poderosas de Kotlin es su compatibilidad con tipos cosificados. Esto le permite acceder a los tipos en tiempo de ejecución, lo que no es posible en Java.

En esta publicación, veremos qué son los tipos cosificados y cómo se pueden usar en Kotlin. También veremos algunos ejemplos de cómo se pueden usar los tipos cosificados para facilitar el desarrollo.

# ¿Qué son los tipos cosificados?

Los tipos reificados son tipos a los que se puede acceder en tiempo de ejecución. Esto no es posible en Java, donde los tipos solo están disponibles en tiempo de compilación.

Los tipos cosificados son muy útiles para trabajar con la reflexión. La reflexión es una forma de acceder dinámicamente a las clases y sus miembros en tiempo de ejecución. A menudo se usa en marcos y bibliotecas.

En Kotlin, los tipos cosificados se declaran con la palabra clave "reificado". Por ejemplo, podemos declarar un tipo cosificado como este:

```kotlin
reified val myType: String = "Hello, world!"
```

Ahora podemos acceder al tipo de `myType` en tiempo de ejecución:

```kotlin
val type = myType::class
```

La variable `tipo` contendrá la clase `String`.

También podemos acceder al tipo de un tipo genérico:

```kotlin
reified val myList: List<String> = listOf("Hello", "world!")

val type = myList::class
```

La variable `tipo` contendrá la clase `Lista`.

# ¿Cómo se pueden usar los tipos cosificados?

Los tipos cosificados se pueden usar de varias maneras. Veremos algunos de los casos de uso más comunes.

## Trabajando con la reflexión

Como hemos visto, los tipos cosificados son muy útiles para trabajar con la reflexión. La reflexión es una forma de acceder dinámicamente a las clases y sus miembros en tiempo de ejecución.

En Java, la reflexión se usa a menudo en marcos y bibliotecas. Por ejemplo, el marco Spring utiliza la reflexión para crear objetos dinámicamente.

En Kotlin, podemos usar la reflexión para acceder a los miembros de una clase:

```kotlin
reified val myClass: MyClass = MyClass()

val members = myClass::class.members
```

La variable `members` contendrá una lista de todos los miembros de la clase `MyClass`.

También podemos usar la reflexión para acceder a las anotaciones de una clase:

```kotlin
reified val myClass: MyClass = MyClass()

val annotations = myClass::class.annotations
```

La variable `anotaciones` contendrá una lista de todas las anotaciones de la clase `MiClase`.

## Trabajar con tipos genéricos

Los tipos cosificados también son muy útiles para trabajar con tipos genéricos. En Java, no es posible acceder al tipo de un tipo genérico en tiempo de ejecución. Esto puede dificultar el trabajo con tipos genéricos.

En Kotlin, podemos usar tipos cosificados para acceder al tipo de un tipo genérico:

```kotlin
reified val myList: List<String> = listOf("Hello", "world!")

val type = myList::class
```

La variable `tipo` contendrá la clase `Lista`.

También podemos usar tipos cosificados para crear tipos genéricos:

```kotlin
inline fun <reified T> createList(): List<T> {
    return listOf()
}

val myList = createList<String>()
```

La variable `myList` contendrá una `List<String>` vacía.

## Trabajando con la reflexión de Kotlin

La reflexión de Kotlin es una forma de acceder dinámicamente a las clases de Kotlin y sus miembros en tiempo de ejecución. Es muy similar a la reflexión de Java, pero es mucho más fácil de usar.

En Kotlin, podemos usar tipos cosificados para acceder a los miembros de una clase:

```kotlin
reified val myClass: MyClass = MyClass()

val members = myClass::class.members
```

La variable `members` contendrá una lista de todos los miembros de la clase `MyClass`.

También podemos usar tipos cosificados para acceder a las anotaciones de una clase:

```kotlin
reified val myClass: MyClass = MyClass()

val annotations = myClass::class.annotations
```

La variable `anotaciones` contendrá una lista de todas las anotaciones de la clase `MiClase`.

# Conclusión

En esta publicación, hemos visto qué son los tipos cosificados y cómo se pueden usar en Kotlin. También hemos visto algunos ejemplos de cómo se pueden usar tipos reificados para facilitar el desarrollo.

Los tipos cosificados son una característica poderosa de Kotlin que se puede usar de varias maneras. Si está trabajando con tipos genéricos o de reflexión, los tipos cosificados pueden ser de gran ayuda.