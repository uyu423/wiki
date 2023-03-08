---
title: 077: El patrón Memento en Kotlin: Preservar los estados de los objetos para futuras restauraciones
description: 
published: true
date: 2023-02-16T22:55:28.545Z
tags: 
editor: markdown
dateCreated: 2023-02-16T22:55:26.917Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [077: The Memento Pattern in Kotlin: Preserving Object States for Future Restoration***English** document is available*](/en/Knowledge-base/Kotlin/Learning/077-the-memento-pattern-in-kotlin-preserving-object-states-for-future-restoration)
{.links-list}


# El patrón Memento en Kotlin: Preservar los estados de los objetos para futuras restauraciones

El patrón memento es un patrón de diseño de software que brinda la capacidad de guardar y restaurar el estado de un objeto. A menudo se usa junto con las operaciones de deshacer/rehacer.

El patrón de recuerdo es una estructura de tres niveles que consiste en el originador, el cuidador y el recuerdo.

El originador es el objeto cuyo estado debe guardarse. El cuidador es el objeto responsable de salvar y restaurar el estado del originador. El memento es un objeto inmutable que almacena el estado del creador.

El patrón memento se utiliza para:

- Guardar y restaurar el estado de un objeto
- Guardar y restaurar el estado de los atributos de un objeto
- Guardar y restaurar el estado de las asociaciones de un objeto

## Implementando el Patrón Memento en Kotlin

Hay dos formas de implementar el patrón memento en Kotlin:

- Usando una clase de datos
- Usando una clase sellada

### Uso de una clase de datos

Una clase de datos es una clase que está diseñada para contener datos. Las clases de datos tienen una serie de características que las hacen ideales para implementar el patrón memento:

- Las clases de datos son inmutables.
- Las clases de datos tienen un método `copia`
- Las clases de datos se pueden declarar usando la palabra clave `data`

Para implementar el patrón memento usando una clase de datos, necesitamos crear una clase `Memento` que almacene el estado de la clase `Original`. La clase `Originator` tiene un método `createMemento` que crea un objeto `Memento` y un método `restoreMemento` que restaura el estado del `Originator` a partir de un objeto `Memento`.

Aquí hay un ejemplo de cómo implementar el patrón memento usando una clase de datos:

```kotlin
data class Originator(var state: String) {
  
  fun createMemento(): Memento {
    return Memento(state)
  }
  
  fun restoreMemento(memento: Memento) {
    state = memento.state
  }
  
  data class Memento(val state: String)
}
```

### Uso de una clase sellada

Una clase sellada es una clase que puede tener una o más subclases. Las clases selladas son ideales para implementar el patrón memento porque:

- Se puede declarar usando la palabra clave `sellado`
- Puede tener subclases
- Puede ser declarado `abstracto`

Para implementar el patrón memento usando una clase sellada, necesitamos crear una clase sellada `Memento` que tenga una subclase para cada estado del `Original`. La clase `Originator` tiene un método `createMemento` que crea un objeto `Memento` y un método `restoreMemento` que restaura el estado del `Originator` a partir de un objeto `Memento`.

Aquí hay un ejemplo de cómo implementar el patrón memento usando una clase sellada:

```kotlin
sealed class Memento

class Originator(var state: String) {
  
  fun createMemento(): Memento {
    return when (state) {
      "state1" -> State1()
      "state2" -> State2()
      else -> throw IllegalArgumentException("Invalid state")
    }
  }
  
  fun restoreMemento(memento: Memento) {
    state = when (memento) {
      is State1 -> "state1"
      is State2 -> "state2"
      else -> throw IllegalArgumentException("Invalid memento")
    }
  }
  
  class State1 : Memento
  class State2 : Memento
}
```

## Conclusión

En este artículo, hemos aprendido sobre el patrón memento y cómo implementarlo en Kotlin usando clases de datos y clases selladas.