---
title: 048: El operador de Elvis en Kotlin: tratar con valores nulos de forma compacta
description: 
published: true
date: 2023-02-02T09:57:28.073Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:57:26.490Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [048: The Elvis Operator in Kotlin: Dealing with Null Values in a Compact Way***English** document is available*](/en/Knowledge-base/Kotlin/Learning/048-the-elvis-operator-in-kotlin-dealing-with-null-values-in-a-compact-way)
{.links-list}


# El operador de Elvis en Kotlin: manejo de valores nulos de manera compacta

Los valores nulos pueden ser un dolor de cabeza en cualquier lenguaje de programación. En Kotlin, el operador Elvis proporciona una forma concisa y segura de manejar valores nulos.

## ¿Qué es el Operador Elvis?

El operador Elvis es un operador de seguridad nula que devuelve el valor no nulo de su operando o un valor predeterminado si el operando es nulo. El operador de Elvis se escribe de la siguiente manera:

```kotlin
val result = operand ?: defaultValue
```

Si el operando no es nulo, el operador de Elvis lo devuelve. Si el operando es nulo, el operador de Elvis devuelve el valor predeterminado.

## ¿Cómo funciona el Operador Elvis?

El operador de Elvis se compone de dos partes: el operador de seguridad nula (`?.`) y el operador de Elvis (`?:`).

El operador de seguridad nula (`?.`) se utiliza para acceder de forma segura a un miembro de un objeto anulable. Si el objeto es nulo, el operador de seguridad nula devuelve nulo en lugar de lanzar una NullPointerException.

El operador Elvis (`?:`) se utiliza para proporcionar un valor predeterminado si el operando es nulo.

## Cuándo usar el Operador Elvis

El operador Elvis se usa más comúnmente para manejar valores nulos de una manera concisa y segura.

Por ejemplo, considere el siguiente código:

```kotlin
val list: List<String>? = null

val firstItem = list?.get(0) ?: "Default Value"
```

En este código, la variable `list` es anulable. Si `list` es nulo, la variable `firstItem` se establecerá en el valor predeterminado ("Valor predeterminado"). Si `list` no es nulo, la variable `firstItem` se establecerá en el primer elemento de la lista.

## Información Adicional

Aquí hay algunos recursos adicionales para aprender más sobre el operador de Elvis:

- [Documentos de Kotlin - El operador de Elvis](https://kotlinlang.org/docs/reference/null-safety.html# the-elvis-operator)
- [Academia Kotlin - Seguridad nula y el operador de Elvis](https://kotlinacademy.com/kotlin-null-safety-elvis-operator/)
- [Desarrolladores de Android - Manejo de nulos en Kotlin](https://developer.android.com/kotlin/null-safety)