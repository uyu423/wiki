---
title: 037: Funciones en línea en Kotlin: Mejora del rendimiento con funciones en línea
description: 
published: true
date: 2023-02-16T10:32:23.722Z
tags: 
editor: markdown
dateCreated: 2023-02-16T10:32:21.639Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [037: Inline Functions in Kotlin: Improving Performance with Inlined Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/037-inline-functions-in-kotlin-improving-performance-with-inlined-functions)
{.links-list}


## Introducción

Kotlin es un lenguaje de programación de tipo estático que se ejecuta en la máquina virtual de Java y también se puede compilar en el código fuente de JavaScript.

En esta publicación, veremos cómo mejorar el rendimiento con funciones en línea en Kotlin.

## ¿Qué son las funciones en línea?

En Kotlin, las funciones en línea son funciones que se expanden en el cuerpo de la persona que llama. Esto es diferente de las funciones no en línea, donde la función se llama como de costumbre.

Las funciones en línea se pueden usar para mejorar el rendimiento al reducir la sobrecarga de las llamadas a funciones. Además, las funciones en línea pueden acceder a las variables de la persona que llama, lo que también puede mejorar el rendimiento.

## Cómo usar las funciones en línea

Para usar funciones en línea, debe anotar la función con la palabra clave `en línea`.

Por ejemplo, digamos que tenemos una función `foo()` que queremos en línea:

```kotlin
inline fun foo() {
    // do something
}
```

Ahora, siempre que llamemos a `foo()`, el cuerpo de la función se expandirá en la persona que llama.

## Cuándo usar funciones en línea

En general, solo debe usar funciones en línea cuando esté seguro de que la función en línea mejorará el rendimiento.

Además, solo debe usar funciones en línea si la función es pequeña y simple. Esto se debe a que la integración de una función compleja puede generar una sobrecarga de código y, de hecho, disminuir el rendimiento.

Finalmente, solo debe usar funciones en línea si está seguro de que la función no se llamará desde varios lugares. Esto se debe a que insertar una función puede dar lugar a un código duplicado si se llama a la función desde varios lugares.

## Conclusión

En esta publicación, hemos aprendido sobre las funciones en línea en Kotlin y cómo usarlas para mejorar el rendimiento. En general, solo debe usar funciones en línea cuando esté seguro de que la función en línea mejorará el rendimiento. Además, solo debe usar funciones en línea si la función es pequeña y simple.