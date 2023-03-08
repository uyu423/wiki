---
title: 072: El patrón mediador en Kotlin: encapsulando la comunicación de objetos
description: 
published: true
date: 2023-02-03T15:17:29.741Z
tags: 
editor: markdown
dateCreated: 2023-02-03T15:17:28.151Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [072: The Mediator Pattern in Kotlin: Encapsulating Object Communication***English** document is available*](/en/Knowledge-base/Kotlin/Learning/072-the-mediator-pattern-in-kotlin-encapsulating-object-communication)
{.links-list}


# 072: El Patrón Mediador en Kotlin: Encapsulando la Comunicación de Objetos

El patrón mediador es un patrón de diseño de software de comportamiento que permite la comunicación entre objetos sin necesidad de que se conozcan entre sí. Esto puede ser útil en situaciones donde existe la necesidad de centralizar el control o reducir las dependencias entre objetos.

En esta publicación, veremos cómo se puede implementar el patrón de mediador en Kotlin. Comenzaremos observando un ejemplo simple de cómo se puede usar el patrón para desacoplar objetos. Luego veremos un ejemplo más realista que hace uso de la biblioteca estándar de Kotlin.

## Un ejemplo sencillo

Supongamos que tenemos una clase que representa una sala de chat:

```kotlin
class ChatRoom {
    fun showMessage(user: User, message: String) {
        println("${user.name}: $message")
    }
}
```

Y una clase que representa a un usuario:

```kotlin
class User(val name: String) {
    fun sendMessage(message: String) {
        ChatRoom.showMessage(this, message)
    }
}
```

En este ejemplo simple, la clase `ChatRoom` actúa como mediador entre los objetos `Usuario`. Los objetos 'Usuario' no se conocen entre sí, solo conocen el objeto 'ChatRoom'.

## Un ejemplo más realista

En un ejemplo más realista, podríamos querer desacoplar la clase `Usuario` de la clase `ChatRoom`. Podemos hacer esto usando el patrón mediador.

Primero, crearemos una interfaz `ChatRoom`:

```kotlin
interface ChatRoom {
    fun showMessage(user: User, message: String)
}
```

Luego crearemos una interfaz de `Usuario`:

```kotlin
interface User {
    fun sendMessage(message: String)
}
```

Ahora podemos crear una implementación `ChatRoom`:

```kotlin
class DefaultChatRoom : ChatRoom {
    override fun showMessage(user: User, message: String) {
        println("${user.name}: $message")
    }
}
```

Y una implementación `Usuario`:

```kotlin
class DefaultUser(override val name: String) : User {
    override fun sendMessage(message: String) {
        DefaultChatRoom.showMessage(this, message)
    }
}
```

En este ejemplo, las clases `DefaultChatRoom` y `DefaultUser` están desacopladas entre sí. Solo se conocen entre sí a través de las interfaces que implementan.

## Conclusión

El patrón mediador es un patrón útil para desacoplar objetos entre sí. Se puede utilizar para centralizar el control o reducir las dependencias entre objetos. En Kotlin, el patrón se puede implementar mediante interfaces.