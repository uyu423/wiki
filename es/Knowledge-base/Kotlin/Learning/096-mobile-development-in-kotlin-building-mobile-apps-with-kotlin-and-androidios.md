---
title: 096: Desarrollo móvil en Kotlin: creación de aplicaciones móviles con Kotlin y Android/iOS
description: 
published: true
date: 2023-02-14T12:18:36.616Z
tags: 
editor: markdown
dateCreated: 2023-02-14T12:18:29.045Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [096: Mobile Development in Kotlin: Building Mobile Apps with Kotlin and Android/iOS***English** document is available*](/en/Knowledge-base/Kotlin/Learning/096-mobile-development-in-kotlin-building-mobile-apps-with-kotlin-and-androidios)
{.links-list}


# 096: Desarrollo móvil en Kotlin: creación de aplicaciones móviles con Kotlin y Android/iOS

Kotlin es un lenguaje de programación de tipo estático que se ejecuta en la máquina virtual de Java y también se puede compilar en el código fuente de JavaScript. Kotlin es desarrollado por JetBrains, la compañía detrás de IntelliJ IDEA Java IDE.

Kotlin fue diseñado para ser una versión mejorada de Java y ofrece una serie de funciones que Java no ofrece. Kotlin es totalmente interoperable con Java, por lo que puede usarse para desarrollar aplicaciones de Android.

En esta publicación, veremos cómo comenzar con Kotlin y el desarrollo de Android. Crearemos un simple "¡Hola, mundo!" aplicación y luego ejecútela en un dispositivo Android.

## Empezando

Para comenzar, deberá instalar el complemento Kotlin para IntelliJ IDEA. Puede hacerlo desde el IDE yendo a Preferencias > Complementos y buscando "Kotlin".

Una vez que se instala el complemento de Kotlin, puede crear un nuevo proyecto de Kotlin yendo a Archivo > Nuevo > Proyecto y seleccionando "Kotlin/JVM" de la lista de plantillas de proyecto.

## Creando un Proyecto Kotlin

Una vez que haya creado un proyecto de Kotlin, puede crear un nuevo archivo de Kotlin yendo a Archivo > Nuevo > Archivo/clase de Kotlin.

Vamos a crear un archivo llamado "HelloWorld.kt" en el directorio src/ de nuestro proyecto. Comenzaremos agregando una función principal a nuestro archivo:

```kotlin
fun main(args: Array<String>) {
    println("Hello, World!")
}
```

Esta función imprime la cadena "¡Hola, mundo!" a la consola

## Ejecutar la aplicación

Para ejecutar nuestra aplicación Kotlin, necesitaremos crear una configuración de ejecución. Podemos hacer esto yendo a Ejecutar > Editar configuraciones y haciendo clic en el botón "+".

En la lista de tipos de configuración de ejecución, seleccione "Kotlin/JVM". Nombraremos nuestra configuración "Hello, World!" y establezca la clase principal en "HelloWorldKt".

Finalmente, necesitaremos seleccionar un dispositivo para ejecutar nuestra aplicación. Podemos hacer esto yendo a Ejecutar> Editar configuraciones y seleccionando nuestro "¡Hola, mundo!" configuración. En el menú desplegable "Dispositivo", seleccione el dispositivo que desea usar.

¡Ahora estamos listos para ejecutar nuestra aplicación Kotlin en nuestro dispositivo Android!