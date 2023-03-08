---
title: 020: Delegated Properties in Kotlin: Implementing Delegation Patterns
description: 
published: true
date: 2023-02-16T06:33:32.368Z
tags: 
editor: markdown
dateCreated: 2023-02-16T06:33:28.389Z
---

- [020: Propiedades delegadas en Kotlin: Implementando patrones de delegación***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/020-delegated-properties-in-kotlin-implementing-delegation-patterns)
{.links-list}
- [020：Kotlin 中的委托属性：实施委托模式***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/020-delegated-properties-in-kotlin-implementing-delegation-patterns)
{.links-list}
- [020: Kotlin의 위임 속성: 위임 패턴 구현***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/020-delegated-properties-in-kotlin-implementing-delegation-patterns)
{.links-list}


# Delegated Properties in Kotlin: Implementing Delegation Patterns

Kotlin's delegation model is built on the idea of delegation by delegation. In this pattern, one object (the delegate) is responsible for handling a request from another object (the delegator). The delegator can delegate all or part of its responsibilities to the delegate.

In Kotlin, delegation is a first-class language feature. You can use delegation to implement common design patterns, such as the Observer pattern, the Decorator pattern, and the Factory pattern. Delegation can also be used to improve the performance of your code.

In this post, we'll take a closer look at delegated properties in Kotlin. We'll learn how to create and use delegated properties, and we'll explore some of the benefits of using delegation.

## What are Delegated Properties?

A delegated property is a property whose value is computed by a delegate. A delegate is an object that knows how to compute the value of a property. In Kotlin, you can create a delegated property by using the `by` keyword.

For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by lazy {
        // compute the name
    }
}
```

In this example, the `name` property is a delegated property. The delegate is an instance of the `Lazy` class. The `Lazy` class knows how to compute the value of the `name` property.

When you access the `name` property, the `Lazy` instance will compute the value of the property and return it. The value will be cached, so that subsequent accesses to the property will be fast.

##Creating Delegated Properties

As we saw in the previous section, you can create a delegated property by using the `by` keyword. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by lazy {
        // compute the name
    }
}
```

In this example, the `name` property is a delegated property. The delegate is an instance of the `Lazy` class. The `Lazy` class knows how to compute the value of the `name` property.

When you access the `name` property, the `Lazy` instance will compute the value of the property and return it. The value will be cached, so that subsequent accesses to the property will be fast.

You can also create a delegated property by using a property delegate. A property delegate is an object that knows how to compute the value of a property. In Kotlin, you can create a property delegate by using the `by` keyword.

For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using a property delegate:

```kotlin
class User {
    val name: String by NameDelegate()
}
```

In this example, the `name` property is a delegated property. The delegate is an instance of the `NameDelegate` class. The `NameDelegate` class knows how to compute the value of the `name` property.

When you access the `name` property, the `NameDelegate` instance will compute the value of the property and return it. The value will be cached, so that subsequent accesses to the property will be fast.

## Implementing a Delegate

In Kotlin, you can create a delegate by using the `by` keyword. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by lazy {
        // compute the name
    }
}
```

In this example, the `name` property is a delegated property. The delegate is an instance of the `Lazy` class. The `Lazy` class knows how to compute the value of the `name` property.

When you access the `name` property, the `Lazy` instance will compute the value of the property and return it. The value will be cached, so that subsequent accesses to the property will be fast.

You can also create a delegate by using a property delegate. A property delegate is an object that knows how to compute the value of a property. In Kotlin, you can create a property delegate by using the `by` keyword.

For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using a property delegate:

```kotlin
class User {
    val name: String by NameDelegate()
}
```

In this example, the `name` property is a delegated property. The delegate is an instance of the `NameDelegate` class. The `NameDelegate` class knows how to compute the value of the `name` property.

When you access the `name` property, the `NameDelegate` instance will compute the value of the property and return it. The value will be cached, so that subsequent accesses to the property will be fast.

## Delegating to a Map

In Kotlin, you can use the `by` keyword to delegate to a map. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by mapOf("id" to 1, "name" to "John")
}
```

In this example, the `name` property is a delegated property. The delegate is a map. When you access the `name` property, the map will be searched for the key `name`. If the key is found, the corresponding value will be returned. If the key is not found, an exception will be thrown.

## Delegating to a Property

In Kotlin, you can use the `by` keyword to delegate to a property. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by lazy {
        firstName + " " + lastName
    }
}
```

In this example, the `name` property is a delegated property. The delegate is a property. When you access the `name` property, the `firstName` and `lastName` properties will be accessed and concatenated. The result will be returned.

## Delegating to a Function

In Kotlin, you can use the `by` keyword to delegate to a function. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by lazy {
        computeName()
    }
}
```

In this example, the `name` property is a delegated property. The delegate is a function. When you access the `name` property, the `computeName()` function will be called. The result will be returned.

## Delegating to an Object

In Kotlin, you can use the `by` keyword to delegate to an object. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by NameDelegate()
}
```

In this example, the `name` property is a delegated property. The delegate is an object. When you access the `name` property, the `NameDelegate` object will be used to compute the value of the property. The result will be returned.

## Delegating to a Class

In Kotlin, you can use the `by` keyword to delegate to a class. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by lazy {
        NameDelegate.computeName()
    }
}
```

In this example, the `name` property is a delegated property. The delegate is a class. When you access the `name` property, the `NameDelegate.computeName()` method will be called. The result will be returned.

## Delegating to a Superclass

In Kotlin, you can use the `by` keyword to delegate to a superclass. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User : SuperUser() {
    val name: String by lazy {
        super.name
    }
}
```

In this example, the `name` property is a delegated property. The delegate is the `name` property of the superclass. When you access the `name` property, the `name` property of the superclass will be accessed. The result will be returned.

## Delegating to a Companion Object

In Kotlin, you can use the `by` keyword to delegate to a companion object. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by lazy {
        User.name
    }
}
```

In this example, the `name` property is a delegated property. The delegate is the `name` property of the companion object. When you access the `name` property, the `name` property of the companion object will be accessed. The result will be returned.

## Delegating to an Interface

In Kotlin, you can use the `by` keyword to delegate to an interface. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by NameDelegate()
}
```

In this example, the `name` property is a delegated property. The delegate is an interface. When you access the `name` property, the `NameDelegate` interface will be used to compute the value of the property. The result will be returned.

## Delegating to an Abstract Class

In Kotlin, you can use the `by` keyword to delegate to an abstract class. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by lazy {
        NameDelegate.computeName()
    }
}
```

In this example, the `name` property is a delegated property. The delegate is an abstract class. When you access the `name` property, the `NameDelegate.computeName()` method will be called. The result will be returned.

## Delegating to an Object Literal

In Kotlin, you can use the `by` keyword to delegate to an object literal. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by mapOf("id" to 1, "name" to "John")
}
```

In this example, the `name` property is a delegated property. The delegate is an object literal. When you access the `name` property, the map will be searched for the key `name`. If the key is found, the corresponding value will be returned. If the key is not found, an exception will be thrown.

## Delegating to a Nested Class

In Kotlin, you can use the `by` keyword to delegate to a nested class. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by lazy {
        NestedClass.name
    }
}
```

In this example, the `name` property is a delegated property. The delegate is a nested class. When you access the `name` property, the `NestedClass.name` property will be accessed. The result will be returned.

## Delegating to an Inner Class

In Kotlin, you can use the `by` keyword to delegate to an inner class. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by lazy {
        InnerClass.name
    }
}
```

In this example, the `name` property is a delegated property. The delegate is an inner class. When you access the `name` property, the `InnerClass.name` property will be accessed. The result will be returned.

## Delegating to an Anonymous Object

In Kotlin, you can use the `by` keyword to delegate to an anonymous object. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by lazy {
        object: NameDelegate {
            override fun computeName(): String {
                // compute the name
            }
        }
    }
}
```

In this example, the `name` property is a delegated property. The delegate is an anonymous object. When you access the `name` property, the `computeName()` method of the anonymous object will be called. The result will be returned.

## Delegating to a Lambda

In Kotlin, you can use the `by` keyword to delegate to a lambda. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by lazy {
        // compute the name
    }
}
```

In this example, the `name` property is a delegated property. The delegate is a lambda. When you access the `name` property, the lambda will be called. The result will be returned.

## Delegating to a Method Reference

In Kotlin, you can use the `by` keyword to delegate to a method reference. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name. You could create this property by using the `by` keyword:

```kotlin
class User {
    val name: String by lazy {
        User::name
    }
}
```

In this example, the `name` property is a delegated property. The delegate is a method reference. When you access the `name` property, the `name` method of the `User` class will be called. The result will be returned.

## Delegating to a Constructor

In Kotlin, you can use the `by` keyword to delegate to a constructor. For example, suppose you have a class that represents a user. You might want to create a property that stores the user's name