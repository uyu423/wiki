---
title: Implementing Constructors and Properties in Kotlin
description: 
published: true
date: 2023-02-02T02:18:23.835Z
tags: 
editor: markdown
dateCreated: 2023-02-02T02:18:19.502Z
---

- [Implementación de constructores y propiedades en Kotlin***Spanish** document is available*](/es/Knowledge-base/Kotlin/implementing-constructors-and-properties-in-kotlin)
{.links-list}
- [在 Kotlin 中实现构造函数和属性***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/implementing-constructors-and-properties-in-kotlin)
{.links-list}
- [Kotlin에서 생성자 및 속성 구현***Korean** document is available*](/ko/Knowledge-base/Kotlin/implementing-constructors-and-properties-in-kotlin)
{.links-list}


# Implementing Constructors and Properties in Kotlin

Kotlin is a relatively new programming language that has been gaining popularity in the development community. It is a statically typed, object-oriented language that runs on the Java Virtual Machine. Kotlin is compatible with all existing Java libraries and frameworks and can be used for a wide range of development tasks.

One of the main features of Kotlin is its support for constructor-based programming. In Kotlin, classes can have one or more constructors. The primary constructor is defined in the class header, and secondary constructors are defined inside the class body.

Constructors are used to initialize objects of a class. They can be used to set initial values for variables, invoke methods, and so on. In Kotlin, constructors are not required if the class does not have any initializers. However, if a class does have initializers, at least one constructor must be defined.

The following is a simple example of a Kotlin class with a primary constructor and two secondary constructors:

```kotlin
class Person(val name: String) {
  
    var age: Int = 0
    
    constructor(name: String, age: Int) : this(name) {
        this.age = age
    }
    
    constructor(name: String, age: Int, gender: String) : this(name, age) {
        // ...
    }
}
```

In the example above, the primary constructor takes a single argument, name. The secondary constructors take two and three arguments, respectively. All constructors call the primary constructor using the this keyword.

Constructors can also be used to initialize properties of a class. In the example above, the name property is initialized by the primary constructor, and the age property is initialized by the secondary constructors.

Another feature of Kotlin is its support for properties. Properties are variables that are associated with a class. They can be declared in the class header or in the class body.

The following is a simple example of a Kotlin class with two properties, name and age:

```kotlin
class Person {
  
    var name: String = ""
    
    var age: Int = 0
}
```

In the example above, the name and age properties are declared in the class header. They are both initialized with the default values of "" and 0, respectively.

Properties can also be initialized with non-default values. In the following example, the name property is initialized with the value "John" and the age property is initialized with the value 30:

```kotlin
class Person {
  
    var name: String = "John"
    
    var age: Int = 30
}
```

Kotlin also supports lazy initialization of properties. Lazy initialization is a technique for delaying the initialization of a property until it is first accessed. In Kotlin, lazy initialization is accomplished using the by keyword.

The following is a simple example of a Kotlin class with a lazy-initialized property, name:

```kotlin
class Person {
  
    val name: String by lazy {
        // ...
    }
}
```

In the example above, the name property is declared as a val (immutable) and is initialized lazily. The initializer is a lambda expression that is invoked when the property is first accessed.

Kotlin also supports delegated properties. Delegated properties are properties that are implemented by a delegate object. In Kotlin, delegated properties are declared using the by keyword.

The following is a simple example of a Kotlin class with a delegated property, name:

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

In the example above, the name property is implemented by a delegate object. The delegate object is lazily initialized by a lambda expression.

Kotlin also supports extension properties. Extension properties are properties that are declared as extensions of a class. In Kotlin, extension properties are declared using the by keyword.

The following is a simple example of a Kotlin class with an extension property, name:

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

In the example above, the name property is extended by a lazy lambda expression that invokes the extension() method.

Kotlin also supportslate-initialized properties. Late-initialized properties are properties that are not initialized until they are first accessed. In Kotlin, late-initialized properties are declared using the by keyword.

The following is a simple example of a Kotlin class with a late-initialized property, name:

```kotlin
class Person {
  
    lateinit var name: String
    
    fun init() {
        name = "John"
    }
}
```

In the example above, the name property is declared as a lateinit var (mutable). It is not initialized until the init() method is invoked.

Kotlin also supports nullable types. Nullable types are types that can hold the value null. In Kotlin, nullable types are declared using the ? operator.

The following is a simple example of a Kotlin class with a nullable property, name:

```kotlin
class Person {
  
    var name: String? = null
}
```

In the example above, the name property is declared as a nullable type. It can hold the value null.

Kotlin also supportsimmutable properties. Immutable properties are properties that cannot be changed after they are initialized. In Kotlin, immutable properties are declared using the val keyword.

The following is a simple example of a Kotlin class with an immutable property, name:

```kotlin
class Person(val name: String) {
  
}
```

In the example above, the name property is declared as a val (immutable). It cannot be changed after it is initialized.

Kotlin also supports mutable properties. Mutable properties are properties that can be changed after they are initialized. In Kotlin, mutable properties are declared using the var keyword.

The following is a simple example of a Kotlin class with a mutable property, name:

```kotlin
class Person {
  
    var name: String = ""
}
```

In the example above, the name property is declared as a var (mutable). It can be changed after it is initialized.

Kotlin also supports backing fields. Backing fields are variables that are used to store the values of properties. In Kotlin, backing fields are declared using the field keyword.

The following is a simple example of a Kotlin class with a backing field, name:

```kotlin
class Person {
  
    var name: String = ""
        private set
}
```

In the example above, the name property has a backing field. The backing field is declared as a private set, which means that it can only be modified by the setter of the property.

Kotlin also supports delegated properties. Delegated properties are properties that are implemented by a delegate object. In Kotlin, delegated properties are declared using the by keyword.

The following is a simple example of a Kotlin class with a delegated property, name:

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

In the example above, the name property is implemented by a delegate object. The delegate object is lazily initialized by a lambda expression.

Kotlin also supports extension properties. Extension properties are properties that are declared as extensions of a class. In Kotlin, extension properties are declared using the by keyword.

The following is a simple example of a Kotlin class with an extension property, name:

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

In the example above, the name property is extended by a lazy lambda expression that invokes the extension() method.

Kotlin also supportslate-initialized properties. Late-initialized properties are properties that are not initialized until they are first accessed. In Kotlin, late-initialized properties are declared using the by keyword.

The following is a simple example of a Kotlin class with a late-initialized property, name:

```kotlin
class Person {
  
    lateinit var name: String
    
    fun init() {
        name = "John"
    }
}
```

In the example above, the name property is declared as a lateinit var (mutable). It is not initialized until the init() method is invoked.

Kotlin also supports nullable types. Nullable types are types that can hold the value null. In Kotlin, nullable types are declared using the ? operator.

The following is a simple example of a Kotlin class with a nullable property, name:

```kotlin
class Person {
  
    var name: String? = null
}
```

In the example above, the name property is declared as a nullable type. It can hold the value null.

Kotlin also supportsimmutable properties. Immutable properties are properties that cannot be changed after they are initialized. In Kotlin, immutable properties are declared using the val keyword.

The following is a simple example of a Kotlin class with an immutable property, name:

```kotlin
class Person(val name: String) {
  
}
```

In the example above, the name property is declared as a val (immutable). It cannot be changed after it is initialized.

Kotlin also supports mutable properties. Mutable properties are properties that can be changed after they are initialized. In Kotlin, mutable properties are declared using the var keyword.

The following is a simple example of a Kotlin class with a mutable property, name:

```kotlin
class Person {
  
    var name: String = ""
}
```

In the example above, the name property is declared as a var (mutable). It can be changed after it is initialized.

Kotlin also supports backing fields. Backing fields are variables that are used to store the values of properties. In Kotlin, backing fields are declared using the field keyword.

The following is a simple example of a Kotlin class with a backing field, name:

```kotlin
class Person {
  
    var name: String = ""
        private set
}
```

In the example above, the name property has a backing field. The backing field is declared as a private set, which means that it can only be modified by the setter of the property.

Kotlin also supports delegated properties. Delegated properties are properties that are implemented by a delegate object. In Kotlin, delegated properties are declared using the by keyword.

The following is a simple example of a Kotlin class with a delegated property, name:

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

In the example above, the name property is implemented by a delegate object. The delegate object is lazily initialized by a lambda expression.

Kotlin also supports extension properties. Extension properties are properties that are declared as extensions of a class. In Kotlin, extension properties are declared using the by keyword.

The following is a simple example of a Kotlin class with an extension property, name:

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

In the example above, the name property is extended by a lazy lambda expression that invokes the extension() method.

Kotlin also supportslate-initialized properties. Late-initialized properties are properties that are not initialized until they are first accessed. In Kotlin, late-initialized properties are declared using the by keyword.

The following is a simple example of a Kotlin class with a late-initialized property, name:

```kotlin
class Person {
  
    lateinit var name: String
    
    fun init() {
        name = "John"
    }
}
```

In the example above, the name property is declared as a lateinit var (mutable). It is not initialized until the init() method is invoked.

Kotlin also supports nullable types. Nullable types are types that can hold the value null. In Kotlin, nullable types are declared using the ? operator.

The following is a simple example of a Kotlin class with a nullable property, name:

```kotlin
class Person {
  
    var name: String? = null
}
```

In the example above, the name property is declared as a nullable type. It can hold the value null.

Kotlin also supportsimmutable properties. Immutable properties are properties that cannot be changed after they are initialized. In Kotlin, immutable properties are declared using the val keyword.

The following is a simple example of a Kotlin class with an immutable property, name:

```kotlin
class Person(val name: String) {
  
}
```

In the example above, the name property is declared as a val (immutable). It cannot be changed after it is initialized.

Kotlin also supports mutable properties. Mutable properties are properties that can be changed after they are initialized. In Kotlin, mutable properties are declared using the var keyword.

The following is a simple example of a Kotlin class with a mutable property, name:

```kotlin
class Person {
  
    var name: String = ""
}
```

In the example above, the name property is declared as a var (mutable). It can be changed after it is initialized.

Kotlin also supports backing fields. Backing fields are variables that are used to store the values of properties. In Kotlin, backing fields are declared using the field keyword.

The following is a simple example of a Kotlin class with a backing field, name:

```kotlin
class Person {
  
    var name: String = ""
        private set
}
```

In the example above, the name property has a backing field. The backing field is declared as a private set, which means that it can only be modified by the setter of the property.

Kotlin also supports delegated properties. Delegated properties are properties that are implemented by a delegate object. In Kotlin, delegated properties are declared using the by keyword.

The following is a simple example of a Kotlin class with a delegated property, name:

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

In the example above, the name property is implemented by a delegate object. The delegate object is lazily initialized by a lambda expression.

Kotlin also supports extension properties. Extension properties are properties that are declared as extensions of a class. In Kotlin, extension properties are declared using the by keyword.

The following is a simple example of a Kotlin class with an extension property, name:

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

In the example above, the name property is extended by a lazy lambda expression that invokes the extension() method.

Kotlin also supportslate-initialized properties. Late-initialized properties are properties that are not initialized until they are first accessed. In Kotlin, late-initialized properties are declared using the by keyword.

The following is a simple example of a Kotlin class with a late-initialized property, name:

```kotlin
class Person {
  
    lateinit var name: String
    
    fun init() {
        name = "John"
    }
}
``