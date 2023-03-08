---
title: 069: The Command Pattern in Kotlin: Encapsulating Invocations as Objects
description: 
published: true
date: 2023-02-17T03:32:49.105Z
tags: 
editor: markdown
dateCreated: 2023-02-17T03:32:40.650Z
---

- [069: El patrón de comando en Kotlin: encapsular invocaciones como objetos***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/069-the-command-pattern-in-kotlin-encapsulating-invocations-as-objects)
{.links-list}
- [069：Kotlin 中的命令模式：将调用封装为对象***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/069-the-command-pattern-in-kotlin-encapsulating-invocations-as-objects)
{.links-list}
- [069: Kotlin의 명령 패턴: 호출을 객체로 캡슐화***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/069-the-command-pattern-in-kotlin-encapsulating-invocations-as-objects)
{.links-list}


# The Command Pattern in Kotlin: Encapsulating Invocations as Objects

The command pattern is a behavioral design pattern in which an object is used to encapsulate all information needed to perform an action or trigger an event at a later time. This information includes the method name, the object that owns the method and values for the method parameters.

The command pattern is used to implement undoable operations, handle menu items in a graphical user interface (GUI) or implement network protocols. It is also a good choice for implementing macros or other high-level actions that should be able to be undone/redone.

## How Does the Command Pattern Work?

The command pattern encapsulates a request as an object, thereby letting you parameterize other objects with different requests, queue or log requests, and support undoable operations.

The command pattern is based on the principle of **inversion of control**. In traditional programming, the flow of control is determined by the structure of the code. In the command pattern, the flow of control is inverted: the object that invokes the method is not the same object that owns the method.

The command pattern has four main components:

- The **invoker** is the object that invokes the command. It contains a reference to the command object.
- The **command** interface is implemented by all command objects. It declares a method for executing the command.
- The **concrete command** class implements the command interface. It contains a reference to the receiver object and defines the action that is executed when the execute method is invoked.
- The **receiver** is the object that owns the method that is invoked by the command.

## When to Use the Command Pattern

The command pattern should be used when you want to **parameterize objects with different requests**, **queue or log requests**, and **support undoable operations**.

## Pros and Cons

The main advantages of the command pattern are:

- It decouples the invoker from the receiver.
- It supports undoable operations.

The main disadvantages of the command pattern are:

- It increases the complexity of the code.
- It can introduce memory leaks if the invoker does not hold a reference to the command object.

## Implementation

Let's see how the command pattern can be implemented in Kotlin.

### The Invoker

The invoker is the object that invokes the command. It contains a reference to the command object.

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

### The Command Interface

The command interface is implemented by all command objects. It declares a method for executing the command.

```kotlin
interface Command {
    fun execute()
}
```

### The Concrete Command

The concrete command class implements the command interface. It contains a reference to the receiver object and defines the action that is executed when the execute method is invoked.

```kotlin
class ConcreteCommand(private val receiver: Receiver) : Command {
    override fun execute() {
        receiver.action()
    }
}
```

### The Receiver

The receiver is the object that owns the method that is invoked by the command.

```kotlin
class Receiver {
    fun action() {
        // ...
    }
}
```

## Usage

The command pattern can be used to implement undoable operations, handle menu items in a GUI or implement network protocols.

### Undoable Operations

The command pattern is a good choice for implementing undoable operations. The undo method can be implemented by keeping a history of all the commands that have been executed.

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

### GUI

The command pattern can be used to handle menu items in a GUI. In this example, the invoker is a menu and the receiver is a text editor.

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

### Network Protocol

The command pattern can be used to implement network protocols. In this example, the invoker is a client and the receiver is a server.

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

## Conclusion

In this blog post, we've learned about the command pattern and how it can be used to encapsulate requests as objects. We've also seen how the command pattern can be used to implement undoable operations, handle menu items in a GUI or implement network protocols.