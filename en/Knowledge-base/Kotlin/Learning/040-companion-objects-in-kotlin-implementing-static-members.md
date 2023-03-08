---
title: 040: Companion Objects in Kotlin: Implementing Static Members
description: 
published: true
date: 2023-02-16T12:33:06.333Z
tags: 
editor: markdown
dateCreated: 2023-02-16T12:32:58.127Z
---

- [040: Objetos complementarios en Kotlin: Implementación de miembros estáticos***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/040-companion-objects-in-kotlin-implementing-static-members)
{.links-list}
- [040：Kotlin 中的伴随对象：实现静态成员***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/040-companion-objects-in-kotlin-implementing-static-members)
{.links-list}
- [040: Kotlin의 컴패니언 객체: 정적 멤버 구현***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/040-companion-objects-in-kotlin-implementing-static-members)
{.links-list}




Companion objects are a great way to implement static members in Kotlin. By using companion objects, you can avoid having to create a separate class for each static member.

To create a companion object, you simply add the keyword "companion" before the object declaration. For example, to create a companion object for a class named "MyClass", you would add the following code:

```kotlin
class MyClass {
    companion object {
        // ...
    }
}
```

Within the companion object, you can add any static members that you want. For example, you could add a static field like this:

```kotlin
class MyClass {
    companion object {
        val myField = "Hello, world!"
    }
}
```

You can also add static methods. For example, you could add a static method named "myMethod" like this:

```kotlin
class MyClass {
    companion object {
        fun myMethod() {
            // ...
        }
    }
}
```

To access members of the companion object, you use the name of the class followed by the companion object name. For example, to access the "myField" field, you would use the following code:

```kotlin
MyClass.myField // "Hello, world!"
```

And to call the "myMethod" method, you would use the following code:

```kotlin
MyClass.myMethod()
```

One advantage of using companion objects is that you can avoid name collisions. For example, suppose you have a class named "Foo" and another class named "Bar". If both classes have a static field named "myField", you can access each field using the following code:

```kotlin
Foo.myField // accesses the "myField" field in the "Foo" class
Bar.myField // accesses the "myField" field in the "Bar" class
```

Another advantage of using companion objects is that you can access private members of the companion object from outside the object. For example, suppose you have a companion object with a private field named "myField":

```kotlin
class MyClass {
    companion object {
        private val myField = "Hello, world!"
    }
}
```

You can access this field from outside the companion object using the following code:

```kotlin
MyClass.Companion.myField // "Hello, world!"
```

This can be useful if you want to create a static factory method that returns an instance of the companion object. For example, you could create a static factory method named "create" like this:

```kotlin
class MyClass {
    companion object {
        private val myField = "Hello, world!"
        
        fun create(): MyClass {
            return MyClass()
        }
    }
}
```

You can then call this method from outside the companion object using the following code:

```kotlin
MyClass.Companion.create() // creates and returns an instance of the "MyClass" class
```

One disadvantage of using companion objects is that they can make your code more difficult to read. For example, suppose you have a class named "Foo" with a companion object. If you want to access a member of the companion object, you have to use the full name of the object:

```kotlin
Foo.Companion.myField // accesses the "myField" field in the "Foo" class
```

This can make your code more difficult to read, especially if you're accessing members of the companion object frequently.

Another disadvantage of using companion objects is that they can't be inherited. For example, suppose you have a class named "Foo" with a companion object. If you create a subclass of "Foo", the subclass will not inherit the companion object:

```kotlin
class Foo {
    companion object {
        // ...
    }
}

class FooSubclass: Foo {
    // does not inherit the companion object from the "Foo" class
}
```

This can be a problem if you want to create a static factory method in the subclass. For example, suppose you want to create a static factory method in the "FooSubclass" that returns an instance of the "FooSubclass". You can't do this because the "FooSubclass" does not inherit the companion object from the "Foo" class:

```kotlin
class Foo {
    companion object {
        // ...
    }
}

class FooSubclass: Foo {
    companion object {
        fun create(): FooSubclass { // error: does not inherit the companion object from the "Foo" class
            return FooSubclass()
        }
    }
}
```

If you want to be able to inherit the companion object, you can use a nested class instead. For example, you could create a nested class named "Companion" like this:

```kotlin
class Foo {
    class Companion {
        // ...
    }
}
```

The "Companion" class can then be inherited by subclasses:

```kotlin
class Foo {
    class Companion {
        // ...
    }
}

class FooSubclass: Foo() {
    class Companion: Foo.Companion() {
        fun create(): FooSubclass {
            return FooSubclass()
        }
    }
}
```

In summary, companion objects are a great way to implement static members in Kotlin. They have the advantages of being able to avoid name collisions and being able to access private members from outside the object. However, they have the disadvantages of being more difficult to read and not being able to be inherited.