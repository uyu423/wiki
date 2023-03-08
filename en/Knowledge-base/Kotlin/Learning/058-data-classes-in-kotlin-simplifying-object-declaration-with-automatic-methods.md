---
title: 058: Data Classes in Kotlin: Simplifying Object Declaration with Automatic Methods
description: 
published: true
date: 2023-02-15T21:55:44.181Z
tags: 
editor: markdown
dateCreated: 2023-02-15T21:55:36.355Z
---

- [058: Clases de datos en Kotlin: simplificación de la declaración de objetos con métodos automáticos***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/058-data-classes-in-kotlin-simplifying-object-declaration-with-automatic-methods)
{.links-list}
- [058：Kotlin 中的数据类：使用自动方法简化对象声明***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/058-data-classes-in-kotlin-simplifying-object-declaration-with-automatic-methods)
{.links-list}
- [058: Kotlin의 데이터 클래스: 자동 메서드로 개체 선언 간소화***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/058-data-classes-in-kotlin-simplifying-object-declaration-with-automatic-methods)
{.links-list}


# Data Classes in Kotlin: Simplifying Object Declaration with Automatic Methods

Kotlin is a JVM language that aims to be a more concise and practical alternative to Java. It has many features that Java developers will find familiar, as well as a few new ones that can make development quicker and easier.

One of these features is data classes. In Kotlin, a data class is a class that is designed to hold data. Data classes have a few specific features that make them different from regular classes:

- They can't be abstract, open, sealed, or inner.
- They can't have any properties other than those declared in the primary constructor.
- They can have one primary constructor with up to twenty-six parameters.
- All primary constructor parameters must be marked as val or var.
- Data classes can't be generic.

Data classes are useful because they automatically generate a number of methods for you. These methods include:

- ```toString()```: Returns a string representation of the object.
- ```equals()```: Compares this object with the specified object for equality.
- ```hashCode()```: Returns a hash code value for the object.
- ```copy()```: Creates a copy of the object.

In addition, data classes can also generate a ```componentN()``` function for each property in the class. This function can be used to access the properties of the data class in a more concise way.

To create a data class, you use the ```data``` keyword:

```kotlin
data class User(val id: Long, val name: String, val email: String)
```

This creates a data class with three properties: ```id```, ```name```, and ```email```. Note that all of the properties are marked as ```val```, which means they're immutable. You can also mark properties as ```var```, which means they're mutable.

Once you've created a data class, you can create objects of that class using the usual syntax:

```kotlin
val user = User(1, "John", "john@example.com")
```

You can then access the properties of the object using the generated ```componentN()``` functions:

```kotlin
println(user.id) // 1
println(user.name) // John
println(user.email) // john@example.com
```

You can also use the generated ```toString()```, ```equals()```, and ```hashCode()``` functions:

```kotlin
println(user.toString()) // User(id=1, name=John, email=john@example.com)

val anotherUser = User(1, "John", "john@example.com")
println(user == anotherUser) // true

val yetAnotherUser = User(2, "John", "john@example.com")
println(user == yetAnotherUser) // false

println(user.hashCode()) // 367910362
println(anotherUser.hashCode()) // 367910362
println(yetAnotherUser.hashCode()) // 367586981
```

Finally, you can use the ```copy()``` function to create a copy of an object with some or all of the properties changed:

```kotlin
val user2 = user.copy(id = 2)
println(user2.id) // 2
println(user2.name) // John
println(user2.email) // john@example.com

val user3 = user.copy(name = "Jane")
println(user3.id) // 1
println(user3.name) // Jane
println(user3.email) // john@example.com

val user4 = user.copy(id = 2, name = "Jane", email = "jane@example.com")
println(user4.id) // 2
println(user4.name) // Jane
println(user4.email) // jane@example.com
```

As you can see, data classes can be a very convenient way to create and work with objects in Kotlin. Not only do they save you from writing a lot of boilerplate code, but they also provide a number of useful methods for free.