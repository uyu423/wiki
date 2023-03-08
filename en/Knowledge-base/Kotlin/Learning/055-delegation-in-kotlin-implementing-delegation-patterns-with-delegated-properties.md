---
title: 055: Delegation in Kotlin: Implementing Delegation Patterns with Delegated Properties
description: 
published: true
date: 2023-02-16T19:32:34.087Z
tags: 
editor: markdown
dateCreated: 2023-02-16T19:32:26.218Z
---

- [055: Delegación en Kotlin: Implementación de patrones de delegación con propiedades delegadas***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/055-delegation-in-kotlin-implementing-delegation-patterns-with-delegated-properties)
{.links-list}
- [055：Kotlin 中的委托：使用委托属性实现委托模式***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/055-delegation-in-kotlin-implementing-delegation-patterns-with-delegated-properties)
{.links-list}
- [055: Kotlin의 위임: 위임된 속성으로 위임 패턴 구현***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/055-delegation-in-kotlin-implementing-delegation-patterns-with-delegated-properties)
{.links-list}


# Delegation in Kotlin: Implementing Delegation Patterns with Delegated Properties

Kotlin provides powerful delegation mechanisms that can be used to implement various delegation patterns. In this post, we'll take a look at how to use delegated properties to implement the delegation pattern in Kotlin.

Delegation is a software design pattern that allows an object to delegate responsibility for certain tasks to another object. Delegation can be used to improve code modularity and reusability.

There are many different delegation patterns, but the most common one is the delegation pattern. In the delegation pattern, an object (the "delegate") is responsible for handling a request from another object (the "requestor").

The delegation pattern is often used in object-oriented programming to improve code modularity. For example, if you have a class that needs to perform a complex task, you can delegate that task to another class. This allows you to reuse the code in the delegate class in other classes.

Delegation can also be used to improve code reusability. For example, if you have a class that needs to perform a task that is not specific to that class, you can delegate that task to another class. This allows you to reuse the code in the delegate class in other classes.

Delegation is a powerful tool, but it can be misused. For example, if you delegate a task to a class that is not well-suited for that task, the code in the delegate class can become convoluted and difficult to maintain.

When used correctly, delegation can be a very powerful tool for improving code modularity and reusability. In this post, we'll take a look at how to use delegated properties to implement the delegation pattern in Kotlin.

Delegated properties are a powerful feature of Kotlin that allow you to delegate responsibility for a property to another object. Delegated properties are declared using the by keyword. For example, the following code declares a delegated property of type String:

```kotlin
class MyClass {
    val delegatedProperty: String by Delegate()
}
```

In the code above, the delegatedProperty property is delegated to an instance of the Delegate class. The Delegate class must implement the getValue() and setValue() methods. These methods are used to get and set the value of the delegated property, respectively.

The getValue() and setValue() methods take two arguments: the instance of the class that owns the delegated property and the value of the delegated property. For example, the following code shows how the getValue() and setValue() methods can be implemented:

```kotlin
class Delegate {
    fun getValue(thisRef: Any, property: KProperty<*>): String {
        // return the value of the delegated property
    }

    fun setValue(thisRef: Any, property: KProperty<*>, value: String) {
        // set the value of the delegated property
    }
}
```

In the code above, the getValue() and setValue() methods are implemented in the Delegate class. These methods take two arguments: the instance of the class that owns the delegated property and the value of the delegated property.

The getValue() method is used to get the value of the delegated property. The setValue() method is used to set the value of the delegated property.

Delegated properties are a powerful feature of Kotlin that can be used to implement the delegation pattern. In the next section, we'll take a look at how to use delegated properties to implement a simple delegation pattern.