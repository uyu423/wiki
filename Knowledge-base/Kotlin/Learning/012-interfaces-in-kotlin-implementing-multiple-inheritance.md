---
title: 012: Kotlin의 인터페이스: 다중 상속 구현
description: 
published: true
date: 2023-01-31T05:42:56.965Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:42:53.573Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [012: Interfaces in Kotlin: Implementing Multiple Inheritance***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/012-interfaces-in-kotlin-implementing-multiple-inheritance)
{.links-list}



Kotlin은 JVM, Android, JavaScript 및 Native를 대상으로 하는 정적 유형 프로그래밍 언어입니다. 강력한 기능을 갖춘 실용적인 오픈 소스 언어입니다.

Kotlin은 기존 Java 코드와 상호 운용 가능하므로 개발자가 쉽게 시작할 수 있습니다.

이 기사에서는 Kotlin의 인터페이스와 이를 사용하여 다중 상속을 구현하는 방법을 살펴봅니다.

## 인터페이스란?

인터페이스는 클래스가 수행해야 하는 작업을 지정하는 계약이지만 클래스가 수행하는 방법은 지정하지 않습니다.

인터페이스는 Kotlin의 핵심 기능이며 클래스가 구현해야 하는 동작을 정의하는 데 사용됩니다.

예를 들어 차량을 나타내는 클래스가 있다고 가정해 보겠습니다. 이 클래스는 바퀴 수에 대한 속성과 구동 기능을 가질 수 있습니다.

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

위의 예에서 우리는 drive()라는 단일 함수가 있는 Driveable이라는 인터페이스를 정의했습니다. 그런 다음 이 인터페이스를 구현하는 Vehicle이라는 클래스를 만들었습니다.

## 인터페이스와 상속

Kotlin의 인터페이스는 다른 인터페이스에서 상속할 수 있습니다. 이를 통해 여러 클래스에서 재사용할 수 있는 복잡한 인터페이스를 만들 수 있습니다.

예를 들어 도로에서 운전할 수 있는 차량용 인터페이스와 물 위에서 운전할 수 있는 차량용 인터페이스가 있다고 가정해 보겠습니다.

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

위의 예에서 우리는 drive()라는 단일 함수가 있는 Driveable이라는 인터페이스를 정의했습니다. 그런 다음 Driveable에서 상속되는 RoadVehicle 및 WaterVehicle이라는 두 개의 인터페이스를 만들었습니다.

이제 이러한 인터페이스를 모두 구현하는 클래스를 만들 수 있습니다.

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

위의 예에서는 RoadVehicle 및 WaterVehicle 인터페이스를 모두 구현하는 AmphibiousVehicle이라는 클래스를 만들었습니다.

이를 통해 코드를 복제하지 않고도 여러 상황에서 사용할 수 있는 클래스를 만들 수 있습니다.

## 결론

이 기사에서는 Kotlin의 인터페이스와 이를 사용하여 다중 상속을 구현하는 방법을 살펴보았습니다.

인터페이스는 복잡하고 재사용 가능한 코드를 만드는 데 사용할 수 있는 강력한 도구입니다.

Kotlin을 처음 사용하는 경우 Kotlin에 대한 다른 문서를 확인하여 이 강력한 언어에 대해 자세히 알아보는 것이 좋습니다.