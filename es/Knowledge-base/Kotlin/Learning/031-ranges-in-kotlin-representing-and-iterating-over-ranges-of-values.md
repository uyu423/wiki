---
title: 031: Rangos en Kotlin: representación e iteración sobre rangos de valores
description: 
published: true
date: 2023-02-10T17:55:15.924Z
tags: 
editor: markdown
dateCreated: 2023-02-10T17:55:14.343Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [031: Ranges in Kotlin: Representing and Iterating Over Ranges of Values***English** document is available*](/en/Knowledge-base/Kotlin/Learning/031-ranges-in-kotlin-representing-and-iterating-over-ranges-of-values)
{.links-list}


# Rangos en Kotlin: representación e iteración sobre rangos de valores

Los rangos son un concepto fundamental en Kotlin que te permite representar una secuencia de valores. En esta publicación, veremos cómo crear e iterar rangos en Kotlin.

## Creando rangos

Hay dos formas de crear rangos en Kotlin: usando el operador `..` o usando la función `rangeTo()`.

El operador `..` se usa para crear rangos que incluyen sus valores inicial y final. Por ejemplo, el siguiente código crea un rango de 1 a 5:

```kotlin
val range1 = 1..5
```

La función `rangeTo()`, por otro lado, se usa para crear rangos que excluyen sus valores finales. Por ejemplo, el siguiente código crea un rango de 1 a 5:

```kotlin
val range2 = 1.rangeTo(5)
```

Ambos rangos son *inclusivos*, lo que significa que incluyen sus valores inicial y final. También puede crear rangos *exclusivos* usando la palabra clave `hasta` en lugar de `..` o `.rangeTo()`. Por ejemplo, el siguiente código crea un rango de 1 a 5:

```kotlin
val range3 = 1 until 5
```

## Iterando sobre rangos

Ahora que sabemos cómo crear rangos, echemos un vistazo a cómo iterar sobre ellos. Podemos hacer esto usando un bucle for:

```kotlin
for (i in 1..5) {
    println(i)
}
```

Este código imprimirá los números del 1 al 5 en la consola. También podemos iterar rangos a la inversa usando la palabra clave `downTo`:

```kotlin
for (i in 5 downTo 1) {
    println(i)
}
```

Este código imprimirá los números del 5 al 1 en la consola.

## Conclusión

En esta publicación, echamos un vistazo a cómo crear e iterar rangos en Kotlin. Los rangos son una herramienta poderosa que se puede utilizar en una variedad de situaciones. ¡Espero que los encuentres tan útiles como yo!