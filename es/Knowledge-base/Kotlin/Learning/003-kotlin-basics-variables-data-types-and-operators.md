---
title: 003: Conceptos básicos de Kotlin: variables, tipos de datos y operadores
description: 
published: true
date: 2023-02-07T19:56:03.026Z
tags: 
editor: markdown
dateCreated: 2023-02-07T19:55:57.047Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [003: Kotlin Basics: Variables, Data Types, and Operators***English** document is available*](/en/Knowledge-base/Kotlin/Learning/003-kotlin-basics-variables-data-types-and-operators)
{.links-list}


# Conceptos básicos de Kotlin: variables, tipos de datos y operadores

Kotlin es un lenguaje de programación de tipo estático que se ejecuta en la JVM. Es un lenguaje conciso, seguro, interoperable y amigable con las herramientas.

Kotlin es un lenguaje orientado a objetos y, por lo tanto, las variables deben declararse antes de que puedan usarse. En Kotlin, hay dos tipos de variables:

* Variables mutables: estas variables se pueden cambiar después de haber sido inicializadas. Para declarar una variable mutable, utilice la palabra clave ```var```.
```kotlin
var name = "John"
name = "Jane" // Valid
```

* Variables inmutables: estas variables no se pueden cambiar después de haber sido inicializadas. Para declarar una variable inmutable, utilice la palabra clave ```val```.
```kotlin
val name = "John"
name = "Jane" // Invalid
```

Kotlin tiene una función de seguridad nula que elimina el riesgo de excepciones de puntero nulo. Para permitir que una variable contenga un valor nulo, debe declararla como anulable mediante el símbolo ```?```.

```kotlin
var name: String? = null
```

Kotlin también tiene un amplio conjunto de operadores que se pueden usar en variables. Éstas incluyen:

* Operadores aritméticos: ```+```, ```-```, ```*```, ```/```, ```%```
* Operadores de asignación: ```=```, ```+=```, ```-=```, ```*=```, ```/=```, `` `%=```
* Operadores de comparación: ```==```, ```!=```, ```>```, ```<```, ```>=```, ``` <=```
* Operadores lógicos: ```&&```, ```||```, ```!```

Ahora que conoce los conceptos básicos de las variables y los operadores de Kotlin, pasemos a los tipos de datos.

## Tipos de datos de Kotlin

Kotlin tiene los siguientes tipos de datos:

* Números: Kotlin admite números enteros y de coma flotante.
* Caracteres: Los caracteres de Kotlin están representados por el tipo ```Char```.
* Booleanos: Los booleanos de Kotlin están representados por el tipo ```Boolean```.
* Arreglos: los arreglos de Kotlin están representados por el tipo ```Array```.
* Cadenas: las cadenas de Kotlin están representadas por el tipo ```String```.

Además de los tipos de datos anteriores, Kotlin también tiene un tipo especial llamado ```Unit```. Este tipo se utiliza para representar un valor nulo.

Ahora que conoce los conceptos básicos de los tipos de datos de Kotlin, pasemos a los operadores de Kotlin.

## Operadores de Kotlin

Kotlin tiene un amplio conjunto de operadores que se pueden usar en variables. Éstas incluyen:

* Operadores aritméticos: ```+```, ```-```, ```*```, ```/```, ```%```
* Operadores de asignación: ```=```, ```+=```, ```-=```, ```*=```, ```/=```, `` `%=```
* Operadores de comparación: ```==```, ```!=```, ```>```, ```<```, ```>=```, ``` <=```
* Operadores lógicos: ```&&```, ```||```, ```!```

Ahora que conoce los conceptos básicos de los operadores de Kotlin, pasemos al flujo de control de Kotlin.

## Flujo de control de Kotlin

Kotlin tiene las siguientes construcciones de flujo de control:

* Expresión ```if```: Se utiliza para evaluar una expresión booleana y ejecutar un bloque de código si la expresión es ```verdadera```.
* Expresión ```if-else```: Se usa para evaluar una expresión booleana y ejecutar uno de dos bloques de código, dependiendo de si la expresión es ```verdadera``` o ```falsa```.
* ```when``` expresión: Se utiliza para evaluar una expresión y ejecutar uno de varios bloques de código, según el valor de la expresión.
* Bucle ```for```: Usado para ejecutar un bloque de código un número fijo de veces.
* Bucle ```while```: se usa para ejecutar un bloque de código varias veces, hasta que se cumple una condición.
* Bucle ```do-while```: se usa para ejecutar un bloque de código varias veces, hasta que se cumple una condición. La diferencia entre un bucle ```while``` y un bucle ```do-while``` es que un bucle ```do-while``` siempre ejecutará el bloque de código al menos una vez.

Ahora que conoce los conceptos básicos del flujo de control de Kotlin, pasemos a las funciones de Kotlin.

## Funciones de Kotlin

Una función es un bloque de código que toma uno o más parámetros de entrada y produce una salida. En Kotlin, las funciones se declaran usando la palabra clave ```fun```.

Aquí hay una función simple que toma dos parámetros de entrada y devuelve la suma de esos parámetros:

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

Si una función no devuelve un valor, su tipo de retorno debe declararse como ```Unit```.

Aquí hay una función simple que toma dos parámetros de entrada e imprime la suma de esos parámetros:

```kotlin
fun sum(a: Int, b: Int): Unit {
    println(a + b)
}
```

Kotlin también admite funciones de orden superior, que son funciones que toman otras funciones como parámetros de entrada. Las funciones de orden superior se pueden utilizar para crear código conciso y legible.

Aquí hay una función simple de orden superior que toma una función como entrada y ejecuta esa función:

```kotlin
fun execute(f: () -> Unit) {
    f()
}
```

La función ```ejecutar``` anterior se puede usar para ejecutar cualquier función que no tome ningún parámetro de entrada y no devuelva un valor.

Ahora que conoce los conceptos básicos de las funciones de Kotlin, pasemos a las clases y objetos de Kotlin.

## Clases y objetos de Kotlin

En Kotlin, una clase es una plantilla para crear objetos. Una clase puede tener propiedades y métodos.

Aquí hay una clase ```Persona``` simple con dos propiedades: ```nombre``` y ```edad```.

```kotlin
class Person(val name: String, val age: Int)
```

Para crear un objeto a partir de una clase, debe usar la palabra clave ```nuevo```.

```kotlin
val person = new Person("John", 30)
```

Kotlin también es compatible con la programación orientada a objetos. En Kotlin, un objeto es un singleton: solo puede haber una instancia de un objeto.

Aquí hay un simple objeto ```Logger``` con un método ```log()```.

```kotlin
object Logger {
    fun log(message: String) {
        println(message)
    }
}
```

Para usar el objeto ```Logger```, no necesita crear una instancia del mismo. Simplemente puede llamar directamente al método ```log()```.

```kotlin
Logger.log("This is a log message")
```

Ahora que conoce los conceptos básicos de las clases y los objetos de Kotlin, ¡está listo para comenzar a programar en Kotlin!