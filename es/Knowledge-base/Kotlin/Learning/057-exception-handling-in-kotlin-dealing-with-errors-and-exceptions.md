---
title: 057: Manejo de excepciones en Kotlin: manejo de errores y excepciones
description: 
published: true
date: 2023-02-01T16:23:24.676Z
tags: 
editor: markdown
dateCreated: 2023-02-01T16:23:22.987Z
---

> Este artículo se tradujo automáticamente con la **API de Google Cloud Translation**.
Algunas páginas pueden leerse mejor que el original.{.is-info}

- [057: Exception Handling in Kotlin: Dealing with Errors and Exceptions***Spanish** version of this document is available*](/es/Knowledge-base/Kotlin/Learning/057-exception-handling-in-kotlin-dealing-with-errors-and-exceptions)
{.links-list}


# Manejo de excepciones de Kotlin

Las excepciones son eventos que ocurren durante la ejecución de un programa que interrumpen el flujo normal de instrucciones. Kotlin proporciona un mecanismo poderoso para manejar las excepciones. En este artículo, veremos cómo manejar las excepciones en Kotlin.

## ¿Qué son las excepciones?

Una excepción es un evento que ocurre durante la ejecución de un programa que interrumpe el flujo normal de instrucciones. Cuando ocurre una excepción, el programa termina abruptamente.

Hay dos tipos de excepciones: marcadas y no marcadas. Las excepciones marcadas son aquellas que ocurren en tiempo de compilación, como cuando no se encuentra un archivo. Las excepciones no verificadas son aquellas que ocurren en tiempo de ejecución, como cuando ocurre un error de división por cero.

## Manejo de excepciones

Kotlin proporciona un mecanismo poderoso para manejar las excepciones. El bloque try/catch se usa para manejar excepciones. El bloque try contiene el código que puede generar una excepción. El bloque catch contiene el código que maneja la excepción.

```kotlin
try {
   // code that may throw an exception
} catch (e: Exception) {
   // code that handles the exception
}
```

Si ocurre una excepción en el bloque try, se ejecuta el bloque catch. Si no se produce ninguna excepción, se omite el bloque catch.

También es posible tener múltiples bloques catch para manejar diferentes tipos de excepciones.

```kotlin
try {
   // code that may throw an exception
} catch (e: FileNotFoundException) {
   // code that handles the FileNotFoundException
} catch (e: IOException) {
   // code that handles the IOException
}
```

## Finalmente bloque

El bloque finalmente es opcional. Se ejecuta tanto si se produce una excepción como si no.

```kotlin
try {
   // code that may throw an exception
} catch (e: Exception) {
   // code that handles the exception
} finally {
   // code that is always executed
}
```

## Lanzamiento de excepciones

Las excepciones se pueden lanzar explícitamente usando la palabra clave throw.

```kotlin
throw FileNotFoundException()
```

## Creación de excepciones personalizadas

Es posible crear excepciones personalizadas extendiendo la clase Exception.

```kotlin
class MyException: Exception() {
}
```

## Recursos

- [Documentos de Kotlin - Manejo de excepciones](https://kotlinlang.org/docs/reference/exceptions.html)
- [JavaWorld - Manejo de excepciones en Kotlin](https://www.javaworld.com/article/3240006/learn-java/exception-handling-in-kotlin.html)
- [Desbordamiento de pila - ¿Cómo creo una excepción personalizada en Kotlin?](https://stackoverflow.com/questions/44487193/how-do-i-create-a-custom-exception-in-kotlin)