---
title: 070: Kotlin의 상태 패턴: 상태 전환으로 객체 상태 관리
description: 
published: true
date: 2023-02-14T20:17:23.987Z
tags: 
editor: markdown
dateCreated: 2023-02-14T20:17:22.216Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [070: The State Pattern in Kotlin: Managing Object States with State Transitions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/070-the-state-pattern-in-kotlin-managing-object-states-with-state-transitions)
{.links-list}


# 070: Kotlin의 상태 패턴: 상태 전환으로 객체 상태 관리

Kotlin은 개발자에게 많은 기능을 제공하는 강력한 프로그래밍 언어입니다. 그러한 기능 중 하나는 개발자가 상태 전환으로 객체 상태를 관리할 수 있게 해주는 상태 패턴입니다. 이번 포스팅에서는 state 패턴이 무엇인지, 그리고 Kotlin에서 어떻게 사용하는지 알아보겠습니다.

## 상태 패턴이란 무엇입니까?

상태 패턴은 개체 상태를 관리하는 데 도움이 되는 동작 디자인 패턴입니다. 이 패턴을 사용하면 개체는 내부 상태에 따라 동작을 변경할 수 있습니다. 이는 개체가 변화하는 조건에 따라 동작을 변경해야 할 때 유용합니다.

예를 들어 전등 스위치를 생각해 보십시오. 스위치가 "켜짐" 위치에 있으면 표시등이 켜집니다. 스위치가 "꺼짐" 위치에 있으면 표시등이 꺼집니다. 상태 패턴을 사용하여 이 동작을 모델링할 수 있습니다.

## Kotlin에서 상태 패턴을 사용하는 방법

Kotlin을 사용하면 상태 패턴을 쉽게 사용할 수 있습니다. 먼저 개체가 있을 수 있는 다양한 상태를 나타내는 봉인된 클래스를 만들어야 합니다. 전등 스위치 예제에는 "켜짐"과 "꺼짐"의 두 가지 상태가 있습니다.

```kotlin
sealed class LightSwitchState {
    object On : LightSwitchState()
    object Off : LightSwitchState()
}
```

다음으로 상태를 관리하려는 개체를 나타내는 클래스를 만들어야 합니다. 이 예에서는 전등 스위치입니다.

```kotlin
class LightSwitch {
    var state: LightSwitchState = LightSwitchState.Off
        private set

    fun turnOn() {
        state = LightSwitchState.On
    }

    fun turnOff() {
        state = LightSwitchState.Off
    }
}
```

```kotlin
val lightSwitch = LightSwitch()

lightSwitch.turnOn()
// The light is now on

lightSwitch.turnOff()
// The light is now off
```코틀린
val lightSwitch = LightSwitch()

lightSwitch.turnOn()
// 현재 불이 켜져 있습니다.

lightSwitch.turnOff()
// 이제 불이 꺼짐
```

보시다시피 상태 패턴을 사용하면 개체의 상태를 쉽게 관리할 수 있습니다. 전등 스위치 예제에서는 전등 스위치의 상태를 변경하여 전등을 쉽게 켜고 끌 수 있었습니다.

## 상태 패턴을 사용하는 경우

상태 패턴은 개체 상태를 관리하는 데 유용한 도구입니다. 그러나 이 패턴을 언제 사용해야 하는지 아는 것이 중요합니다. 상태 패턴은 다음과 같은 경우에 사용해야 합니다.

- 개체의 동작은 내부 상태에 따라 변경되어야 합니다.
- 객체는 내부 상태를 변경할 수 있어야 합니다.

전등 스위치 예제에서는 전등 스위치의 상태를 변경할 수 있어야 했기 때문에 상태 패턴을 사용했습니다. 덕분에 조명을 쉽게 켜고 끌 수 있었습니다.

## 추가 정보

상태 패턴은 개체 상태를 관리하는 데 사용할 수 있는 강력한 도구입니다. 그러나 이 패턴을 언제 사용해야 하는지 아는 것이 중요합니다. 개체의 동작이 내부 상태에 따라 변경되어야 하는 경우 상태 패턴을 사용합니다.