---
title: 069: Kotlin의 명령 패턴: 호출을 객체로 캡슐화
description: 
published: true
date: 2023-02-17T03:32:42.955Z
tags: 
editor: markdown
dateCreated: 2023-02-17T03:32:40.635Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [069: The Command Pattern in Kotlin: Encapsulating Invocations as Objects***English** document is available*](/en/Knowledge-base/Kotlin/Learning/069-the-command-pattern-in-kotlin-encapsulating-invocations-as-objects)
{.links-list}


# Kotlin의 명령 패턴: 호출을 객체로 캡슐화

명령 패턴은 개체가 나중에 작업을 수행하거나 이벤트를 트리거하는 데 필요한 모든 정보를 캡슐화하는 데 사용되는 동작 디자인 패턴입니다. 이 정보에는 메서드 이름, 메서드를 소유하는 개체 및 메서드 매개 변수 값이 포함됩니다.

명령 패턴은 실행 취소 가능한 작업을 구현하거나 GUI(그래픽 사용자 인터페이스)에서 메뉴 항목을 처리하거나 네트워크 프로토콜을 구현하는 데 사용됩니다. 또한 실행 취소/재실행이 가능해야 하는 매크로 또는 기타 고급 작업을 구현하는 데 적합합니다.

## 명령 패턴은 어떻게 작동합니까?

명령 패턴은 요청을 객체로 캡슐화하므로 다른 요청, 큐 또는 로그 요청으로 다른 객체를 매개 변수화하고 실행 취소 가능한 작업을 지원할 수 있습니다.

명령 패턴은 **제어 역전** 원칙을 기반으로 합니다. 전통적인 프로그래밍에서 제어 흐름은 코드 구조에 의해 결정됩니다. 명령 패턴에서는 제어 흐름이 반전됩니다. 메서드를 호출하는 개체는 메서드를 소유하는 개체와 다릅니다.

명령 패턴에는 네 가지 주요 구성 요소가 있습니다.

- **invoker**는 명령을 호출하는 개체입니다. 여기에는 명령 개체에 대한 참조가 포함됩니다.
- **명령** 인터페이스는 모든 명령 개체에 의해 구현됩니다. 명령을 실행하는 방법을 선언합니다.
- **구체적인 명령** 클래스는 명령 인터페이스를 구현합니다. 여기에는 수신자 개체에 대한 참조가 포함되어 있으며 execute 메서드가 호출될 때 실행되는 작업을 정의합니다.
- **수신자**는 명령에 의해 호출되는 메서드를 소유하는 개체입니다.

## 명령 패턴을 사용하는 경우

명령 패턴은 **요청이 다른 개체를 매개 변수화**하고 **요청을 대기열에 넣거나 기록**하고 **실행 취소 가능한 작업을 지원**하려는 경우에 사용해야 합니다.

## 장점과 단점

명령 패턴의 주요 이점은 다음과 같습니다.

- 수신기에서 호출자를 분리합니다.
- 취소 가능한 작업을 지원합니다.

명령 패턴의 주요 단점은 다음과 같습니다.

- 코드의 복잡성을 증가시킵니다.
- 호출자가 명령 개체에 대한 참조를 보유하지 않는 경우 메모리 누수가 발생할 수 있습니다.

## 구현

Kotlin에서 명령 패턴을 구현하는 방법을 살펴보겠습니다.

### 호출자

호출자는 명령을 호출하는 개체입니다. 여기에는 명령 개체에 대한 참조가 포함됩니다.

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

### 명령 인터페이스

명령 인터페이스는 모든 명령 개체에 의해 구현됩니다. 명령을 실행하는 방법을 선언합니다.

```kotlin
interface Command {
    fun execute()
}
```

### 구체적인 명령

구체적인 명령 클래스는 명령 인터페이스를 구현합니다. 여기에는 수신자 개체에 대한 참조가 포함되어 있으며 execute 메서드가 호출될 때 실행되는 작업을 정의합니다.

```kotlin
class ConcreteCommand(private val receiver: Receiver) : Command {
    override fun execute() {
        receiver.action()
    }
}
```

### 수신자

수신자는 명령에 의해 호출되는 메서드를 소유하는 개체입니다.

```kotlin
class Receiver {
    fun action() {
        // ...
    }
}
```

## 용법

명령 패턴은 실행 취소 가능한 작업을 구현하거나 GUI에서 메뉴 항목을 처리하거나 네트워크 프로토콜을 구현하는 데 사용할 수 있습니다.

### 실행 취소 가능한 작업

명령 패턴은 실행 취소 가능한 작업을 구현하는 데 적합합니다. 실행 취소 방법은 실행된 모든 명령의 기록을 유지하여 구현할 수 있습니다.

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

명령 패턴은 GUI에서 메뉴 항목을 처리하는 데 사용할 수 있습니다. 이 예제에서 호출자는 메뉴이고 수신자는 텍스트 편집기입니다.

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

### 네트워크 프로토콜

명령 패턴은 네트워크 프로토콜을 구현하는 데 사용할 수 있습니다. 이 예에서 호출자는 클라이언트이고 수신자는 서버입니다.

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

## 결론

이 블로그 게시물에서는 명령 패턴과 이를 사용하여 요청을 객체로 캡슐화하는 방법에 대해 배웠습니다. 또한 실행 취소 가능한 작업을 구현하고 GUI에서 메뉴 항목을 처리하거나 네트워크 프로토콜을 구현하는 데 명령 패턴을 사용하는 방법도 살펴보았습니다.