---
title: 077: Kotlin의 Memento 패턴: 향후 복원을 위해 객체 상태 보존
description: 
published: true
date: 2023-02-16T22:55:28.572Z
tags: 
editor: markdown
dateCreated: 2023-02-16T22:55:26.913Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [077: The Memento Pattern in Kotlin: Preserving Object States for Future Restoration***English** document is available*](/en/Knowledge-base/Kotlin/Learning/077-the-memento-pattern-in-kotlin-preserving-object-states-for-future-restoration)
{.links-list}


# Kotlin의 Memento 패턴: 향후 복원을 위해 객체 상태 보존

메멘토 패턴은 객체의 상태를 저장하고 복원하는 기능을 제공하는 소프트웨어 설계 패턴입니다. 종종 실행 취소/다시 실행 작업과 함께 사용됩니다.

memento 패턴은 originator, caretaker, memento로 구성된 3계층 구조입니다.

발신자는 상태를 저장해야 하는 객체입니다. 케어테이커는 발신자의 상태를 저장하고 복원하는 일을 담당하는 객체입니다. memento는 작성자의 상태를 저장하는 불변 객체입니다.

memento 패턴은 다음과 같은 용도로 사용됩니다.

- 개체의 상태 저장 및 복원
- 객체의 속성 상태 저장 및 복원
- 개체 연결 상태 저장 및 복원

## Kotlin에서 Memento 패턴 구현

Kotlin에서 memento 패턴을 구현하는 방법에는 두 가지가 있습니다.

- 데이터 클래스 사용
- 봉인 클래스 사용

### 데이터 클래스 사용

데이터 클래스는 데이터를 보유하도록 설계된 클래스입니다. 데이터 클래스에는 memento 패턴을 구현하는 데 이상적인 여러 기능이 있습니다.

- 데이터 클래스는 변경할 수 없습니다.
- 데이터 클래스에는 `복사` 방법이 있습니다.
- 데이터 클래스는 `data` 키워드를 사용하여 선언할 수 있습니다.

데이터 클래스를 사용하여 memento 패턴을 구현하려면 `Originator` 클래스의 상태를 저장하는 `Memento` 클래스를 만들어야 합니다. `Originator` 클래스에는 `Memento` 오브젝트를 생성하는 `createMemento` 메소드와 `Memento` 오브젝트에서 `Originator`의 상태를 복원하는 `restoreMemento` 메소드가 있습니다.

다음은 데이터 클래스를 사용하여 memento 패턴을 구현하는 방법의 예입니다.

```kotlin
data class Originator(var state: String) {
  
  fun createMemento(): Memento {
    return Memento(state)
  }
  
  fun restoreMemento(memento: Memento) {
    state = memento.state
  }
  
  data class Memento(val state: String)
}
```

### 봉인된 클래스 사용

봉인된 클래스는 하나 이상의 하위 클래스를 가질 수 있는 클래스입니다. Sealed 클래스는 다음과 같은 이유로 memento 패턴을 구현하는 데 이상적입니다.

- `sealed` 키워드를 사용하여 선언 가능
- 하위 클래스를 가질 수 있음
- '추상'으로 선언 가능

봉인된 클래스를 사용하여 메멘토 패턴을 구현하려면 `Originator`의 각 상태에 대한 하위 클래스가 있는 `Memento` 봉인된 클래스를 만들어야 합니다. `Originator` 클래스에는 `Memento` 오브젝트를 생성하는 `createMemento` 메소드와 `Memento` 오브젝트에서 `Originator`의 상태를 복원하는 `restoreMemento` 메소드가 있습니다.

다음은 봉인된 클래스를 사용하여 memento 패턴을 구현하는 방법의 예입니다.

```kotlin
sealed class Memento

class Originator(var state: String) {
  
  fun createMemento(): Memento {
    return when (state) {
      "state1" -> State1()
      "state2" -> State2()
      else -> throw IllegalArgumentException("Invalid state")
    }
  }
  
  fun restoreMemento(memento: Memento) {
    state = when (memento) {
      is State1 -> "state1"
      is State2 -> "state2"
      else -> throw IllegalArgumentException("Invalid memento")
    }
  }
  
  class State1 : Memento
  class State2 : Memento
}
```

## 결론

이 글에서는 메멘토 패턴에 대해 알아보고 데이터 클래스와 봉인된 클래스를 사용하여 코틀린에서 구현하는 방법에 대해 알아보았습니다.