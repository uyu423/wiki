---
title: 073: El patrón Flyweight en Kotlin: compartir instancias de objetos para ahorrar memoria
description: 
published: true
date: 2023-02-07T06:55:43.464Z
tags: 
editor: markdown
dateCreated: 2023-02-07T06:55:41.862Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [073: The Flyweight Pattern in Kotlin: Sharing Object Instances to Save Memory***English** document is available*](/en/Knowledge-base/Kotlin/Learning/073-the-flyweight-pattern-in-kotlin-sharing-object-instances-to-save-memory)
{.links-list}


# El patrón Flyweight en Kotlin: compartir instancias de objetos para ahorrar memoria

Cuando se trata de desarrollar software, una de las consideraciones clave es cómo usar la memoria de manera eficiente. Una forma de optimizar el uso de la memoria es utilizar el patrón de peso ligero.

El patrón flyweight es un patrón de diseño que ayuda a ahorrar memoria al compartir instancias de objetos. Esto es especialmente útil cuando tiene una gran cantidad de objetos que comparten un estado similar.

En esta publicación, veremos cómo usar el patrón de peso mosca en Kotlin. Comenzaremos analizando qué es el patrón de peso mosca y cómo funciona. Luego veremos algunos ejemplos de cómo usar el patrón de peso ligero en Kotlin.

## ¿Qué es el patrón de peso mosca?

El patrón flyweight es un patrón de diseño que ayuda a ahorrar memoria al compartir instancias de objetos. Esto es especialmente útil cuando tiene una gran cantidad de objetos que comparten un estado similar.

En el patrón de peso mosca, el estado de un objeto se divide en dos partes:

* **Estado intrínseco**: Este es el estado que comparten todos los objetos del mismo tipo.
* **Estado extrínseco**: Este es el estado que es único para cada objeto.

El estado intrínseco se almacena en un objeto de peso mosca. El estado extrínseco se almacena fuera del objeto flyweight, en el objeto cliente.

Cuando un objeto cliente necesita acceder al objeto flyweight, pasa al estado extrínseco como argumento. El objeto flyweight luego usa el estado extrínseco para devolver el resultado correcto.

## ¿Cómo funciona el patrón de peso mosca?

El patrón flyweight funciona compartiendo instancias de objetos. Esto es especialmente útil cuando tiene una gran cantidad de objetos que comparten un estado similar.

En el patrón de peso mosca, el estado de un objeto se divide en dos partes:

* **Estado intrínseco**: Este es el estado que comparten todos los objetos del mismo tipo.
* **Estado extrínseco**: Este es el estado que es único para cada objeto.

El estado intrínseco se almacena en un objeto de peso mosca. El estado extrínseco se almacena fuera del objeto flyweight, en el objeto cliente.

Cuando un objeto cliente necesita acceder al objeto flyweight, pasa al estado extrínseco como argumento. El objeto flyweight luego usa el estado extrínseco para devolver el resultado correcto.

## Ejemplos del patrón de peso mosca

Ahora que hemos visto cómo funciona el patrón de peso mosca, veamos algunos ejemplos de cómo usar el patrón de peso mosca en Kotlin.

### Ejemplo 1: Creación de un objeto de peso mosca

En este ejemplo, crearemos un objeto flyweight que almacene el estado intrínseco de un usuario.


```kotlin
// The flyweight object
class User(val name: String) {

}

// The client object
class UserClient(val user: User) {

    fun doSomething() {
        // Use the user object
    }
}

// Create a flyweight object
val user = User("John Smith")

// Create a client object
val userClient = UserClient(user)

// Use the client object
userClient.doSomething()
```

En este ejemplo, hemos creado un objeto flyweight que almacena el estado intrínseco de un usuario. También hemos creado un objeto de cliente que utiliza el objeto flyweight.

### Ejemplo 2: Paso en estado extrínseco

En este ejemplo, crearemos un objeto flyweight que almacene el estado intrínseco de un usuario. También crearemos un objeto de cliente que use el objeto flyweight.

Cuando el objeto del cliente necesite usar el objeto flyweight, pasará al estado extrínseco como argumento.


```kotlin
// The flyweight object
class User(val name: String) {

    fun doSomething(state: String) {
        // Use the user object
    }
}

// The client object
class UserClient(val user: User) {

    fun doSomething() {
        // Pass in the extrinsic state
        user.doSomething("John Smith")
    }
}

// Create a flyweight object
val user = User("John Smith")

// Create a client object
val userClient = UserClient(user)

// Use the client object
userClient.doSomething()
```

En este ejemplo, hemos creado un objeto flyweight que almacena el estado intrínseco de un usuario. También hemos creado un objeto de cliente que utiliza el objeto flyweight.

Cuando el objeto del cliente necesita usar el objeto flyweight, pasa al estado extrínseco como argumento.