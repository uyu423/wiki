---
title: 067: The Abstract Factory Pattern en Kotlin: creación de objetos a través de interfaces abstractas
description: 
published: true
date: 2023-02-06T22:17:40.556Z
tags: 
editor: markdown
dateCreated: 2023-02-06T22:17:33.770Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [067: The Abstract Factory Pattern in Kotlin: Creating Objects Through Abstract Interfaces***English** document is available*](/en/Knowledge-base/Kotlin/Learning/067-the-abstract-factory-pattern-in-kotlin-creating-objects-through-abstract-interfaces)
{.links-list}


# The Abstract Factory Pattern en Kotlin: creación de objetos a través de interfaces abstractas

El patrón Abstract Factory es un patrón de diseño creacional que nos permite crear objetos a través de interfaces abstractas. Este patrón es particularmente útil cuando necesitamos crear objetos que forman parte de un sistema más grande, como una GUI o una base de datos.

En esta publicación, veremos cómo usar el patrón Abstract Factory en Kotlin. Comenzaremos analizando el problema que resuelve este patrón. Luego veremos cómo implementar el patrón en Kotlin. Finalmente, veremos algunos de los beneficios y desventajas de usar este patrón.

## El problema

Considere una aplicación GUI simple que consta de una ventana con un botón. Podemos crear esta ventana usando el patrón Abstract Factory de la siguiente manera:

```kotlin
interface Window {
    fun draw()
}

class Button(val window: Window) {
    fun draw() {
        // ...
    }
}

class Application {
    val window: Window

    init {
        window = WindowFactory.createWindow()
    }

    fun addButton(button: Button) {
        // ...
    }
}

object WindowFactory {
    fun createWindow(): Window {
        // ...
    }
}
```

En este ejemplo, tenemos una interfaz para una ventana y una implementación concreta de esa interfaz. También tenemos una clase de botón que toma una ventana como parámetro. Finalmente, tenemos una clase de aplicación que crea una ventana y le agrega botones.

El patrón Abstract Factory nos permite desacoplar la creación de la ventana del resto de la aplicación. Esto es particularmente útil cuando necesitamos admitir múltiples plataformas, como Windows y macOS. Simplemente podemos crear una nueva WindowFactory para cada plataforma y el resto de la aplicación seguirá funcionando como antes.

## Implementación

Veamos ahora cómo implementar el patrón Abstract Factory en Kotlin. Comenzaremos mirando la interfaz de nuestra ventana:

```kotlin
interface Window {
    fun draw()
}
```

A continuación, crearemos una implementación concreta de esta interfaz para nuestra plataforma Windows:

```kotlin
class WindowsWindow : Window {
    override fun draw() {
        // ...
    }
}
```

Ahora podemos crear una WindowsWindowFactory que devolverá instancias de nuestra clase WindowsWindow:

```kotlin
class WindowsWindowFactory : WindowFactory {
    override fun createWindow(): Window {
        return WindowsWindow()
    }
}
```

Ahora podemos crear una macOSWindowFactory que devolverá instancias de nuestra clase macOSWindow:

```kotlin
class macOSWindowFactory : WindowFactory {
    override fun createWindow(): Window {
        return macOSWindow()
    }
}
```

Finalmente, podemos actualizar nuestra clase de aplicación para usar nuestra nueva WindowFactory:

```kotlin
class Application {
    val window: Window

    init {
        window = WindowFactory.createWindow()
    }

    fun addButton(button: Button) {
        // ...
    }
}
```

## Beneficios

Hay varios beneficios al usar el patrón Abstract Factory:

- El patrón nos permite desacoplar la creación de objetos del resto de nuestro código. Esto es particularmente útil cuando necesitamos soportar múltiples plataformas.

- El patrón es fácil de extender. Por ejemplo, podemos agregar fácilmente una nueva plataforma creando una nueva WindowFactory.

- El patrón promueve el uso de interfaces. Esto puede ser beneficioso para la reutilización y el mantenimiento del código.

## Inconvenientes

También existen algunos inconvenientes al usar el patrón Abstract Factory:

- El patrón puede dar lugar a una gran cantidad de código repetitivo.

- El patrón puede ser difícil de entender y usar.