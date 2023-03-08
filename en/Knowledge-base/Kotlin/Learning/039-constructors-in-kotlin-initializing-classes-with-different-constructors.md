---
title: 039: Constructors in Kotlin: Initializing Classes with Different Constructors
description: 
published: true
date: 2023-02-16T11:32:57.765Z
tags: 
editor: markdown
dateCreated: 2023-02-16T11:32:49.874Z
---

- [039: Constructores en Kotlin: inicialización de clases con diferentes constructores***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/039-constructors-in-kotlin-initializing-classes-with-different-constructors)
{.links-list}
- [039：Kotlin 中的构造函数：使用不同的构造函数初始化类***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/039-constructors-in-kotlin-initializing-classes-with-different-constructors)
{.links-list}
- [039: Kotlin의 생성자: 다른 생성자로 클래스 초기화***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/039-constructors-in-kotlin-initializing-classes-with-different-constructors)
{.links-list}


# 039: Constructors in Kotlin: Initializing Classes with Different Constructors

Kotlin offers a wide variety of options when it comes to initializing classes. In this post, we'll take a look at constructors in Kotlin and how they can be used to initialize classes with different values.

Constructors are special functions that are used to initialize classes. In Kotlin, there are two types of constructors: primary and secondary. The primary constructor is the one that is used to initialize the class when it is first created. It is declared at the top of the class, before the body of the class.

Secondary constructors are used to initialize the class with different values. They are declared inside the body of the class.

Classes can have multiple secondary constructors, but they must all call the primary constructor. This ensures that the class is always initialized with at least the default values.

To create a class with a primary constructor, we use the keyword `class` followed by the name of the class. We then declare the primary constructor inside parentheses. Inside the primary constructor, we can declare any number of parameters. These parameters can be either val or var.

```kotlin
class MyClass(val param1: String, var param2: Int) {

}
```

In the example above, we have created a class called `MyClass` with a primary constructor that takes two parameters. The first parameter is a `val` and the second is a `var`.

We can also create a class without a primary constructor. In this case, the class will be initialized with the default values for each of the parameters.

```kotlin
class MyClass {

}
```

To create a secondary constructor, we use the keyword `constructor` followed by the parameters inside parentheses. We can then initialize the class with different values inside the body of the secondary constructor.

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

}
```

In the example above, we have created a secondary constructor that takes a single parameter. This constructor calls the primary constructor and passes in the default value for the second parameter.

We can also create a class with multiple secondary constructors. In this case, each secondary constructor must call a different secondary constructor.

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

In the example above, we have created a class with two secondary constructors. The first constructor calls the primary constructor and the second constructor calls the first secondary constructor.

We can also create a class with a primary constructor and multiple secondary constructors. In this case, each secondary constructor must call the primary constructor.

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

In the example above, we have created a class with a primary constructor and two secondary constructors. The first secondary constructor calls the primary constructor and the second secondary constructor calls the first secondary constructor.

We can also create a class with a primary constructor and multiple secondary constructors. In this case, each secondary constructor must call a different secondary constructor.

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

In the example above, we have created a class with a primary constructor and two secondary constructors. The first secondary constructor calls the primary constructor and the second secondary constructor calls the first secondary constructor.

We can also create a class with a primary constructor and multiple secondary constructors. In this case, each secondary constructor must call the primary constructor.

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

In the example above, we have created a class with a primary constructor and two secondary constructors. The first secondary constructor calls the primary constructor and the second secondary constructor calls the first secondary constructor.