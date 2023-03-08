---
title: 086: Kotlin en Android: creación de aplicaciones de Android con Kotlin
description: 
published: true
date: 2023-02-15T12:18:01.796Z
tags: 
editor: markdown
dateCreated: 2023-02-15T12:17:59.347Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [086: Kotlin on Android: Building Android Apps with Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/Learning/086-kotlin-on-android-building-android-apps-with-kotlin)
{.links-list}


# 086: Kotlin en Android: Creación de aplicaciones de Android con Kotlin

Kotlin es un poderoso lenguaje de programación que se puede usar para crear aplicaciones de Android. En esta publicación, veremos cómo comenzar con Kotlin en Android.

## Instalación de Kotlin

Para comenzar con Kotlin en Android, primero debe instalar el complemento de Kotlin. Puede hacerlo desde Android Studio yendo a Archivo > Configuración > Complementos y buscando el complemento de Kotlin. Una vez que haya instalado el complemento, deberá reiniciar Android Studio.

Una vez que Android Studio se haya reiniciado, podrá crear un nuevo proyecto de Kotlin. Para hacer esto, vaya a Archivo > Nuevo > Nuevo proyecto y seleccione la opción Kotlin de la lista de tipos de proyectos.

## Creando un Proyecto Kotlin

Una vez que haya instalado el complemento de Kotlin, puede crear un nuevo proyecto de Kotlin. Para hacer esto, vaya a Archivo > Nuevo > Nuevo proyecto y seleccione la opción Kotlin de la lista de tipos de proyectos.

Cuando cree un nuevo proyecto de Kotlin, se le pedirá que especifique el nombre y la ubicación del proyecto, así como el SDK del proyecto. Una vez que haya especificado estos detalles, haga clic en el botón Finalizar para crear el proyecto.

## Crear un archivo Kotlin

Una vez que haya creado un proyecto de Kotlin, puede crear un archivo de Kotlin. Para hacer esto, vaya a Archivo > Nuevo > Archivo/clase de Kotlin.

Cuando cree un nuevo archivo Kotlin, se le pedirá que especifique el nombre y la ubicación del archivo. También se le pedirá que especifique el tipo de archivo Kotlin. Hay cuatro tipos de archivos Kotlin:

- Clase Kotlin
- Archivo Kotlin
- Objeto Kotlin
- Interfaz Kotlin

Una vez que haya especificado el nombre y la ubicación del archivo, haga clic en el botón Finalizar para crear el archivo.

## Escribir código Kotlin

Ahora que ha creado un proyecto Kotlin y un archivo Kotlin, está listo para comenzar a escribir código Kotlin.

El código de Kotlin está escrito en archivos con la extensión .kt. Los archivos de Kotlin pueden contener una o más declaraciones de nivel superior. Una declaración de nivel superior es una declaración que no está dentro de una clase, objeto o interfaz.

Kotlin tiene un amplio conjunto de características que lo convierten en una excelente opción para desarrollar aplicaciones de Android. Algunas de estas características incluyen:

- Seguridad nula
- Funciones de extensión
- Clases de datos
- Corrutinas

En la siguiente sección, veremos algunas de estas características con más detalle.

## Seguridad nula

Una de las características más importantes de Kotlin es la seguridad nula. La seguridad nula es una función que evita que se produzcan excepciones de puntero nulo.

Para hacer que una variable nula sea segura, debe usar el ? operador. Por ejemplo, el siguiente código no se compilará porque la variable de nombre puede ser nula:

```kotlin
var name: String = "John"
name = null
```

Para hacer que el código nulo sea seguro, debe usar el ? operador:

```kotlin
var name: String? = "John"
name = null
```

Ahora el código se compilará porque la variable de nombre puede ser nula.

## Funciones de extensión

Otra característica importante de Kotlin son las funciones de extensión. Las funciones de extensión le permiten extender una clase con nueva funcionalidad sin tener que subclasificarla.

Por ejemplo, suponga que tiene una clase con una función isEmpty() que devuelve verdadero si la clase está vacía y falso si no lo está. Puede ampliar esta clase con una nueva función isNotEmpty() que devuelve lo contrario de isEmpty():

```kotlin
fun isNotEmpty(): Boolean {
    return !isEmpty()
}
```

Para usar la nueva función, simplemente necesita llamarla en una instancia de la clase:

```kotlin
val list = ArrayList<String>()
list.isNotEmpty() // returns false
```

## Clases de datos

Kotlin también tiene soporte para clases de datos. Las clases de datos son clases diseñadas para contener datos. Son similares a JavaBeans, pero son mucho más simples de crear y usar.

Para crear una clase de datos, debe usar la palabra clave de datos:

```kotlin
data class User(val name: String, val age: Int)
```

Este código crea una clase de datos con dos propiedades: nombre y edad. Las propiedades se declaran con la palabra clave val, lo que significa que son de solo lectura.

Para crear una instancia de la clase de datos, simplemente necesita llamar al constructor:

```kotlin
val user = User("John", 30)
```

Para acceder a las propiedades de la clase de datos, puede utilizar la notación de puntos:

```kotlin
user.name // returns "John"
user.age // returns 30
```

Las clases de datos también tienen varias funciones útiles, como toString(), hashCode() y equals():

```kotlin
user.toString() // returns "User(name=John, age=30)"
user.hashCode() // returns -1234
user.equals(other) // returns true if the two objects are equal
```

## Corrutinas

Las rutinas son una característica nueva de Kotlin que facilita la escritura de código asincrónico. Las corrutinas son similares a los hilos, pero son mucho más ligeras y se pueden suspender sin bloquear un hilo.

Para usar coroutines, debe importar el paquete kotlinx.coroutines:

```kotlin
import kotlinx.coroutines.*
```

Luego, puedes usar la función launch() para lanzar una nueva rutina:

```kotlin
GlobalScope.launch {
    // suspendable code
}
```

Dentro de la función launch(), puede escribir código suspendible. Este código se puede suspender sin bloquear un hilo.

Para suspender una rutina, puedes usar la función delay():

```kotlin
GlobalScope.launch {
    delay(1000) // suspend for 1 second
    // resume here
}
```

La función delay() toma un argumento de tiempo en milisegundos. La rutina se reanudará una vez transcurrido el tiempo especificado.

También puede usar la función yield() para suspender una rutina y permitir que se ejecuten otras rutinas:

```kotlin
GlobalScope.launch {
    yield() // suspend and allow other coroutines to run
    // resume here
}
```

## Conclusión

En esta publicación, hemos visto cómo comenzar con Kotlin en Android. Hemos visto cómo instalar el complemento Kotlin, crear un proyecto Kotlin y escribir código Kotlin. También hemos visto algunas de las características que hacen de Kotlin una excelente opción para desarrollar aplicaciones de Android.