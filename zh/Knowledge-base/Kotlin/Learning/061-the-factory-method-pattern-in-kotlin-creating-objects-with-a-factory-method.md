---
title: 061：Kotlin 中的工厂方法模式：使用工厂方法创建对象
description: 
published: true
date: 2023-01-31T09:04:58.775Z
tags: 
editor: markdown
dateCreated: 2023-01-31T09:04:57.097Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [061: The Factory Method Pattern in Kotlin: Creating Objects with a Factory Method***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/061-the-factory-method-pattern-in-kotlin-creating-objects-with-a-factory-method)
{.links-list}




# 061：Kotlin 中的工厂方法模式：使用工厂方法创建对象

在软件开发中，工厂方法模式是一种创建型设计模式，它使用工厂方法来处理创建对象的问题，而不必指定将要创建的对象的确切类。这是通过工厂方法创建对象而不是调用构造函数来完成的。

在本文中，我们将讨论工厂方法模式以及如何在 Kotlin 中使用它来创建对象。我们还将查看一些代码示例，以演示如何在实践中使用此模式。

# # 什么是工厂方法模式？

工厂方法模式是一种创建型设计模式，它使用工厂方法来处理创建对象的问题，而不必指定将要创建的对象的确切类。这是通过工厂方法创建对象而不是调用构造函数来完成的。

工厂方法模式也称为虚拟构造函数模式和工厂模式。它用于抽象出对象创建的细节，并允许创建新对象而无需硬编码它们的类名。

# # 工厂方法模式是如何工作的？

工厂方法模式依赖于继承来工作。它定义了用于创建对象的接口或抽象类，以及实现接口或继承抽象类的具体子类来实际创建对象。

使用工厂方法模式创建的对象的客户端代码不需要知道或关心用于创建对象的具体类，它只需要知道接口或抽象类。

# # 何时使用工厂方法模式

工厂方法模式可用于以下情况：

- 事先不知道要创建的对象时
- 当要创建的对象需要在与使用对象不同的代码部分中创建时
- 当要创建的对象需要从直到运行时才知道的数据创建时

# # 工厂方法模式的好处

工厂方法模式具有以下优点：

- 它允许创建对象而不必硬编码它们的类名
- 它允许在代码的不同部分创建对象，而不是它们将被使用的地方
- 它允许从直到运行时才知道的数据创建对象

# # 工厂方法模式的缺点

工厂方法模式有以下缺点：

- 它会使代码更难阅读和理解
- 它可以使代码更难调试
- 它会导致大量的代码重复

# # 科特林实现

Kotlin 没有对工厂方法模式的内置支持，但可以在 Kotlin 中实现它。

在 Kotlin 中实现工厂方法模式的一种方法是使用伴随对象。伴随对象是与类关联的对象。一个类只能有一个伴随对象，反之亦然。

伴随对象可用于实现工厂方法模式，如下所示：

```kotlin
interface Shape {
    fun draw()
}

class Circle : Shape {
    override fun draw() {
        println("Circle.draw()")
    }
}

class Rectangle : Shape {
    override fun draw() {
        println("Rectangle.draw()")
    }
}

class Triangle : Shape {
    override fun draw() {
        println("Triangle.draw()")
    }
}

object ShapeFactory {
    fun getShape(shapeType: String): Shape? {
        if (shapeType == null) {
            return null
        }
        if (shapeType.equals("CIRCLE", ignoreCase = true)) {
            return Circle()
        } else if (shapeType.equals("RECTANGLE", ignoreCase = true)) {
            return Rectangle()
        } else if (shapeType.equals("TRIANGLE", ignoreCase = true)) {
            return Triangle()
        }
        return null
    }
}
```

在上面的代码中，我们定义了一个 Shape 接口和三个实现 Shape 接口的具体类。我们还定义了一个包含工厂方法 getShape() 的伴随对象 ShapeFactory。这个工厂方法接受一个字符串参数 shapeType 并返回一个 Shape 类型的对象。

我们可以使用 ShapeFactory 伴生对象，如下所示：

```kotlin
val circle = ShapeFactory.getShape("CIRCLE")
circle?.draw()

val rectangle = ShapeFactory.getShape("RECTANGLE")
rectangle?.draw()

val triangle = ShapeFactory.getShape("TRIANGLE")
triangle?.draw()
```

在上面的代码中，我们使用 ShapeFactory 伴生对象创建了三个对象，每种类型各一个。然后我们在每个对象上调用了 draw() 方法来显示它的类型。

或者，我们可以使用对象声明来实现工厂方法模式，如下所示：

```kotlin
interface Shape {
    fun draw()
}

class Circle : Shape {
    override fun draw() {
        println("Circle.draw()")
    }
}

class Rectangle : Shape {
    override fun draw() {
        println("Rectangle.draw()")
    }
}

class Triangle : Shape {
    override fun draw() {
        println("Triangle.draw()")
    }
}

object ShapeFactory {
    fun getShape(shapeType: String): Shape? {
        if (shapeType == null) {
            return null
        }
        if (shapeType.equals("CIRCLE", ignoreCase = true)) {
            return Circle()
        } else if (shapeType.equals("RECTANGLE", ignoreCase = true)) {
            return Rectangle()
        } else if (shapeType.equals("TRIANGLE", ignoreCase = true)) {
            return Triangle()
        }
        return null
    }
}

fun main(args: Array<String>) {
    val circle = ShapeFactory.getShape("CIRCLE")
    circle?.draw()

    val rectangle = ShapeFactory.getShape("RECTANGLE")
    rectangle?.draw()

    val triangle = ShapeFactory.getShape("TRIANGLE")
    triangle?.draw()
}
```

在上面的代码中，我们定义了一个包含工厂方法 getShape() 的对象声明 ShapeFactory。这个工厂方法接受一个字符串参数 shapeType 并返回一个 Shape 类型的对象。

我们可以按如下方式使用 ShapeFactory 对象：

```kotlin
val circle = ShapeFactory.getShape("CIRCLE")
circle?.draw()

val rectangle = ShapeFactory.getShape("RECTANGLE")
rectangle?.draw()

val triangle = ShapeFactory.getShape("TRIANGLE")
triangle?.draw()
```

在上面的代码中，我们使用 ShapeFactory 对象创建了三个对象，每种类型各一个。然后我们在每个对象上调用了 draw() 方法来显示它的类型。

# # 与抽象工厂模式的比较

抽象工厂模式与工厂方法模式类似，但用途不同。抽象工厂模式用于创建相关或依赖对象的系列，而工厂方法模式用于创建单个对象。

抽象工厂模式也比工厂方法模式更复杂。抽象工厂模式要求存在一个或多个具体工厂，而工厂方法模式只需要一个具体工厂。

## 结论

在本文中，我们讨论了工厂方法模式以及如何在 Kotlin 中使用它来创建对象。我们还查看了一些代码示例来演示如何在实践中使用此模式。