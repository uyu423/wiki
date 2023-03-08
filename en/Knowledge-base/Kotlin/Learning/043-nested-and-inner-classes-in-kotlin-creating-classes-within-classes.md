---
title: 043: Nested and Inner Classes in Kotlin: Creating Classes within Classes
description: 
published: true
date: 2023-02-16T13:32:37.257Z
tags: 
editor: markdown
dateCreated: 2023-02-16T13:32:29.316Z
---

- [043: Clases internas y anidadas en Kotlin: creación de clases dentro de clases***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/043-nested-and-inner-classes-in-kotlin-creating-classes-within-classes)
{.links-list}
- [043：Kotlin 中的嵌套类和内部类：在类中创建类***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/043-nested-and-inner-classes-in-kotlin-creating-classes-within-classes)
{.links-list}
- [043: Kotlin의 중첩 및 내부 클래스: 클래스 내에 클래스 만들기***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/043-nested-and-inner-classes-in-kotlin-creating-classes-within-classes)
{.links-list}


# 043: Nested and Inner Classes in Kotlin: Creating Classes within Classes

Kotlin supports two types of classes that can be created within another class: nested classes and inner classes. In this post, we'll take a look at the differences between nested and inner classes in Kotlin, and how to create each type of class.

## Nested Classes

A nested class is a class that is defined within another class. Nested classes are not members of the class in which they are defined. They are simply classes that are defined within another class.

Here's an example of a nested class in Kotlin:

```kotlin
class OuterClass {
    class NestedClass {
        // ...
    }
}
```

In the example above, the `NestedClass` is not a member of the `OuterClass`. It is simply a class that is defined within the `OuterClass`.

Nested classes can be used to group related classes together. For example, if you have a class that represents a car, you could create a nested class that represents the engine of the car.

Nested classes can also be used to create static members of a class. In the example below, the `NestedClass` has a static member called `foo`:

```kotlin
class OuterClass {
    class NestedClass {
        companion object {
            val foo = "bar"
        }
    }
}
```

In the example above, the `NestedClass` has a static member called `foo`. This means that the `NestedClass` can be accessed without an instance of the `OuterClass`.

## Inner Classes

An inner class is a class that is defined within another class and is a member of that class. Inner classes have access to the members of the class in which they are defined.

Here's an example of an inner class in Kotlin:

```kotlin
class OuterClass {
    inner class InnerClass {
        // ...
    }
}
```

In the example above, the `InnerClass` is a member of the `OuterClass`. This means that the `InnerClass` has access to the members of the `OuterClass`.

Inner classes can be used to create objects that are associated with a particular instance of a class. For example, if you have a class that represents a car, you could create an inner class that represents the engine of the car.

Inner classes can also be used to create anonymous classes. An anonymous class is a class that is defined without a name. Anonymous classes are useful for creating objects that are not associated with any particular instance of a class.

Here's an example of an anonymous inner class in Kotlin:

```kotlin
class OuterClass {
    val anonymousInnerClass = object: SomeType {
        // ...
    }
}
```

In the example above, an anonymous inner class is created that implements the `SomeType` interface.

## Conclusion

In this post, we've taken a look at the differences between nested and inner classes in Kotlin. We've also seen how to create each type of class.