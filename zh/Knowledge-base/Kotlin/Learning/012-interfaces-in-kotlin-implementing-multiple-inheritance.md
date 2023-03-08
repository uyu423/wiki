---
title: 012：Kotlin 中的接口：实现多重继承
description: 
published: true
date: 2023-01-31T05:42:56.965Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:42:53.576Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [012: Interfaces in Kotlin: Implementing Multiple Inheritance***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/012-interfaces-in-kotlin-implementing-multiple-inheritance)
{.links-list}



Kotlin 是一种针对 JVM、Android、JavaScript 和 Native 的静态类型编程语言。它是一种开源、实用的语言，具有强大的功能。

Kotlin 可与现有 Java 代码互操作，使开发人员可以轻松上手。

在本文中，我们将探讨 Kotlin 的接口以及如何使用它们来实现多重继承。

## 什么是接口？

接口是一种约定，它指定类必须做什么，但不指定类如何做。

接口是 Kotlin 的一个关键特性，用于定义类必须实现的行为。

例如，假设我们有一个代表车辆的类。这个类可能有一个关于车轮数量的属性和一个驾驶功能。

```kotlin
interface Driveable {
    fun drive()
}

class Vehicle(val wheels: Int) : Driveable {
    override fun drive() {
        // drive the vehicle
    }
}
```

在上面的示例中，我们定义了一个名为 Driveable 的接口，它具有一个名为 drive() 的函数。然后我们创建了一个名为 Vehicle 的类来实现这个接口。

## 接口和继承

Kotlin 中的接口可以继承自其他接口。这允许我们创建可以在多个类中重用的复杂接口。

例如，假设我们有一个用于可以在道路上行驶的车辆的接口，以及另一个用于可以在水上行驶的车辆的接口。

```kotlin
interface Driveable {
    fun drive()
}

interface RoadVehicle : Driveable {
    fun driveOnRoad()
}

interface WaterVehicle : Driveable {
    fun driveOnWater()
}
```

在上面的示例中，我们定义了一个名为 Driveable 的接口，它具有一个名为 drive() 的函数。然后我们创建了两个继承自 Driveable 的接口，称为 RoadVehicle 和 WaterVehicle。

我们现在可以创建一个实现这两个接口的类。

```kotlin
class AmphibiousVehicle(val wheels: Int) : RoadVehicle, WaterVehicle {
    override fun drive() {
        // drive the vehicle
    }

    override fun driveOnRoad() {
        // drive on the road
    }

    override fun driveOnWater() {
        // drive on the water
    }
}
```

在上面的示例中，我们创建了一个名为 AmphibiousVehicle 的类，它同时实现了 RoadVehicle 和 WaterVehicle 接口。

这使我们能够创建可在多种情况下使用的类，而无需重复代码。

## 结论

在本文中，我们探讨了 Kotlin 的接口以及如何使用它们来实现多重继承。

接口是一种强大的工具，可用于创建复杂且可重用的代码。

如果您是 Kotlin 的新手，那么我建议您查看我们关于 Kotlin 的其他文章，以了解有关这种强大语言的更多信息。