---
title: 084: Depuración en Kotlin: Depuración de su código Kotlin con puntos de interrupción, relojes y registros
description: 
published: true
date: 2023-02-14T22:17:16.451Z
tags: 
editor: markdown
dateCreated: 2023-02-14T22:17:14.490Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [084: Debugging in Kotlin: Debugging Your Kotlin Code with Breakpoints, Watches, and Logs***English** document is available*](/en/Knowledge-base/Kotlin/Learning/084-debugging-in-kotlin-debugging-your-kotlin-code-with-breakpoints-watches-and-logs)
{.links-list}


# Depuración en Kotlin: depuración de su código Kotlin con puntos de interrupción, relojes y registros

La depuración es una habilidad esencial para cualquier desarrollador. Le permite encontrar y corregir errores en su código para que su programa se ejecute correctamente.

Kotlin es un lenguaje de programación que se ejecuta en Java Virtual Machine (JVM). Es un lenguaje de tipo estático que está diseñado para ser interoperable con Java. Kotlin es un lenguaje conciso, seguro y poderoso que está ganando popularidad.

En esta publicación, aprenderemos cómo depurar el código de Kotlin usando puntos de interrupción, relojes y registros. También aprenderemos sobre algunas de las mejores prácticas para depurar el código de Kotlin.

## ¿Qué es un punto de interrupción?

Un punto de interrupción es un punto en su código donde se detendrá la ejecución de su programa. Esto le permite examinar el estado de su programa y ver qué está pasando. Los puntos de interrupción son muy útiles para la depuración porque le permiten delimitar dónde está el problema en su código.

Hay dos tipos de puntos de interrupción: puntos de interrupción de línea y puntos de interrupción de método. Los puntos de interrupción de línea se establecen en una línea específica de código y pausarán la ejecución de su programa cuando se alcance esa línea. Los puntos de interrupción del método se establecen en un método específico y pausarán la ejecución de su programa cuando se llame a ese método.

Puede establecer puntos de interrupción en Kotlin usando la siguiente sintaxis:

```kotlin
val x = 5

x.setBreakpoint() // line breakpoint

fun foo() {
    // ...
}

foo.setBreakpoint() // method breakpoint
```

## ¿Qué es un reloj?

Un reloj es una variable que está monitoreando mientras su programa se está ejecutando. Puede configurar relojes en Kotlin usando la siguiente sintaxis:

```kotlin
val x = 5

x.watch() // watch x

fun foo() {
    // ...
}

foo.watch() // watch foo
```

## ¿Qué es un registro?

Un registro es un mensaje que puede imprimir mientras se ejecuta su programa. Esto puede ser útil para la depuración porque puede ver lo que sucede en su código en un momento específico. Puede establecer registros en Kotlin usando la siguiente sintaxis:

```kotlin
val x = 5

x.log() // print x

fun foo() {
    // ...
}

foo.log() // print foo
```

## Prácticas recomendadas para depurar código Kotlin

Estas son algunas de las mejores prácticas para depurar el código de Kotlin:

- Use puntos de interrupción para delimitar dónde está el problema en su código.
- Use relojes para monitorear variables mientras su programa se está ejecutando.
- Use registros para imprimir mensajes mientras su programa se está ejecutando.
- Sea paciente y metódico al depurar. Puede ser frustrante, pero tómese su tiempo y eventualmente encontrará el problema.

## Información adicional

- [Documentación de depuración de Kotlin](https://kotlinlang.org/docs/reference/debugging.html)
- [Documentación de depuración de IntelliJ IDEA] (https://www.jetbrains.com/help/idea/debugging.html)
- [Documentación de depuración de Eclipse](https://help.eclipse.org/2018-09/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Fconcepts%2Fconcepts-debug.htm)