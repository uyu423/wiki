---
title: 040：Kotlin 中的伴随对象：实现静态成员
description: 
published: true
date: 2023-02-16T12:32:59.909Z
tags: 
editor: markdown
dateCreated: 2023-02-16T12:32:58.121Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [040: Companion Objects in Kotlin: Implementing Static Members***English** document is available*](/en/Knowledge-base/Kotlin/Learning/040-companion-objects-in-kotlin-implementing-static-members)
{.links-list}




伴随对象是在 Kotlin 中实现静态成员的好方法。通过使用伴随对象，您可以避免为每个静态成员创建一个单独的类。

要创建伴生对象，只需在对象声明前添加关键字“companion”。例如，要为名为“MyClass”的类创建伴随对象，您可以添加以下代码：

```kotlin
class MyClass {
    companion object {
        // ...
    }
}
```

在伴生对象中，您可以添加所需的任何静态成员。例如，您可以像这样添加一个静态字段：

```kotlin
class MyClass {
    companion object {
        val myField = "Hello, world!"
    }
}
```

您还可以添加静态方法。例如，您可以添加一个名为“myMethod”的静态方法，如下所示：

```kotlin
class MyClass {
    companion object {
        fun myMethod() {
            // ...
        }
    }
}
```

要访问伴生对象的成员，可以使用类名后跟伴生对象名。例如，要访问“myField”字段，您可以使用以下代码：

```kotlin
MyClass.myField // "Hello, world!"
```

要调用“myMethod”方法，您可以使用以下代码：

```kotlin
MyClass.myMethod()
```

使用伴生对象的优点之一是可以避免名称冲突。例如，假设您有一个名为“Foo”的类和另一个名为“Bar”的类。如果两个类都有一个名为“myField”的静态字段，您可以使用以下代码访问每个字段：

```kotlin
Foo.myField // accesses the "myField" field in the "Foo" class
Bar.myField // accesses the "myField" field in the "Bar" class
```

使用伴生对象的另一个优点是您可以从对象外部访问伴生对象的私有成员。例如，假设您有一个带有名为“myField”的私有字段的伴生对象：

```kotlin
class MyClass {
    companion object {
        private val myField = "Hello, world!"
    }
}
```

您可以使用以下代码从伴随对象外部访问此字段：

```kotlin
MyClass.Companion.myField // "Hello, world!"
```

如果你想创建一个返回伴随对象实例的静态工厂方法，这会很有用。例如，您可以创建一个名为“create”的静态工厂方法，如下所示：

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

然后，您可以使用以下代码从伴生对象外部调用此方法：

```kotlin
MyClass.Companion.create() // creates and returns an instance of the "MyClass" class
```

使用伴生对象的缺点之一是它们会使您的代码更难阅读。例如，假设您有一个名为“Foo”的类和一个伴生对象。如果要访问伴随对象的成员，则必须使用对象的全名：

```kotlin
Foo.Companion.myField // accesses the "myField" field in the "Foo" class
```

这会使您的代码更难阅读，尤其是当您经常访问伴随对象的成员时。

使用伴生对象的另一个缺点是它们不能被继承。例如，假设您有一个名为“Foo”的类和一个伴生对象。如果创建“Foo”的子类，子类将不会继承伴生对象：

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

如果您想在子类中创建静态工厂方法，这可能会成为一个问题。例如，假设您想在“FooSubclass”中创建一个返回“FooSubclass”实例的静态工厂方法。您不能这样做，因为“FooSubclass”没有从“Foo”类继承伴随对象：

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

如果你希望能够继承伴生对象，你可以使用嵌套类来代替。例如，您可以创建一个名为“Companion”的嵌套类，如下所示：

```kotlin
class Foo {
    class Companion {
        // ...
    }
}
```

然后“Companion”类可以被子类继承：

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

总之，伴随对象是在 Kotlin 中实现静态成员的好方法。它们的优点是能够避免名称冲突并能够从对象外部访问私有成员。但是，它们的缺点是更难阅读并且不能被继承。