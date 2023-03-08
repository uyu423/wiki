---
title: 076: The Null Object Pattern in Kotlin: Providing a Non-Null Object in Place of Null
description: 
published: true
date: 2023-02-17T05:32:27.177Z
tags: 
editor: markdown
dateCreated: 2023-02-17T05:32:25.021Z
---

- [076: El patrón de objeto nulo en Kotlin: proporcionar un objeto no nulo en lugar de nulo***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/076-the-null-object-pattern-in-kotlin-providing-a-non-null-object-in-place-of-null)
{.links-list}
- [076：Kotlin 中的空对象模式：提供非空对象代替空对象***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/076-the-null-object-pattern-in-kotlin-providing-a-non-null-object-in-place-of-null)
{.links-list}
- [076: Kotlin의 Null 개체 패턴: Null 대신 Null이 아닌 개체 제공***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/076-the-null-object-pattern-in-kotlin-providing-a-non-null-object-in-place-of-null)
{.links-list}


# The Null Object Pattern in Kotlin: Providing a Non-Null Object in Place of Null

Kotlin's type system is designed to eliminate the need for null values. However, there are times when null values are required, such as when interfacing with legacy code written in Java. In these cases, the null object pattern can be used to provide a non-null object in place of a null value.

## What is the Null Object Pattern?

The null object pattern is a design pattern that aims to eliminate the need for null values. It does this by providing a non-null object in place of a null value. This non-null object can be used to represent the absence of a value.

## How Does the Null Object Pattern Work?

The null object pattern works by creating an object that represents the absence of a value. This object can be used in place of a null value. The object can be given a default value, such as an empty string, or it can be given a behavior that is appropriate for the situation.

## When Should the Null Object Pattern be Used?

The null object pattern should be used when null values are required, such as when interfacing with legacy code written in Java.

## What are the Benefits of the Null Object Pattern?

The null object pattern has several benefits:

- It eliminates the need for null values.
- It makes code more readable.
- It makes code more maintainable.
- It makes code more extensible.

## What are the Drawbacks of the Null Object Pattern?

The null object pattern has one drawback:

- It can add complexity to code.

## Kotlin Implementation

The null object pattern can be implemented in Kotlin using the following steps:

1. Create an interface for the object.
2. Create a class that implements the interface.
3. Create an object that represents the absence of a value.

### Step 1: Create an Interface for the Object

The first step is to create an interface for the object. This interface will define the contract for the object.

```kotlin
interface MyInterface {
    fun doSomething()
}
```

### Step 2: Create a Class that Implements the Interface

The second step is to create a class that implements the interface. This class will provide the implementation for the object.

```kotlin
class MyClass : MyInterface {
    override fun doSomething() {
        // do something
    }
}
```

### Step 3: Create an Object that Represents the Absence of a Value

The third step is to create an object that represents the absence of a value. This object can be used in place of a null value.

```kotlin
object MyObject : MyInterface {
    override fun doSomething() {
        // do something
    }
}
```

## Usage

The null object pattern can be used as follows:

```kotlin
fun doSomething(myInterface: MyInterface?) {
    if (myInterface != null) {
        myInterface.doSomething()
    }
}

fun main() {
    val myClass: MyClass? = MyClass()
    val myObject: MyObject? = MyObject()

    doSomething(myClass)
    doSomething(myObject)
}
```

## Additional Information

- The null object pattern is also known as the dummy object pattern.

## Warnings

- The null object pattern should only be used when null values are required.

## Dangers

- The null object pattern can add complexity to code.