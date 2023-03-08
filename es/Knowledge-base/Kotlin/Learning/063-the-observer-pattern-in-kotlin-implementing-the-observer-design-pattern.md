---
title: 063: El patrón Observer en Kotlin: Implementando el patrón de diseño Observer
description: 
published: true
date: 2023-02-17T00:32:41.708Z
tags: 
editor: markdown
dateCreated: 2023-02-17T00:32:33.163Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [063: The Observer Pattern in Kotlin: Implementing the Observer Design Pattern***English** document is available*](/en/Knowledge-base/Kotlin/Learning/063-the-observer-pattern-in-kotlin-implementing-the-observer-design-pattern)
{.links-list}


# El patrón Observer en Kotlin: Implementando el patrón de diseño Observer

El patrón de observador es un patrón de diseño de software en el que un objeto, llamado sujeto, mantiene una lista de sus dependientes, llamados observadores, y les notifica automáticamente cualquier cambio de estado, generalmente llamando a uno de sus métodos.

Es un patrón muy útil para implementar sistemas controlados por eventos y también es uno de los patrones de diseño de comportamiento.

## ¿Qué es el patrón del observador?

El patrón de observador es un patrón de diseño de software en el que un objeto, llamado sujeto, mantiene una lista de sus dependientes, llamados observadores, y les notifica automáticamente cualquier cambio de estado, generalmente llamando a uno de sus métodos.

Es un patrón muy útil para implementar sistemas controlados por eventos y también es uno de los patrones de diseño de comportamiento.

El Patrón del Observador tiene los siguientes participantes:
- Sujeto: el objeto que mantiene una lista de observadores y les notifica los cambios de estado
- Observer: la interfaz que deben implementar los objetos para ser notificados de los cambios de estado en el sujeto
- ConcreteObserver: el objeto que implementa la interfaz de Observer y es notificado de los cambios de estado en el sujeto

## ¿Cuándo usar el patrón de observador?

El patrón de observador se utiliza en las siguientes situaciones:
- Cuando una abstracción tiene dos aspectos, uno dependiente del otro. Encapsular estos aspectos en objetos separados le permite variarlos y reutilizarlos de forma independiente
- Cuando un cambio en un objeto requiere cambiar otros y no sabe cuántos objetos necesita cambiar
- Cuando un objeto debería poder notificar a otros objetos sin hacer suposiciones sobre quiénes son estos objetos. En otras palabras, no desea que estos objetos estén estrechamente acoplados

## ¿Cómo implementar el patrón Observer en Kotlin?

Kotlin no tiene un patrón de observador incorporado, pero es fácil de implementar.

Primero, creemos la interfaz Asunto:

```kotlin
interface Subject {
    fun addObserver(observer: Observer)
    fun removeObserver(observer: Observer)
    fun notifyObservers()
}
```

Como puede ver, la interfaz Asunto tiene tres métodos:
- addObserver(observer: Observer): para agregar un observador a la lista de observadores
- removeObserver(observer: Observer): para eliminar un observador de la lista de observadores
- notificar a los observadores (): para notificar a todos los observadores que el estado del sujeto ha cambiado

Ahora vamos a crear la interfaz de Observer:

```kotlin
interface Observer {
    fun update(subject: Subject)
}
```

La interfaz de Observer tiene un solo método:
- actualizar(sujeto: Sujeto): para ser llamado cuando el estado del sujeto ha cambiado. Este método toma al sujeto como parámetro para que el observador pueda consultar el estado del sujeto si es necesario.

Ahora vamos a crear una clase ConcreteSubject que implemente la interfaz Subject:

```kotlin
class ConcreteSubject : Subject {

    private val observers = mutableListOf<Observer>()
    private var state: Int = 0

    override fun addObserver(observer: Observer) {
        observers.add(observer)
    }

    override fun removeObserver(observer: Observer) {
        observers.remove(observer)
    }

    override fun notifyObservers() {
        for (observer in observers) {
            observer.update(this)
        }
    }

    fun setState(state: Int) {
        this.state = state
        notifyObservers()
    }

    fun getState(): Int {
        return state
    }
}
```

Como puede ver, la clase ConcreteSubject mantiene una lista de observadores y les notifica cuando cambia el estado del sujeto.

Finalmente, creemos una clase ConcreteObserver que implemente la interfaz Observer:

```kotlin
class ConcreteObserver : Observer {

    private var state: Int = 0

    override fun update(subject: Subject) {
        state = subject.getState()
    }

    fun getState(): Int {
        return state
    }
}
```

La clase ConcreteObserver simplemente almacena el estado del sujeto y proporciona un método getter para acceder a él.

## Probando el patrón del observador

Ahora escribamos una prueba para ver el patrón de observador en acción:

```kotlin
import org.junit.Test
import kotlin.test.assertEquals

class ObserverPatternTest {

    @Test
    fun testObserverPattern() {
        val subject = ConcreteSubject()

        val observer1 = ConcreteObserver()
        val observer2 = ConcreteObserver()

        subject.addObserver(observer1)
        subject.addObserver(observer2)

        subject.setState(1)
        assertEquals(1, observer1.getState())
        assertEquals(1, observer2.getState())

        subject.setState(2)
        assertEquals(2, observer1.getState())
        assertEquals(2, observer2.getState())

        subject.removeObserver(observer1)

        subject.setState(3)
        assertEquals(2, observer1.getState())
        assertEquals(3, observer2.getState())
    }
}
```

En esta prueba, primero creamos un ConcreteSubject y dos ConcreteObservers. Luego agregamos los observadores al sujeto y cambiamos el estado del sujeto. Afirmamos que los estados de los observadores han cambiado en consecuencia. Finalmente, eliminamos uno de los observadores y volvemos a cambiar el estado del sujeto. Afirmamos que solo ha cambiado el estado del observador restante.

## Información adicional

- El patrón de observador también se conoce como patrón de publicación-suscripción o pub-sub.
- El patrón de observador se usa a menudo en aplicaciones GUI para manejar eventos como clics en botones
- El Patrón de observador se utiliza en el patrón arquitectónico Modelo-Vista-Controlador (MVC)
- El patrón Observer se utiliza en el patrón arquitectónico Model-View-ViewModel (MVVM)

## Advertencias

- No utilice el patrón de observador cuando el número de dependencias es muy pequeño. En este caso, probablemente sea más fácil llamar directamente a los métodos del objeto dependiente.
- No utilice el patrón de observador cuando el orden en que se envían las notificaciones es importante. En este caso, debe utilizar el patrón de mediador

## Peligros

- El patrón del observador puede conducir a gráficos de objetos muy complejos con una gran cantidad de dependencias. Esto puede ser difícil de mantener y depurar
- El patrón de observador puede provocar pérdidas de memoria si los observadores no se anulan correctamente cuando ya no se necesitan.