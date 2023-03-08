---
title: 011: Properties and Fields in Kotlin: Understanding Getters and Setters
description: 
published: true
date: 2023-01-31T05:36:56.370Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:36:54.284Z
---

- [011: Kotlin의 속성 및 필드: Getter 및 Setter 이해***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/011-properties-and-fields-in-kotlin-understanding-getters-and-setters)
{.links-list}
- [011: Kotlin のプロパティとフィールド: ゲッターとセッターを理解する***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/011-properties-and-fields-in-kotlin-understanding-getters-and-setters)
{.links-list}
- [011：Kotlin 中的属性和字段：了解 getter 和 setter***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/011-properties-and-fields-in-kotlin-understanding-getters-and-setters)
{.links-list}


# Properties and Fields in Kotlin: Understanding Getters and Setters

In Kotlin, properties and fields can have custom getters and setters. By default, properties and fields have public visibility, meaning that they can be accessed from outside the class.

## Properties

Properties are declared using the `val` keyword. They are immutable, meaning that they can only be assigned once.

```kotlin
val name = "John"
```

In the example above, the `name` property is initialized with the value "John". It cannot be reassigned.

## Fields

Fields are declared using the `var` keyword. They are mutable, meaning that they can be reassigned.

```kotlin
var name = "John"
name = "Jane"
```

In the example above, the `name` field is initialized with the value "John". It can be reassigned to "Jane".

## Getters and Setters

By default, properties and fields have public visibility, meaning that they can be accessed from outside the class. However, we can create custom getters and setters to control how they are accessed.

Getters are used to retrieve the value of a property or field. They are invoked when we use the property or field in our code.

Setters are used to reassign the value of a property or field. They are invoked when we reassign the property or field in our code.

Consider the following property:

```kotlin
var name: String = "John"
```

We can create custom getters and setters for this property as follows:

```kotlin
var name: String = "John"
    get() {
        return field
    }
    set(value) {
        field = value
    }
```

In the example above, the `get()` function is the getter and the `set(value)` function is the setter. The `get()` function returns the value of the `name` field and the `set(value)` function sets the value of the `name` field.

We can also create custom getters and setters for properties and fields that are declared with the `val` keyword. In this case, we can only create a custom getter. We cannot create a custom setter because the property is immutable.

Consider the following property:

```kotlin
val name: String = "John"
```

We can create a custom getter for this property as follows:

```kotlin
val name: String = "John"
    get() {
        return field
    }
```

In the example above, the `get()` function is the getter. The `get()` function returns the value of the `name` field.

## Conclusion

In Kotlin, properties and fields can have custom getters and setters. Getters are used to retrieve the value of a property or field and setters are used to reassign the value of a property or field.