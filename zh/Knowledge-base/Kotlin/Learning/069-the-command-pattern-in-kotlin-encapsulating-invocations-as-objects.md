---
title: 069：Kotlin 中的命令模式：将调用封装为对象
description: 
published: true
date: 2023-02-17T03:32:42.475Z
tags: 
editor: markdown
dateCreated: 2023-02-17T03:32:40.635Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [069: The Command Pattern in Kotlin: Encapsulating Invocations as Objects***English** document is available*](/en/Knowledge-base/Kotlin/Learning/069-the-command-pattern-in-kotlin-encapsulating-invocations-as-objects)
{.links-list}


# Kotlin 中的命令模式：将调用封装为对象

命令模式是一种行为设计模式，其中使用对象来封装执行某个动作或稍后触发事件所需的所有信息。此信息包括方法名称、拥有该方法的对象和方法参数的值。

命令模式用于实现不可撤销的操作、处理图形用户界面 (GUI) 中的菜单项或实现网络协议。它也是实现宏或其他应该能够撤消/重做的高级操作的不错选择。

## 命令模式如何工作？

命令模式将一个请求封装为一个对象，从而让您用不同的请求、队列或日志请求参数化其他对象，并支持可撤销操作。

命令模式基于**反转控制**的原则。在传统的编程中，控制流是由代码的结构决定的。在命令模式中，控制流是相反的：调用该方法的对象与拥有该方法的对象不同。

命令模式有四个主要组成部分：

- **invoker** 是调用命令的对象。它包含对命令对象的引用。
- **command** 接口由所有命令对象实现。它声明了执行命令的方法。
- **具体命令**类实现了命令接口。它包含对接收者对象的引用，并定义调用执行方法时执行的操作。
- **receiver** 是拥有命令调用的方法的对象。

## 何时使用命令模式

当你想要**参数化具有不同请求的对象**、**队列或日志请求**以及**支持可撤销操作**时，应该使用命令模式。

## 优点和缺点

命令模式的主要优点是：

- 它将调用者与接收者分离。
- 它支持可撤销的操作。

命令模式的主要缺点是：

- 它增加了代码的复杂性。
- 如果调用程序不持有对命令对象的引用，它可能会引入内存泄漏。

## 执行

让我们看看如何在 Kotlin 中实现命令模式。

### 调用者

调用者是调用命令的对象。它包含对命令对象的引用。

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

### 命令界面

命令接口由所有命令对象实现。它声明了执行命令的方法。

```kotlin
interface Command {
    fun execute()
}
```

### 具体命令

具体命令类实现命令接口。它包含对接收者对象的引用，并定义调用执行方法时执行的操作。

```kotlin
class ConcreteCommand(private val receiver: Receiver) : Command {
    override fun execute() {
        receiver.action()
    }
}
```

### 收件人

接收者是拥有命令调用的方法的对象。

```kotlin
class Receiver {
    fun action() {
        // ...
    }
}
```

## 用法

命令模式可用于实现不可撤销的操作、处理 GUI 中的菜单项或实现网络协议。

### 不可撤销的操作

命令模式是实现可撤销操作的不错选择。 undo 方法可以通过保留所有已执行命令的历史记录来实现。

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

### 界面

命令模式可用于处理 GUI 中的菜单项。在这个例子中，调用者是一个菜单，接收者是一个文本编辑器。

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

### 网络协议

命令模式可用于实现网络协议。在此示例中，调用者是客户端，接收者是服务器。

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

## 结论

在这篇博文中，我们了解了命令模式以及如何使用它来将请求封装为对象。我们还看到了如何使用命令模式来实现不可撤销的操作、处理 GUI 中的菜单项或实现网络协议。