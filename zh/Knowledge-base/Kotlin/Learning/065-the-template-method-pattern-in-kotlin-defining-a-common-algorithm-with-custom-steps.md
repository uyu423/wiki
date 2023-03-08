---
title: 065：Kotlin 中的模板方法模式：使用自定义步骤定义通用算法
description: 
published: true
date: 2023-02-17T01:32:35.269Z
tags: 
editor: markdown
dateCreated: 2023-02-17T01:32:33.653Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [065: The Template Method Pattern in Kotlin: Defining a Common Algorithm with Custom Steps***English** document is available*](/en/Knowledge-base/Kotlin/Learning/065-the-template-method-pattern-in-kotlin-defining-a-common-algorithm-with-custom-steps)
{.links-list}


# Kotlin 中的模板方法模式：使用自定义步骤定义通用算法

在软件工程中，模板方法模式是一种行为设计模式，它在基类中定义算法的程序骨架，但允许其子类为部分或全部算法提供具体实现。

模板方法模式是一种用于代码重用和定义算法结构的强大技术，但应谨慎使用。特别是，仅当根据算法的步骤来定义算法是合适的，并且可以合理地预期这些步骤将由不同的子类以不同方式实现时，才应使用模板方法。

## 什么是模板方法模式？

模板方法模式是一种行为设计模式，它在基类中定义算法的程序骨架，但允许其子类为部分或全部算法提供具体实现。

模板方法模式是一种用于代码重用和定义算法结构的强大技术，但应谨慎使用。特别是，仅当根据算法的步骤来定义算法是合适的，并且可以合理地预期这些步骤将由不同的子类以不同方式实现时，才应使用模板方法。

在模板方法模式中，算法的步骤在抽象或具有默认实现的方法中实现。这些方法称为模板方法。模板方法定义了算法的整体结构，而具体的实现细节由抽象或具有默认实现的方法提供。

模板方法模式常用于框架中，框架定义算法或应用程序的整体结构，而具体细节由框架的使用者提供。

## 何时使用模板方法模式？

当你想根据算法的步骤定义一个算法时，以及当这些步骤可以合理地预期由不同的子类以不同的方式实现时，应该使用模板方法模式。

特别是，模板方法模式在以下情况下很有用：

* 你需要定义一个可以分解为一系列步骤的算法。

* 预计不同的子类将以不同方式实现算法中的一个或多个步骤。

* 执行步骤的顺序很重要。

* 你想把算法的实现细节封装在一个基类中，这样它们可以很容易地改变而不影响子类。

## 如何实现模板方法模式？

可以使用继承或委托在 Kotlin 中实现模板方法模式。

### 继承

使用继承时，基类定义了算法的总体结构，而具体的实现细节则由子类提供。

要使用继承来实现模板方法模式，我们需要：

* 定义一个包含模板方法的抽象基类。

* 定义覆盖基类中方法的具体子类以提供所需的实现。

例如，考虑一个需要将消息记录到文件的应用程序。我们可以定义一个基类，其中包含用于记录消息的模板方法，以及覆盖这些方法以提供所需实现的具体子类。

```kotlin
abstract class Logger {
    fun log(message: String) {
        openFile()
        writeFile(message)
        closeFile()
    }

    abstract fun openFile()
    abstract fun writeFile(message: String)
    abstract fun closeFile()
}

class FileLogger: Logger() {
    override fun openFile() {
        // ...
    }

    override fun writeFile(message: String) {
        // ...
    }

    override fun closeFile() {
        // ...
    }
}

class ConsoleLogger: Logger() {
    override fun openFile() {
        // ...
    }

    override fun writeFile(message: String) {
        // ...
    }

    override fun closeFile() {
        // ...
    }
}
```

在上面的例子中，基类定义了包含算法整体结构的模板方法```log()```。 ```log()``` 方法调用```openFile()```、```writeFile()``` 和```closeFile()``` 方法，它们的实现方式不同子类。

### 代表团

使用委托时，基类定义了算法的整体结构，而具体的实现细节则由委托对象提供。

要使用委托来实现模板方法模式，我们需要：

* 定义一个包含模板方法的基类。

* 定义一个委托类，其中包含将由模板方法调用的方法。

* 在基类中创建委托类的实例，并将其传递给模板方法。

例如，考虑一个需要将消息记录到文件的应用程序。我们可以定义一个基类，其中包含用于记录消息的模板方法，以及一个委托类，其中包含要由模板方法调用的方法。

```kotlin
class Logger(val delegate: LoggerDelegate) {
    fun log(message: String) {
        delegate.openFile()
        delegate.writeFile(message)
        delegate.closeFile()
    }
}

class FileLoggerDelegate: LoggerDelegate {
    override fun openFile() {
        // ...
    }

    override fun writeFile(message: String) {
        // ...
    }

    override fun closeFile() {
        // ...
    }
}

class ConsoleLoggerDelegate: LoggerDelegate {
    override fun openFile() {
        // ...
    }

    override fun writeFile(message: String) {
        // ...
    }

    override fun closeFile() {
        // ...
    }
}
```

在上面的例子中，基类定义了包含算法整体结构的模板方法```log()```。 ```log()``` 方法调用委托对象的```openFile()```、```writeFile()``` 和```closeFile()``` 方法。具体的实现细节由委托类提供。

## 模板方法模式的优点

模板方法模式有以下优点：

* 它将算法的实现细节封装在一个基类中，这样它们可以很容易地改变而不影响子类。

* 它允许您在基类中定义算法的总体结构，同时允许子类为部分或全部步骤提供具体实现。

* 它通过允许您在基类中定义可被所有子类重用的公共代码来促进代码重用。

* 允许您在不影响现有代码的情况下向算法添加新步骤，从而易于扩展。

## 模板方法模式的缺点

模板方法模式有以下缺点：

* 如果在多个地方需要相同的算法并且只有很小的变化，它可能会导致代码重复。在这种情况下，通常最好将公共代码提取到单独的函数或方法中。

* 如果算法过于复杂，会使代码更难理解和维护。在这种情况下，通常最好重构代码以使其更具可读性和可维护性。

## 结论

模板方法模式是一种用于代码重用和定义算法结构的强大技术，但应谨慎使用。特别是，仅当根据算法的步骤来定义算法是合适的，并且可以合理地预期这些步骤将由不同的子类以不同方式实现时，才应使用模板方法。