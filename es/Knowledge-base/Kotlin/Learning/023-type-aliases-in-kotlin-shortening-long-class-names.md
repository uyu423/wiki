---
title: 023: Tipo de alias en Kotlin: acortamiento de nombres de clase largos
description: 
published: true
date: 2023-02-01T20:17:28.187Z
tags: 
editor: markdown
dateCreated: 2023-02-01T20:17:24.107Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [023: Type Aliases in Kotlin: Shortening Long Class Names***English** document is available*](/en/Knowledge-base/Kotlin/Learning/023-type-aliases-in-kotlin-shortening-long-class-names)
{.links-list}


# 023: Tipo de alias en Kotlin: Acortar nombres de clase largos

Kotlin tiene una gran característica llamada alias de tipo que se puede usar para acortar los nombres de clase largos. Por ejemplo, considere el siguiente nombre de clase:

```kotlin
class MyVeryLongClassName {
    // ...
}
```

Este nombre de clase es bastante largo y sería bueno si pudiéramos acortarlo. Podemos hacer esto usando un alias de tipo:

```kotlin
typealias MyClass = MyVeryLongClassName

class MyClass {
    // ...
}
```

Ahora, el alias `MyClass` se puede usar en cualquier parte de nuestro código en lugar del nombre largo de la clase. Esto es especialmente útil cuando se trabaja con tipos genéricos:

```kotlin
typealias MyClass = MyVeryLongClassName

class MyClass<T> {
    // ...
}

fun main() {
    val myClass: MyClass<String> = MyClass()
}
```

En el ejemplo anterior, hemos definido un alias de tipo para la clase `MyVeryLongClassName`. Entonces podemos usar este alias al declarar variables del tipo genérico. Esto puede hacer que nuestro código sea mucho más fácil de leer y comprender.

Hay algunas cosas a tener en cuenta al usar alias de tipo:

- Los alias de tipo no son lo mismo que las clases. Son simplemente una forma de dar un nombre diferente a un tipo.
- Los alias de tipo no se pueden utilizar para crear nuevos tipos. Solo se pueden usar para dar un nuevo nombre a un tipo existente.
- Los alias de tipo no se pueden utilizar para cambiar el tipo de una variable. Solo se pueden usar cuando se declara una nueva variable.

En general, los alias de tipo son una excelente manera de acortar los nombres de clase largos y hacer que nuestro código sea más legible. Son especialmente útiles cuando se trabaja con tipos genéricos.