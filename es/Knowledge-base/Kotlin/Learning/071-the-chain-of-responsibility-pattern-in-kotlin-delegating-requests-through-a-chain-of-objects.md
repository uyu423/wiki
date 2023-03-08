---
title: 071: El patrón de cadena de responsabilidad en Kotlin: Delegar solicitudes a través de una cadena de objetos
description: 
published: true
date: 2023-02-17T04:33:28.458Z
tags: 
editor: markdown
dateCreated: 2023-02-17T04:32:36.351Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [071: The Chain of Responsibility Pattern in Kotlin: Delegating Requests Through a Chain of Objects***English** document is available*](/en/Knowledge-base/Kotlin/Learning/071-the-chain-of-responsibility-pattern-in-kotlin-delegating-requests-through-a-chain-of-objects)
{.links-list}


## Introducción

El patrón de cadena de responsabilidad es un patrón de diseño que implica pasar solicitudes a lo largo de una cadena de objetos para encontrar el controlador adecuado. Este patrón se usa a menudo junto con el decorador y los patrones de comando.

## El problema

Supongamos que tenemos un sistema con varios objetos que pueden manejar solicitudes. Cada objeto tiene una cierta responsabilidad y puede gestionar la solicitud o pasarla al siguiente objeto de la cadena.

El problema es que puede ser difícil determinar qué objeto debe manejar una solicitud en particular. También es posible que queramos añadir o quitar objetos de la cadena sin tener que cambiar el código que hace la petición.

## La solución

El patrón de cadena de responsabilidad resuelve estos problemas al crear una cadena de objetos que pueden manejar la solicitud. Los objetos se vinculan entre sí y la solicitud se pasa de un objeto al siguiente hasta que se gestiona.

## Implementación

Veamos cómo podemos implementar el patrón de cadena de responsabilidad en Kotlin.

Comenzaremos creando una clase para la solicitud:

```kotlin
class Request(val data: String)
```

A continuación, crearemos una clase para los controladores. Cada controlador tendrá una referencia al siguiente controlador en la cadena:

```kotlin
abstract class Handler(protected var next: Handler?) {

    fun handle(request: Request) {
        if (canHandle(request)) {
            doHandle(request)
        } else {
            next?.handle(request)
        }
    }

    abstract fun canHandle(request: Request): Boolean

    abstract fun doHandle(request: Request)
}
```

Finalmente, crearemos algunas clases concretas para los controladores:

```kotlin
class FirstHandler : Handler(null) {

    override fun canHandle(request: Request): Boolean {
        return request.data.startsWith("first")
    }

    override fun doHandle(request: Request) {
        println("First handler handling request: ${request.data}")
    }
}

class SecondHandler : Handler(null) {

    override fun canHandle(request: Request): Boolean {
        return request.data.startsWith("second")
    }

    override fun doHandle(request: Request) {
        println("Second handler handling request: ${request.data}")
    }
}

class ThirdHandler : Handler(null) {

    override fun canHandle(request: Request): Boolean {
        return request.data.startsWith("third")
    }

    override fun doHandle(request: Request) {
        println("Third handler handling request: ${request.data}")
    }
}
```

Ahora podemos crear una cadena de controladores y pasar solicitudes a través de la cadena:

```kotlin
val firstHandler = FirstHandler()
val secondHandler = SecondHandler()
val thirdHandler = ThirdHandler()

firstHandler.next = secondHandler
secondHandler.next = thirdHandler

val request = Request("first request")
firstHandler.handle(request)

val request2 = Request("second request")
firstHandler.handle(request2)

val request3 = Request("third request")
firstHandler.handle(request3)
```

## Ventajas

La principal ventaja del patrón de cadena de responsabilidad es que nos permite desacoplar el remitente de una solicitud del receptor. El remitente no necesita saber quién es el destinatario o cómo se manejará la solicitud.

Otra ventaja es que podemos agregar o quitar manejadores de la cadena dinámicamente sin tener que cambiar el código que hace la solicitud.

## Desventajas

Una desventaja del patrón de cadena de responsabilidad es que puede ser difícil de depurar porque puede ser difícil determinar dónde se está manejando una solicitud.

Otra desventaja es que el patrón de cadena de responsabilidad puede conducir a un código que es difícil de mantener.

## Conclusión

En esta publicación, hemos visto cómo implementar el patrón de cadena de responsabilidad en Kotlin. Este patrón puede ser útil para desvincular al remitente de una solicitud del receptor y para agregar o eliminar dinámicamente controladores de la cadena.