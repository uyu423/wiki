---
title: 024: Enumeraciones en Kotlin: creación de listas de valores con nombre
description: 
published: true
date: 2023-02-16T07:33:05.551Z
tags: 
editor: markdown
dateCreated: 2023-02-16T07:32:57.681Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [024: Enumerations in Kotlin: Creating Lists of Named Values***English** document is available*](/en/Knowledge-base/Kotlin/Learning/024-enumerations-in-kotlin-creating-lists-of-named-values)
{.links-list}


# Enumeraciones en Kotlin: creación de listas de valores con nombre

Las enumeraciones de Kotlin son una herramienta poderosa para crear listas de valores con nombre. Mediante el uso de enumeraciones, puede crear listas de valores inmutables y con seguridad de tipos que se pueden usar en su código.

Las enumeraciones se declaran usando la palabra clave ```enum```. Cada valor en una enumeración se denomina ```constante de enumeración```. Las constantes de enumeración están separadas por comas.

Aquí hay un ejemplo simple de una enumeración en Kotlin:

```kotlin
enum class Color {
    RED,
    GREEN,
    BLUE
}
```

En este ejemplo, hemos creado una enumeración de colores. La palabra clave ```enum``` se usa para declarar la enumeración, y la palabra clave ```class``` se usa para crear las constantes de enumeración.

Las enumeraciones son inmutables, lo que significa que una vez que se crean, no se pueden cambiar. Esto los hace seguros para usar en su código.

Las enumeraciones se pueden usar de varias maneras en Kotlin. En esta publicación, veremos algunas de las formas en que puede usar enumeraciones en su código.

## Uso de enumeraciones

Las enumeraciones se pueden usar de varias maneras en Kotlin. En esta sección, veremos algunas de las formas en que puede usar enumeraciones en su código.

### Cambiar declaraciones

Las enumeraciones se pueden usar en declaraciones ```when``` en Kotlin. Las sentencias ```When``` son un tipo de sentencia ```switch``` que le permite hacer coincidir un valor con una lista de valores posibles.

Aquí hay un ejemplo de una declaración ```when``` que usa una enumeración:

```kotlin
fun getColor(color: Color): String {
    when (color) {
        Color.RED -> return "Red"
        Color.GREEN -> return "Green"
        Color.BLUE -> return "Blue"
    }
}
```

En este ejemplo, hemos creado una función que toma una enumeración ```Color``` como argumento. Luego usamos una declaración ```when``` para hacer coincidir el ```color``` con la lista de valores posibles.

Si el ```color``` es ```RED```, la función devolverá la cadena ```"Rojo"```. Si el ```color``` es ```VERDE```, la función devolverá la cadena ```"Verde"```. Si el ```color``` es ```AZUL```, la función devolverá la cadena ```"Azul"```.

### Iterando sobre enumeraciones

Las enumeraciones se pueden iterar usando el bucle ```for```. El ciclo ```for``` iterará sobre todas las constantes de enumeración en la enumeración.

Aquí hay un ejemplo de cómo iterar sobre una enumeración:

```kotlin
for (color in Color.values()) {
    println(color)
}
```

En este ejemplo, usamos el ciclo ```for``` para iterar sobre la enumeración ```Color```. Imprimimos cada valor de la enumeración a la consola.

Este código imprimirá lo siguiente en la consola:

```
RED
GREEN
BLUE
```

### Comprobación de valores de enumeración

Puede verificar si un valor particular está contenido dentro de una enumeración usando la palabra clave ```in```.

Aquí hay un ejemplo de cómo verificar si un valor está contenido en una enumeración:

```kotlin
if (Color.RED in Color.values()) {
    println("Color.RED is in the Color enumeration")
}
```

En este ejemplo, usamos la palabra clave ```in``` para verificar si la constante de enumeración ```Color.RED``` está contenida en la enumeración ```Color```.

Si la constante de enumeración ```Color.RED``` está contenida en la enumeración ```Color```, el código imprimirá lo siguiente en la consola:

```
Color.RED is in the Color enumeration
```

### Obtener valores de enumeración por nombre

Puede obtener una constante de enumeración por su nombre usando la función ```valueOf()```.

Aquí hay un ejemplo de cómo obtener una constante de enumeración por su nombre:

```kotlin
val color: Color = Color.valueOf("RED")
```

En este ejemplo, usamos la función ```valueOf()``` para obtener la constante de enumeración ```Color.RED``` de la enumeración ```Color```.

### Creación de sus propias enumeraciones

Además de las enumeraciones estándar de Kotlin, también puede crear sus propias enumeraciones personalizadas.

Aquí hay un ejemplo de cómo crear una enumeración personalizada:

```kotlin
enum class MyEnum {
    FIRST_VALUE,
    SECOND_VALUE
}
```

En este ejemplo, hemos creado una enumeración personalizada llamada ```MyEnum```. Esta enumeración contiene dos valores: ```FIRST_VALUE``` y ```SECOND_VALUE```.

También puede crear enumeraciones con propiedades y métodos personalizados.

Aquí hay un ejemplo de cómo crear una enumeración con una propiedad personalizada:

```kotlin
enum class MyEnum {
    FIRST_VALUE {
        override val property: Int
            get() = 1
    },
    SECOND_VALUE {
        override val property: Int
            get() = 2
    }

    abstract val property: Int
}
```

En este ejemplo, hemos creado una enumeración con una propiedad personalizada llamada ```property```. Esta propiedad es una propiedad ```abstract``` que debe ser anulada por cada constante de enumeración.

En este ejemplo, hemos anulado la propiedad ```property``` para las constantes de enumeración ```FIRST_VALUE``` y ```SECOND_VALUE```.

También puede crear enumeraciones con métodos personalizados.

Aquí hay un ejemplo de cómo crear una enumeración con un método personalizado:

```kotlin
enum class MyEnum {
    FIRST_VALUE {
        override fun method(): String {
            return "First Value"
        }
    },
    SECOND_VALUE {
        override fun method(): String {
            return "Second Value"
        }
    }

    abstract fun method(): String
}
```

En este ejemplo, hemos creado una enumeración con un método personalizado llamado ```method()```. Este método es un método ```abstracto``` que debe ser anulado por cada constante de enumeración.

En este ejemplo, hemos anulado el método ```method()``` para las constantes de enumeración ```FIRST_VALUE``` y ```SECOND_VALUE```.

Las enumeraciones son una herramienta poderosa para crear listas de valores con nombre en Kotlin. Mediante el uso de enumeraciones, puede crear listas de valores inmutables y con seguridad de tipos que se pueden usar en su código.