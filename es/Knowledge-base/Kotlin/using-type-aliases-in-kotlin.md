---
title: Uso de alias de tipo en Kotlin
description: 
published: true
date: 2023-02-08T12:17:17.403Z
tags: 
editor: markdown
dateCreated: 2023-02-08T12:17:15.703Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Using Type Aliases in Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/using-type-aliases-in-kotlin)
{.links-list}


# Uso de alias de tipo en Kotlin

Los alias de tipo son una excelente manera de mejorar la legibilidad de su código, especialmente cuando se trabaja con tipos genéricos largos. En Kotlin, puede usar alias de tipo para crear un alias para un tipo, que luego se puede usar en lugar del tipo original. Esto puede ser especialmente útil cuando se trabaja con tipos genéricos, ya que puede hacer que su código sea mucho más fácil de leer y comprender.

Para crear un alias de tipo, utilice la palabra clave `typealias`, seguida del nombre del alias y el tipo del que desea crear un alias. Por ejemplo, digamos que tenemos un tipo genérico `Person<T>`, donde `T` es el tipo del nombre de la persona. Podríamos crear un alias de tipo para este tipo de la siguiente manera:

```kotlin
typealias PersonName = Person<String>
```

Ahora, en lugar de usar `Person<String>` en todas partes de nuestro código, podemos usar `PersonName`. Esto puede hacer que nuestro código sea mucho más fácil de leer, ya que queda claro a qué se refiere `PersonName`.

También vale la pena señalar que los alias de tipo no se limitan solo a tipos genéricos. Puede usarlos para cualquier tipo, incluidas clases regulares, interfaces e incluso otros tipos de alias.

Una nota final sobre los alias de tipo es que no son intercambiables con los tipos originales. Esto significa que no puede usar un alias de tipo donde se espera el tipo original. Por ejemplo, el siguiente código no se compilará:

```kotlin
fun main() {
    val list: List<String> = listOf("a", "b", "c")
    val personNameList: PersonNameList = list // Error: Type mismatch
}
```

Esto se debe a que `List<String>` no es del mismo tipo que `PersonNameList`. Si desea poder usar un alias de tipo donde se espera el tipo original, puede usar la palabra clave `en línea`. Esto está fuera del alcance de este artículo, pero puede leer más al respecto [aquí] (https://kotlinlang.org/docs/reference/inline-classes.html).

## Referencias

- [Alias de tipo Kotlin](https://kotlinlang.org/docs/reference/type-aliases.html)
- [Clases en línea de Kotlin] (https://kotlinlang.org/docs/reference/inline-classes.html)