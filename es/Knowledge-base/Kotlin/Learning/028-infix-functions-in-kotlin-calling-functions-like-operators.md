---
title: 028: Funciones infijas en Kotlin: funciones de llamada como operadores
description: 
published: true
date: 2023-02-01T17:23:30.520Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:23:28.881Z
---

> Este artículo se tradujo automáticamente con la **API de Google Cloud Translation**.
Algunas páginas pueden leerse mejor que el original.{.is-info}

- [028: Infix Functions in Kotlin: Calling Functions Like Operators***Spanish** version of this document is available*](/es/Knowledge-base/Kotlin/Learning/028-infix-functions-in-kotlin-calling-functions-like-operators)
{.links-list}



#028: Funciones infijas en Kotlin: funciones de llamada como operadores
Kotlin es un lenguaje de programación de tipo estático para JVM, Android y el navegador. Es conocido por su interoperabilidad, seguridad, soporte de herramientas y sintaxis concisa.

Kotlin tiene una serie de características que lo hacen único y atractivo para los desarrolladores, una de las cuales son las funciones infix.

Las funciones infijas son funciones que se pueden llamar sin usar la notación de punto habitual. Esto significa que pueden llamarse como operadores, lo que puede hacer que el código sea más conciso y legible.

Las funciones infix están marcadas con la palabra clave infix. Deben ser funciones miembro o funciones de extensión. Solo pueden tener un parámetro.

Aquí hay un ejemplo simple de una función infija:

```kotlin
infix fun Int.times(str: String) = str.repeat(this)

println(2 times "Bye ") // Prints "Bye Bye "
```

En el ejemplo anterior, la función `times` se llama con los parámetros `2` y `"Bye "`. La función `times` devuelve la cadena `"Bye"` repetida `2` veces.

Las funciones infix pueden ser muy útiles para hacer que el código sea más legible. Por ejemplo, el operador `+` se usa a menudo para concatenar cadenas. Sin embargo, también se puede utilizar para sumar. Esto puede resultar confuso para los desarrolladores que no están familiarizados con Kotlin.

Con funciones infix, podemos definir nuestro propio operador `+` para la concatenación de cadenas, lo que puede hacer que nuestro código sea más legible:

```kotlin
infix fun String.plus(str: String) = this + str

println("Hello" plus " world") // Prints "Hello world"
```

En el ejemplo anterior, hemos definido una función infija para la concatenación de cadenas. Ahora podemos usar el operador `+` para concatenar dos cadenas. Esto puede hacer que nuestro código sea más legible y conciso.

Las funciones infijas también se pueden usar para comparar. Por ejemplo, podemos usar la función `compareTo` para comparar dos cadenas:

```kotlin
infix fun String.compareTo(str: String) = this.compareTo(str)

println("a" compareTo "b") // Prints -1
println("b" compareTo "a") // Prints 1
println("a" compareTo "a") // Prints 0
```

En el ejemplo anterior, hemos definido una función infija para la comparación de cadenas. Ahora podemos usar la función `compareTo` para comparar dos cadenas. Esto puede hacer que nuestro código sea más legible y conciso.

Las funciones Infix son una herramienta poderosa que puede hacer que el código de Kotlin sea más legible y conciso. Sin embargo, deben usarse con precaución, ya que pueden hacer que el código sea menos legible si se usan en exceso.