---
title: 044: Anonymous Inner Classes in Kotlin: Creating Classes Without Names
description: 
published: true
date: 2023-02-15T10:17:55.611Z
tags: 
editor: markdown
dateCreated: 2023-02-15T10:17:47.789Z
---

- [044: Clases internas anónimas en Kotlin: creación de clases sin nombres***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/044-anonymous-inner-classes-in-kotlin-creating-classes-without-names)
{.links-list}
- [044：Kotlin 中的匿名内部类：创建没有名称的类***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/044-anonymous-inner-classes-in-kotlin-creating-classes-without-names)
{.links-list}
- [044: Kotlin의 익명 내부 클래스: 이름 없이 클래스 만들기***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/044-anonymous-inner-classes-in-kotlin-creating-classes-without-names)
{.links-list}


# Anonymous Inner Classes in Kotlin: Creating Classes Without Names

In Kotlin, you can create anonymous inner classes without giving them a name. These classes are often used when you need to create a one-time object, or when you need an object that is only used in a limited scope.

Anonymous inner classes are declared using the `object` keyword:

```kotlin
object: SomeClass() {
    // Body of the anonymous inner class
}
```

You can also specify the supertype for the anonymous inner class using the `object` keyword:

```kotlin
object: SomeInterface {
    // Body of the anonymous inner class
}
```

## Creating an Anonymous Inner Class That Extends a Class

Let's create an anonymous inner class that extends the `Animal` class. We'll create an `Animal` class that has a `makeNoise` method. This method will be overridden in the anonymous inner class.

```kotlin
open class Animal {
    open fun makeNoise() {
        println("Some noise")
    }
}

val animal = object: Animal() {
    override fun makeNoise() {
        println("Bark")
    }
}

animal.makeNoise() // Prints "Bark"
```

In the code above, we created an `Animal` class and an anonymous inner class that extends it. We override the `makeNoise` method in the anonymous inner class. When we call the `makeNoise` method on the `animal` object, it prints "Bark".

## Creating an Anonymous Inner Class That Implements an Interface

You can also create anonymous inner classes that implement interfaces. Let's create an `Animal` interface with a `makeNoise` method. We'll create an anonymous inner class that implements this interface.

```kotlin
interface Animal {
    fun makeNoise()
}

val animal = object: Animal {
    override fun makeNoise() {
        println("Some noise")
    }
}

animal.makeNoise() // Prints "Some noise"
```

In the code above, we created an `Animal` interface and an anonymous inner class that implements it. We override the `makeNoise` method in the anonymous inner class. When we call the `makeNoise` method on the `animal` object, it prints "Some noise".

## Creating an Anonymous Inner Class That Extends a Class and Implements an Interface

You can also create anonymous inner classes that extend a class and implement an interface. Let's create an `Animal` interface with a `makeNoise` method. We'll also create an `Animal` class that has a `makeNoise` method. We'll create an anonymous inner class that extends the `Animal` class and implements the `Animal` interface.

```kotlin
interface Animal {
    fun makeNoise()
}

open class Animal {
    open fun makeNoise() {
        println("Some noise")
    }
}

val animal = object: Animal(), Animal {
    override fun makeNoise() {
        println("Bark")
    }
}

animal.makeNoise() // Prints "Bark"
```

In the code above, we created an `Animal` class and an `Animal` interface. We created an anonymous inner class that extends the `Animal` class and implements the `Animal` interface. We override the `makeNoise` method in the anonymous inner class. When we call the `makeNoise` method on the `animal` object, it prints "Bark".

## Creating an Object of an Anonymous Inner Class

When you create an anonymous inner class, an object of that class is also created. You can access this object using the `object` keyword.

```kotlin
interface Animal {
    fun makeNoise()
}

open class Animal {
    open fun makeNoise() {
        println("Some noise")
    }
}

val animal = object: Animal(), Animal {
    override fun makeNoise() {
        println("Bark")
    }
}

println(animal.javaClass) // Prints "class com.example.Animal$1"
```

In the code above, we created an `Animal` class and an `Animal` interface. We created an anonymous inner class that extends the `Animal` class and implements the `Animal` interface. We printed the class of the `animal` object using the `javaClass` property. As you can see, the `animal` object is an instance of the anonymous inner class.

## Creating a Static Nested Class

You can also create static nested classes in Kotlin. Static nested classes are declared using the `static` keyword:

```kotlin
class OuterClass {
    class NestedClass
}
```

Static nested classes can access the members of the outer class. They can also be declared `abstract` or `sealed`.

```kotlin
class OuterClass {
    class NestedClass {
        fun someMethod() {
            println("Some method")
        }
    }
}

val nestedClass = OuterClass.NestedClass()
nestedClass.someMethod() // Prints "Some method"
```

In the code above, we created a static nested class and an instance of that class. We called the `someMethod` method on the `nestedClass` object.

## Creating an Inner Class

Inner classes are non-static nested classes. Inner classes can access the members of the outer class. They can also be declared `abstract` or `sealed`.

```kotlin
class OuterClass {
    inner class InnerClass {
        fun someMethod() {
            println("Some method")
        }
    }
}

val outerClass = OuterClass()
val innerClass = outerClass.InnerClass()
innerClass.someMethod() // Prints "Some method"
```

In the code above, we created an inner class and an instance of that class. We called the `someMethod` method on the `innerClass` object.

## Conclusion

In this post, we learned about anonymous inner classes in Kotlin. We saw how to create anonymous inner classes that extend classes, implement interfaces, and extend classes and implement interfaces. We also saw how to create static nested classes and inner classes.