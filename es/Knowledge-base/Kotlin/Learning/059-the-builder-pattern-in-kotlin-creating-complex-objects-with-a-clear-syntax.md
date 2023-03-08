---
title: 059: El patrón Builder en Kotlin: creación de objetos complejos con una sintaxis clara
description: 
published: true
date: 2023-02-16T20:32:34.912Z
tags: 
editor: markdown
dateCreated: 2023-02-16T20:32:26.452Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [059: The Builder Pattern in Kotlin: Creating Complex Objects with a Clear Syntax***English** document is available*](/en/Knowledge-base/Kotlin/Learning/059-the-builder-pattern-in-kotlin-creating-complex-objects-with-a-clear-syntax)
{.links-list}


# 059: El Patrón Constructor en Kotlin: Creando Objetos Complejos con una Sintaxis Clara

El patrón Builder es un patrón de diseño creacional que permite la construcción de objetos complejos con una sintaxis clara. A menudo se usa junto con el patrón Factory Method.

El patrón Builder es una buena opción cuando necesita crear objetos complejos con muchos campos diferentes. El patrón Builder le permite crear estos objetos paso a paso, sin tener que escribir mucho código.

En Kotlin, el patrón Builder se usa a menudo para crear clases de datos. Las clases de datos son clases que contienen solo datos, sin ningún comportamiento. A menudo se utilizan para almacenar datos que se leen de un archivo o una base de datos.

Las clases de datos generalmente se crean utilizando la palabra clave de clase de datos. Sin embargo, si necesita crear una clase de datos con muchos campos, la palabra clave de la clase de datos puede volverse bastante detallada. En tales casos, el patrón Builder se puede utilizar para crear la clase de datos.

El patrón Builder también es útil cuando necesita crear objetos inmutables. Los objetos inmutables son objetos que no se pueden modificar después de su creación. A menudo se utilizan para almacenar datos que no deben modificarse, como los datos de configuración.

La biblioteca estándar de Kotlin contiene una serie de funciones útiles para crear objetos inmutables. Por ejemplo, la función toImmutableList() se puede usar para crear una lista inmutable a partir de una lista mutable.

Para usar el patrón Builder, debe crear una clase que contenga varios campos. Estos campos serán establecidos por el constructor. La clase también debe contener un constructor que tome un constructor como argumento.

El constructor es una clase separada que contiene métodos para configurar los campos del objeto. El constructor también tiene un método para crear el objeto. Este método toma todos los campos que se han establecido y crea una instancia del objeto.

Aquí hay un ejemplo de una clase de datos que usa el patrón Builder:

usuario de clase de datos (
    nombre de valor: Cadena,
    valor: Int,
    dirección de valor: Cadena
) {
    constructor de clases {
        nombre de la variable: cadena = ""
        var edad: Int = 0
        var dirección: Cadena = ""
 
        compilación divertida(): Usuario {
            volver Usuario (nombre, edad, dirección)
        }
    }
}

Como puede ver, la clase Usuario contiene tres campos. Estos campos los establece el constructor. La clase también contiene un constructor que toma un constructor como argumento.

El constructor es una clase separada que contiene métodos para configurar los campos del objeto. El constructor también tiene un método para crear el objeto. Este método toma todos los campos que se han establecido y crea una instancia del objeto.

Para usar el patrón Builder, primero debe crear un constructor. Puedes hacer esto usando la función builder():

val usuario = Usuario.Builder().apply {
    nombre = "Juan"
    edad = 30
    dirección = "Londres"
}.construir()

La función builder() crea un nuevo objeto constructor. La función apply() se usa para llamar a métodos en el objeto constructor. En este caso, los métodos se utilizan para establecer los campos del objeto Usuario.

Finalmente, se llama al método build() para crear el objeto Usuario. El objeto Usuario creado por el constructor es inmutable.

El patrón Builder es una forma útil de crear objetos complejos con una sintaxis clara. También es una buena opción cuando necesita crear objetos inmutables.