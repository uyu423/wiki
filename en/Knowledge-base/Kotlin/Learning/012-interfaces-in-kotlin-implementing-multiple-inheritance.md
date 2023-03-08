---
title: 012: Interfaces in Kotlin: Implementing Multiple Inheritance
description: 
published: true
date: 2023-01-31T05:42:55.217Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:42:53.572Z
---

- [012: Kotlin의 인터페이스: 다중 상속 구현***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/012-interfaces-in-kotlin-implementing-multiple-inheritance)
{.links-list}
- [012: Kotlin のインターフェイス: 多重継承の実装***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/012-interfaces-in-kotlin-implementing-multiple-inheritance)
{.links-list}
- [012：Kotlin 中的接口：实现多重继承***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/012-interfaces-in-kotlin-implementing-multiple-inheritance)
{.links-list}



Kotlin is a statically typed programming language that targets the JVM, Android, JavaScript, and Native. It is an open-source, pragmatic language with powerful features.   

Kotlin is interoperable with existing Java code, making it easy for developers to get started with it.   

In this article, we will explore Kotlin's interfaces and how they can be used to implement multiple inheritance.   

## What is an Interface?

An interface is a contract that specifies what a class must do, but it does not specify how the class does it.   

Interfaces are a key feature of Kotlin and are used to define behavior that a class must implement.   

For example, let's say we have a class that represents a vehicle. This class might have a property for the number of wheels and a function for driving.   

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

In the example above, we have defined an interface called Driveable that has a single function called drive(). We have then created a class called Vehicle that implements this interface.   

## Interfaces and Inheritance

Interfaces in Kotlin can inherit from other interfaces. This allows us to create complex interfaces that can be reused in multiple classes.   

For example, let's say we have an interface for a vehicle that can be driven on the road, and another interface for a vehicle that can be driven on the water.   

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

In the example above, we have defined an interface called Driveable that has a single function called drive(). We have then created two interfaces that inherit from Driveable, called RoadVehicle and WaterVehicle.   

We can now create a class that implements both of these interfaces.   

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

In the example above, we have created a class called AmphibiousVehicle that implements both the RoadVehicle and WaterVehicle interfaces.   

This allows us to create classes that can be used in multiple situations, without having to duplicate code.   

## Conclusion

In this article, we have explored Kotlin's interfaces and how they can be used to implement multiple inheritance.   

Interfaces are a powerful tool that can be used to create complex and reusable code.   

If you are new to Kotlin, then I recommend you check out our other articles on Kotlin to learn more about this powerful language.