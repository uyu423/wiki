---
title: 052: Nullability y Null Safety en Kotlin: Gestión de valores nulos en su código
description: 
published: true
date: 2023-02-14T03:17:31.249Z
tags: 
editor: markdown
dateCreated: 2023-02-14T03:17:29.684Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [052: Nullability and Null Safety in Kotlin: Managing Null Values in Your Code***English** document is available*](/en/Knowledge-base/Kotlin/Learning/052-nullability-and-null-safety-in-kotlin-managing-null-values-in-your-code)
{.links-list}


## Introducción

Kotlin es un lenguaje de programación de tipo estático que se ejecuta en la máquina virtual de Java. Es un lenguaje JVM que es interoperable con Java y se puede usar para desarrollar aplicaciones de Android.

Una de las características clave de Kotlin es la seguridad nula. La seguridad nula es la capacidad de evitar NullPointerException. Kotlin logra la seguridad nula mediante el uso de tipos anulables y no nulos.

Los tipos anulables pueden contener un valor nulo, mientras que los tipos no nulos no pueden. Esto significa que si intenta asignar un valor nulo a un tipo no nulo, obtendrá un error de tiempo de compilación.

## Tipos anulables y no nulos

Kotlin tiene dos tipos de tipos anulables y no nulos:

* **Tipo anulable**: un tipo que puede contener un valor nulo. Kotlin usa el ? (signo de interrogación) para indicar un tipo anulable.

* **Tipo no nulo**: un tipo que no puede contener un valor nulo. Kotlin usa el !! (doble signo de exclamación) para indicar un tipo no nulo.

Este es un ejemplo de cómo declarar un tipo anulable y no nulo:

```kotlin
// Nullable type
var name: String? = "John"

// Non-null type
var age: Int = 20
```

Como puede ver, el tipo anulable se declara con un ? después del nombre del tipo, mientras que el tipo no nulo se declara sin ?.

## Asignación de valores nulos

Puede asignar un valor nulo a un tipo anulable, pero no puede asignar un valor nulo a un tipo no nulo.

Si intenta asignar un valor nulo a un tipo no nulo, obtendrá un error de tiempo de compilación.

Este es un ejemplo de cómo asignar un valor nulo a un tipo que acepta valores NULL:

```kotlin
var name: String? = "John"

name = null
```

Como puede ver, hemos declarado un tipo anulable y le hemos asignado un valor nulo. Esto está permitido porque el tipo es anulable.

Sin embargo, si intentamos hacer lo mismo con un tipo no nulo, obtendremos un error en tiempo de compilación:

```kotlin
var age: Int = 20

age = null // This will give a compile-time error
```

## Comprobación de valores nulos

Siempre debe verificar los valores nulos antes de usarlos. Kotlin proporciona el ?. (operador de llamada segura) y el !! (operador de aserción no nulo) para ayudarlo a verificar valores nulos.

El ?. El operador comprueba si el valor es nulo antes de acceder a él. Si el valor es nulo, devolverá nulo. De lo contrario, devolverá el valor.

Aquí hay un ejemplo de cómo usar el ?. operador:

```kotlin
var name: String? = "John"

// This will print "John"
println(name?.length)

name = null

// This will print "null"
println(name?.length)
```

Como puede ver, hemos verificado si la variable de nombre es nula antes de acceder a su propiedad de longitud. Si la variable de nombre es nula, el ?. el operador devolverá nulo. De lo contrario, devolverá el valor.

El !! El operador se utiliza para forzar el desenvolvimiento de un valor. Esto significa que devolverá el valor incluso si es nulo.

Esto puede ser peligroso porque puede generar una NullPointerException si el valor es realmente nulo.

Aquí hay un ejemplo de cómo usar el !! operador:

```kotlin
var name: String? = "John"

// This will print "John"
println(name!!.length)

name = null

// This will give a NullPointerException
println(name!!.length)
```

Como puede ver, hemos utilizado el !! operador para forzar el desenvolvimiento de la variable de nombre. Aunque la variable de nombre es nula, el !! el operador seguirá devolviendo el valor.

Sin embargo, si intentamos acceder a la propiedad de longitud de la variable de nombre, obtendremos una NullPointerException porque la variable de nombre es en realidad nula.

## Conclusión

En esta publicación, hemos aprendido sobre la seguridad nula en Kotlin. Hemos aprendido acerca de los tipos anulables y no nulos y cómo asignarles valores nulos. También hemos aprendido sobre el ?. y !! operadores y cómo usarlos para verificar valores nulos.