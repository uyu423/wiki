---
title: 018: Companion Objects in Kotlin: Static Members in Classes
description: 
published: true
date: 2023-02-16T05:32:22.873Z
tags: 
editor: markdown
dateCreated: 2023-02-16T05:32:14.985Z
---

- [018: Objetos complementarios en Kotlin: miembros estáticos en clases***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/018-companion-objects-in-kotlin-static-members-in-classes)
{.links-list}
- [018：Kotlin 中的伴随对象：类中的静态成员***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/018-companion-objects-in-kotlin-static-members-in-classes)
{.links-list}
- [018: Kotlin의 컴패니언 객체: 클래스의 정적 멤버***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/018-companion-objects-in-kotlin-static-members-in-classes)
{.links-list}


# Companion Objects in Kotlin: Static Members in Classes

Kotlin companion objects allow you to define static members in a class. In this post, we'll take a look at what companion objects are and how to use them.

## What are Companion Objects?

 Companion objects are objects that are associated with a class. They are used to store static members in a class.

Static members are members that are associated with a class, not with an instance of a class. This means that you can access them without creating an instance of the class.

 Companion objects are declared using the `companion object` keyword. They can be used to store constants, utility functions, and factory methods.

## How to Use Companion Objects

Companion objects are declared using the `companion object` keyword. They can be used to store constants, utility functions, and factory methods.

To access members of a companion object, you use the class name as a qualifier. For example, if you have a companion object named `MyClass` in a file named `MyClass.kt`, you would access its members like this:

```kotlin
MyClass.Companion.myFunction()
```

If you want to access members of a companion object from within the class, you can omit the `companion` keyword. For example:

```kotlin
class MyClass {
    companion object {
        fun myFunction() {
            // ...
        }
    }
}
```

## Conclusion

In this post, we've looked at what companion objects are and how to use them. Companion objects are a great way to store static members in a class.