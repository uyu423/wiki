---
title: 069: El patrón de comando en Kotlin: encapsular invocaciones como objetos
description: 
published: true
date: 2023-02-17T03:32:42.973Z
tags: 
editor: markdown
dateCreated: 2023-02-17T03:32:40.649Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [069: The Command Pattern in Kotlin: Encapsulating Invocations as Objects***English** document is available*](/en/Knowledge-base/Kotlin/Learning/069-the-command-pattern-in-kotlin-encapsulating-invocations-as-objects)
{.links-list}


# El patrón de comando en Kotlin: encapsulando invocaciones como objetos

El patrón de comando es un patrón de diseño de comportamiento en el que se utiliza un objeto para encapsular toda la información necesaria para realizar una acción o desencadenar un evento en un momento posterior. Esta información incluye el nombre del método, el objeto que posee el método y los valores de los parámetros del método.

El patrón de comando se utiliza para implementar operaciones que se pueden deshacer, manejar elementos de menú en una interfaz gráfica de usuario (GUI) o implementar protocolos de red. También es una buena opción para implementar macros u otras acciones de alto nivel que deberían poder deshacerse/rehacerse.

## ¿Cómo funciona el patrón de comando?

El patrón de comando encapsula una solicitud como un objeto, lo que le permite parametrizar otros objetos con diferentes solicitudes, solicitudes de cola o registro y admite operaciones que se pueden deshacer.

El patrón de comando se basa en el principio de **inversión de control**. En la programación tradicional, el flujo de control está determinado por la estructura del código. En el patrón de comando, el flujo de control se invierte: el objeto que invoca el método no es el mismo objeto que posee el método.

El patrón de comando tiene cuatro componentes principales:

- El **invocador** es el objeto que invoca el comando. Contiene una referencia al objeto de comando.
- Todos los objetos de comando implementan la interfaz de **comando**. Declara un método para ejecutar el comando.
- La clase **comando concreto** implementa la interfaz de comando. Contiene una referencia al objeto receptor y define la acción que se ejecuta cuando se invoca el método de ejecución.
- El **receptor** es el objeto que posee el método que es invocado por el comando.

## Cuándo usar el patrón de comando

El patrón de comando se debe usar cuando desee **parametrizar objetos con diferentes solicitudes**, **solicitar en cola o registrar** y **apoyar operaciones que se pueden deshacer**.

## Pros y contras

Las principales ventajas del patrón de comando son:

- Desvincula al invocador del receptor.
- Soporta operaciones deshacer.

Las principales desventajas del patrón de comando son:

- Aumenta la complejidad del código.
- Puede introducir pérdidas de memoria si el invocador no tiene una referencia al objeto de comando.

## Implementación

Veamos cómo se puede implementar el patrón de comando en Kotlin.

### El invocador

El invocador es el objeto que invoca el comando. Contiene una referencia al objeto de comando.

```kotlin
class Invoker {
    private val command: Command

    constructor(command: Command) {
        this.command = command
    }

    fun execute() {
        command.execute()
    }
}
```

### La interfaz de comandos

La interfaz de comando es implementada por todos los objetos de comando. Declara un método para ejecutar el comando.

```kotlin
interface Command {
    fun execute()
}
```

### El comando concreto

La clase de comando concreta implementa la interfaz de comando. Contiene una referencia al objeto receptor y define la acción que se ejecuta cuando se invoca el método de ejecución.

```kotlin
class ConcreteCommand(private val receiver: Receiver) : Command {
    override fun execute() {
        receiver.action()
    }
}
```

### El receptor

El receptor es el objeto que posee el método invocado por el comando.

```kotlin
class Receiver {
    fun action() {
        // ...
    }
}
```

## Uso

El patrón de comando se puede usar para implementar operaciones que se pueden deshacer, manejar elementos de menú en una GUI o implementar protocolos de red.

### Operaciones que se pueden deshacer

El patrón de comando es una buena opción para implementar operaciones que se pueden deshacer. El método de deshacer se puede implementar manteniendo un historial de todos los comandos que se han ejecutado.

```kotlin
class Invoker {
    private val commands: Stack<Command> = Stack()

    fun execute(command: Command) {
        command.execute()
        commands.push(command)
    }

    fun undo() {
        if (!commands.isEmpty()) {
            val command = commands.pop()
            command.undo()
        }
    }
}

class ConcreteCommand(private val receiver: Receiver) : Command {
    override fun execute() {
        receiver.action()
    }

    override fun undo() {
        receiver.undoAction()
    }
}

class Receiver {
    fun action() {
        // ...
    }

    fun undoAction() {
        // ...
    }
}
```

### interfaz gráfica de usuario

El patrón de comando se puede usar para manejar elementos de menú en una GUI. En este ejemplo, el invocador es un menú y el receptor es un editor de texto.

```kotlin
class Menu(private val textEditor: TextEditor) {
    private val commands: Stack<Command> = Stack()

    fun clickUndo() {
        if (!commands.isEmpty()) {
            val command = commands.pop()
            command.undo()
        }
    }

    fun clickOpen() {
        val command = OpenCommand(textEditor)
        command.execute()
        commands.push(command)
    }

    fun clickSave() {
        val command = SaveCommand(textEditor)
        command.execute()
        commands.push(command)
    }
}

class OpenCommand(private val textEditor: TextEditor) : Command {
    override fun execute() {
        textEditor.open()
    }

    override fun undo() {
        textEditor.close()
    }
}

class SaveCommand(private val textEditor: TextEditor) : Command {
    override fun execute() {
        textEditor.save()
    }

    override fun undo() {
        // ...
    }
}

class TextEditor {
    fun open() {
        // ...
    }

    fun save() {
        // ...
    }

    fun close() {
        // ...
    }
}
```

### Protocolo de red

El patrón de comando se puede utilizar para implementar protocolos de red. En este ejemplo, el invocador es un cliente y el receptor es un servidor.

```kotlin
class Client {
    private val commands: Stack<Command> = Stack()

    fun send(command: Command) {
        command.execute()
        commands.push(command)
    }

    fun undo() {
        if (!commands.isEmpty()) {
            val command = commands.pop()
            command.undo()
        }
    }
}

class Server {
    fun action() {
        // ...
    }

    fun undoAction() {
        // ...
    }
}

class ConcreteCommand(private val receiver: Receiver) : Command {
    override fun execute() {
        receiver.action()
    }

    override fun undo() {
        receiver.undoAction()
    }
}
```

## Conclusión

En esta publicación de blog, aprendimos sobre el patrón de comando y cómo se puede usar para encapsular solicitudes como objetos. También hemos visto cómo se puede usar el patrón de comando para implementar operaciones que se pueden deshacer, manejar elementos de menú en una GUI o implementar protocolos de red.