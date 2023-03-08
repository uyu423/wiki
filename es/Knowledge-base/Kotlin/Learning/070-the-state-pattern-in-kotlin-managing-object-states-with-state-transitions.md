---
title: 070: El patrón de estado en Kotlin: gestión de estados de objetos con transiciones de estado
description: 
published: true
date: 2023-02-14T20:17:23.772Z
tags: 
editor: markdown
dateCreated: 2023-02-14T20:17:22.219Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [070: The State Pattern in Kotlin: Managing Object States with State Transitions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/070-the-state-pattern-in-kotlin-managing-object-states-with-state-transitions)
{.links-list}


# 070: El patrón de estado en Kotlin: gestión de estados de objetos con transiciones de estado

Kotlin es un poderoso lenguaje de programación que ofrece muchas funciones para los desarrolladores. Una de esas características es el patrón de estado, que permite a los desarrolladores administrar los estados de los objetos con transiciones de estado. En esta publicación, veremos qué es el patrón de estado y cómo se puede usar en Kotlin.

## ¿Qué es el patrón de estado?

El patrón de estado es un patrón de diseño de comportamiento que ayuda a administrar los estados de los objetos. Con este patrón, un objeto puede cambiar su comportamiento en función de su estado interno. Esto es útil cuando un objeto necesita cambiar su comportamiento en función de las condiciones cambiantes.

Por ejemplo, considere un interruptor de luz. Cuando el interruptor está en la posición "on", la luz se enciende. Cuando el interruptor está en la posición de "apagado", la luz se apaga. El patrón de estado se puede utilizar para modelar este comportamiento.

## Cómo usar el patrón de estado en Kotlin

Kotlin facilita el uso del patrón de estado. Primero, necesitamos crear una clase sellada que represente los diferentes estados en los que puede estar un objeto. En nuestro ejemplo de interruptor de luz, tenemos dos estados: "encendido" y "apagado".

```kotlin
sealed class LightSwitchState {
    object On : LightSwitchState()
    object Off : LightSwitchState()
}
```

A continuación, necesitamos crear una clase que represente el objeto cuyo estado queremos administrar. En nuestro ejemplo, este es el interruptor de luz.

```kotlin
class LightSwitch {
    var state: LightSwitchState = LightSwitchState.Off
        private set

    fun turnOn() {
        state = LightSwitchState.On
    }

    fun turnOff() {
        state = LightSwitchState.Off
    }
}
```

En la clase ```LightSwitch```, tenemos una propiedad ```state``` que representa el estado actual del interruptor de luz. También tenemos los métodos ```turnOn()``` y ```turnOff()``` que se pueden usar para cambiar el estado del interruptor de la luz.

Ahora que tenemos configurado nuestro patrón de estado, podemos usarlo para modelar el comportamiento de nuestro interruptor de luz.

```kotlin
val lightSwitch = LightSwitch()

lightSwitch.turnOn()
// The light is now on

lightSwitch.turnOff()
// The light is now off
```

Como puede ver, el patrón de estado facilita la gestión del estado de un objeto. En nuestro ejemplo del interruptor de luz, pudimos encender y apagar la luz fácilmente cambiando el estado del interruptor de luz.

## Cuándo usar el patrón de estado

El patrón de estado es una herramienta útil para gestionar estados de objetos. Sin embargo, es importante saber cuándo usar este patrón. El patrón de estado debe usarse cuando:

- El comportamiento de un objeto debe cambiar en función de su estado interno.
- Un objeto necesita poder cambiar su estado interno

En nuestro ejemplo del interruptor de luz, usamos el patrón de estado porque necesitábamos poder cambiar el estado del interruptor de luz. Esto nos permitió encender y apagar fácilmente la luz.

## Información adicional

El patrón de estado es una herramienta poderosa que se puede usar para administrar los estados de los objetos. Sin embargo, es importante saber cuándo usar este patrón. Utilice el patrón de estado cuando el comportamiento de un objeto necesite cambiar en función de su estado interno.