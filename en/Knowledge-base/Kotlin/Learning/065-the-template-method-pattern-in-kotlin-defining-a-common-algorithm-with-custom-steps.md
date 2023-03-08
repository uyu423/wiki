---
title: 065: The Template Method Pattern in Kotlin: Defining a Common Algorithm with Custom Steps
description: 
published: true
date: 2023-02-17T01:32:41.881Z
tags: 
editor: markdown
dateCreated: 2023-02-17T01:32:33.658Z
---

- [065: El patrón del método de plantilla en Kotlin: definición de un algoritmo común con pasos personalizados***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/065-the-template-method-pattern-in-kotlin-defining-a-common-algorithm-with-custom-steps)
{.links-list}
- [065：Kotlin 中的模板方法模式：使用自定义步骤定义通用算法***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/065-the-template-method-pattern-in-kotlin-defining-a-common-algorithm-with-custom-steps)
{.links-list}
- [065: Kotlin의 템플릿 메서드 패턴: 사용자 지정 단계로 공통 알고리즘 정의***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/065-the-template-method-pattern-in-kotlin-defining-a-common-algorithm-with-custom-steps)
{.links-list}


# The Template Method Pattern in Kotlin: Defining a Common Algorithm with Custom Steps

In software engineering, the template method pattern is a behavioral design pattern that defines the program skeleton of an algorithm in a base class, but allows its subclasses to provide concrete implementation for some or all of the algorithm.

The template method pattern is a powerful technique for code reuse and for defining an algorithm's structure, but it should be used with care. In particular, template methods should be used only when it is appropriate to define an algorithm in terms of its steps, and when those steps can be reasonably expected to be implemented differently by different subclasses.

## What is the Template Method Pattern?

The template method pattern is a behavioral design pattern that defines the program skeleton of an algorithm in a base class, but allows its subclasses to provide concrete implementation for some or all of the algorithm.

The template method pattern is a powerful technique for code reuse and for defining an algorithm's structure, but it should be used with care. In particular, template methods should be used only when it is appropriate to define an algorithm in terms of its steps, and when those steps can be reasonably expected to be implemented differently by different subclasses.

In the template method pattern, the algorithm's steps are implemented in methods that are either abstract or have a default implementation. These methods are called template methods. The template methods define the overall structure of the algorithm, while the concrete implementation details are provided by the methods that are either abstract or have a default implementation.

The template method pattern is often used in frameworks, where the framework defines the overall structure of an algorithm or application, while the concrete details are provided by the user of the framework.

## When to Use the Template Method Pattern?

The template method pattern should be used when you want to define an algorithm in terms of its steps, and when those steps can be reasonably expected to be implemented differently by different subclasses.

In particular, the template method pattern is useful when:

* You need to define an algorithm that can be decomposed into a series of steps.

* It is expected that different subclasses will implement one or more of the steps in the algorithm differently.

* The order in which the steps are executed is important.

* You want to encapsulate the implementation details of the algorithm in a base class, so that they can be easily changed without affecting the subclasses.

## How to Implement the Template Method Pattern?

The template method pattern can be implemented in Kotlin using either inheritance or delegation.

### Inheritance

When using inheritance, the base class defines the overall structure of the algorithm, while the concrete implementation details are provided by the subclasses.

To implement the template method pattern using inheritance, we need to:

* Define an abstract base class that contains the template method.

* Define concrete subclasses that override the methods in the base class to provide the desired implementation.

For example, consider an application that needs to log messages to a file. We can define a base class that contains the template method for logging messages, and concrete subclasses that override the methods to provide the desired implementation.

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

In the example above, the base class defines the template method ```log()``` that contains the overall structure of the algorithm. The ```log()``` method calls the ```openFile()```, ```writeFile()```, and ```closeFile()``` methods, which are implemented differently by the subclasses.

### Delegation

When using delegation, the base class defines the overall structure of the algorithm, while the concrete implementation details are provided by a delegate object.

To implement the template method pattern using delegation, we need to:

* Define a base class that contains the template method.

* Define a delegate class that contains the methods that will be called by the template method.

* Create an instance of the delegate class in the base class, and pass it to the template method.

For example, consider an application that needs to log messages to a file. We can define a base class that contains the template method for logging messages, and a delegate class that contains the methods to be called by the template method.

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

In the example above, the base class defines the template method ```log()``` that contains the overall structure of the algorithm. The ```log()``` method calls the ```openFile()```, ```writeFile()```, and ```closeFile()``` methods of the delegate object. The concrete implementation details are provided by the delegate classes.

## Advantages of the Template Method Pattern

The template method pattern has the following advantages:

* It encapsulates the implementation details of an algorithm in a base class, so that they can be easily changed without affecting the subclasses.

* It allows you to define the overall structure of an algorithm in a base class, while allowing subclasses to provide concrete implementation for some or all of the steps.

* It promotes code reuse by allowing you to define common code in a base class that can be reused by all subclasses.

* It is easy to extend by allowing you to add new steps to the algorithm without affecting the existing code.

## Disadvantages of the Template Method Pattern

The template method pattern has the following disadvantages:

* It can lead to code duplication if the same algorithm is needed in multiple places with only minor variations. In such cases, it is usually better to extract the common code into a separate function or method.

* It can make the code harder to understand and maintain if the algorithm is too complex. In such cases, it is usually better to refactor the code to make it more readable and maintainable.

## Conclusion

The template method pattern is a powerful technique for code reuse and for defining an algorithm's structure, but it should be used with care. In particular, template methods should be used only when it is appropriate to define an algorithm in terms of its steps, and when those steps can be reasonably expected to be implemented differently by different subclasses.