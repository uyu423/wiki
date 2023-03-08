---
title: 029: Funciones de biblioteca estándar en Kotlin: uso de funciones de uso común
description: 
published: true
date: 2023-02-06T17:55:48.649Z
tags: 
editor: markdown
dateCreated: 2023-02-06T17:55:47.015Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [029: Standard Library Functions in Kotlin: Utilizing Commonly Used Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/029-standard-library-functions-in-kotlin-utilizing-commonly-used-functions)
{.links-list}


# 029: Funciones de biblioteca estándar en Kotlin: uso de funciones de uso común

Kotlin es un lenguaje de programación de tipo estático que se ejecuta en la máquina virtual de Java y también se puede compilar en el código fuente de JavaScript. La biblioteca estándar de Kotlin proporciona un conjunto de funciones de uso común, que están disponibles sin dependencias adicionales.

En esta publicación, veremos algunas de las funciones más utilizadas en la biblioteca estándar de Kotlin y cómo utilizarlas en su código.

## Colecciones

Kotlin proporciona un conjunto de funciones para trabajar con colecciones de datos. Estas funciones están disponibles en el paquete ```kotlin.collections```.

### Creación de colecciones

Puede crear una nueva colección utilizando las funciones ```arrayOf()```, ```listOf()``` o ```mutableListOf()```. La función ```arrayOf()``` crea una matriz de los elementos dados, la función ```listOf()``` crea una lista de solo lectura y la función ```mutableListOf()``` crea una lista mutable.

Por ejemplo, puede crear una nueva matriz de cadenas como esta:

```kotlin
val array = arrayOf("a", "b", "c")
```

Puede crear una nueva lista de enteros como esta:

```kotlin
val list = listOf(1, 2, 3)
```

Y puedes crear una nueva lista mutable de flotantes como esta:

```kotlin
val mutableList = mutableListOf(1.0f, 2.0f, 3.0f)
```

### Acceso a elementos de una colección

Puede acceder a los elementos de una colección utilizando la función ```get()```. Esta función toma un índice ```Int``` y devuelve el elemento en ese índice.

Por ejemplo, puede acceder al primer elemento de una matriz como esta:

```kotlin
val firstElement = array[0]
```

Puede acceder al último elemento en una lista como esta:

```kotlin
val lastElement = list[list.size - 1]
```

Y puede acceder al elemento central en una lista mutable como esta:

```kotlin
val middleElement = mutableList[mutableList.size / 2]
```

### Adición y eliminación de elementos de una colección

Puede agregar y eliminar elementos de una colección mutable usando las funciones ```add()``` y ```remove()```. La función ```add()``` agrega un elemento al final de la colección, y la función ```remove()``` elimina un elemento de la colección.

Por ejemplo, puede agregar un elemento a una lista mutable como esta:

```kotlin
mutableList.add("d")
```

Puede eliminar el primer elemento de una lista mutable como esta:

```kotlin
mutableList.removeAt(0)
```

Y puede eliminar el último elemento de una lista mutable como esta:

```kotlin
mutableList.removeAt(mutableList.size - 1)
```

## Cuerdas

Kotlin proporciona un conjunto de funciones para trabajar con cadenas. Estas funciones están disponibles en el paquete ```kotlin.text```.

### Creación de cadenas

Puede crear una nueva cadena usando la función ```String()```. Esta función toma un valor ```Any``` y lo convierte en una cadena.

Por ejemplo, puede crear una nueva cadena a partir de un número entero como este:

```kotlin
val string = String(42)
```

También puede crear una nueva cadena concatenando dos cadenas juntas. Por ejemplo, puede concatenar la cadena "Hola" con la cadena "Mundo" de esta manera:

```kotlin
val string = "Hello" + "World"
```

### Acceso a caracteres en una cadena

Puede acceder a los caracteres de una cadena utilizando la función ```get()```. Esta función toma un índice ```Int``` y devuelve el carácter en ese índice.

Por ejemplo, puede acceder al primer carácter de una cadena como esta:

```kotlin
val firstCharacter = string[0]
```

Puede acceder al último carácter de una cadena como esta:

```kotlin
val lastCharacter = string[string.length - 1]
```

Y puede acceder al carácter del medio en una cadena como esta:

```kotlin
val middleCharacter = string[string.length / 2]
```

### Adición y eliminación de caracteres de una cadena

Puede agregar y eliminar caracteres de una cadena usando las funciones ```plus()``` y ```minus()```. La función ```plus()``` agrega un carácter al final de la cadena, y la función ```minus()``` elimina un carácter de la cadena.

Por ejemplo, puede agregar el carácter "!" al final de una cadena como esta:

```kotlin
val exclamationString = string + "!"
```

Puede eliminar el primer carácter de una cadena como esta:

```kotlin
val noFirstCharacterString = string.drop(1)
```

Y puede eliminar el último carácter de una cadena como esta:

```kotlin
val noLastCharacterString = string.dropLast(1)
```

## Conclusión

En esta publicación, echamos un vistazo a algunas de las funciones más utilizadas en la biblioteca estándar de Kotlin. Hemos visto cómo crear y manipular colecciones, cómo trabajar con cadenas y cómo usar algunas de las otras funciones de uso común en Kotlin.