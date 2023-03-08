---
title: 066: Kotlin의 프로토타입 패턴: 기존 개체에서 새 개체 만들기
description: 
published: true
date: 2023-01-31T10:17:35.759Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:17:32.292Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [066: The Prototype Pattern in Kotlin: Creating New Objects from Existing Ones***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/066-the-prototype-pattern-in-kotlin-creating-new-objects-from-existing-ones)
{.links-list}


  066: Kotlin의 프로토타입 패턴: 기존 개체에서 새 개체 만들기

프로토타입 패턴은 생성할 객체의 유형이 새로운 객체를 생성하기 위해 복제되는 프로토타입 인스턴스에 의해 결정될 때 소프트웨어 개발에서 사용되는 생성 디자인 패턴입니다. 이 패턴은 다음에 사용됩니다.

- 처음부터 새 객체를 생성하는 오버헤드를 피하고,
- 개체 생성을 관리하기 위해 "팩토리" 개체가 필요하지 않습니다.
- 개체를 조립하기 위해 "빌더" 개체가 필요하지 않습니다.

프로토타입 패턴은 팩토리 메소드 및 추상 팩토리 패턴의 대안이며 종종 함께 사용됩니다.

프로토타입 패턴의 주요 이점은 생성할 객체의 정확한 유형을 지정할 필요 없이 새 객체를 생성할 수 있다는 것입니다. 이는 생성할 객체 유형을 미리 알 수 없거나 처음부터 새 객체를 생성하는 비용이 막대한 경우에 유용할 수 있습니다.

프로토타입 패턴의 주요 단점은 프로토타입에 대한 모든 변경 사항이 모든 클론에 전파되기 때문에 프로토타입을 유지 관리하고 업데이트하기 어려울 수 있다는 것입니다.

프로토타입 패턴을 사용하는 경우

프로토타입 패턴은 다음과 같은 경우에 사용해야 합니다.

- 생성할 객체의 유형을 미리 알 수 없음,
- 처음부터 새로운 객체를 생성하는 비용이 엄청나다.
- 생성할 객체의 수가 많다.

프로토타입 패턴 구현 방법

프로토타입 패턴은 다음 단계를 사용하여 Kotlin에서 구현할 수 있습니다.

1. 프로토타입을 나타내는 클래스를 만듭니다. 이 클래스에는 프로토타입의 복사본을 반환하는 clone() 메서드가 있어야 합니다.

2. 프로토타입 클래스를 확장하는 구체적인 클래스를 만듭니다.

3. 프로토타입을 인스턴스화하고 복제할 main() 메서드를 만듭니다.

4. 프로토타입에서 새 객체를 생성하고 복제본인지 확인하여 프로토타입 패턴을 테스트합니다.

다음은 Kotlin의 프로토타입 패턴의 예입니다.

```kotlin
// The Prototype class

abstract class Prototype {

abstract fun clone(): Prototype

}

// The Concrete Prototype classes

class ConcretePrototypeA: Prototype {

override fun clone(): Prototype {

return ConcretePrototypeA()

}

}

class ConcretePrototypeB: Prototype {

override fun clone(): Prototype {

return ConcretePrototypeB()

}

}

// The main() method

fun main(args: Array<String>) {

val prototypeA = ConcretePrototypeA()

val prototypeB = ConcretePrototypeB()

// Clone the prototypes

val cloneA = prototypeA.clone()

val cloneB = prototypeB.clone()

// Verify that the prototypes have been cloned

println("cloneA is a clone of prototypeA: ${cloneA === prototypeA}")

println("cloneB is a clone of prototypeB: ${cloneB === prototypeB}")

}
```

이 예제에서 Prototype 클래스는 추상 클래스이며 구체적인 클래스에 의해 구현될 clone() 메서드를 정의합니다. Concrete Prototype 클래스는 객체의 복사본을 반환하기 위해 clone() 메서드를 재정의하는 Prototype 클래스의 구체적인 하위 클래스입니다.

main() 메서드는 ConcretePrototypeA와 ConcretePrototypeB의 두 프로토타입을 인스턴스화하고 복제합니다. 그런 다음 복제본이 원본의 복사본임을 확인합니다.

프로그램의 출력은 다음과 같습니다.

```
cloneA is a clone of prototypeA: false

cloneB is a clone of prototypeB: false
```

출력에서 볼 수 있듯이 복제본은 프로토타입과 동일한 개체가 아니라 프로토타입의 복사본입니다.

프로토타입 패턴을 사용하는 경우

프로토타입 패턴은 다음과 같은 경우에 사용해야 합니다.

- 생성할 객체의 유형을 미리 알 수 없음,
- 처음부터 새로운 객체를 생성하는 비용이 엄청나다.
- 생성할 객체의 수가 많다.

프로토타입 패턴의 주요 이점은 생성할 객체의 정확한 유형을 지정할 필요 없이 새 객체를 생성할 수 있다는 것입니다. 이는 생성할 객체 유형을 미리 알 수 없거나 처음부터 새 객체를 생성하는 비용이 막대한 경우에 유용할 수 있습니다.

프로토타입 패턴의 주요 단점은 프로토타입에 대한 모든 변경 사항이 모든 클론에 전파되기 때문에 프로토타입을 유지 관리하고 업데이트하기 어려울 수 있다는 것입니다.

외부 링크

- Wikipedia의 프로토타입 패턴(https://en.wikipedia.org/wiki/Prototype_pattern)

- Java의 프로토타입 디자인 패턴(https://www.geeksforgeeks.org/prototype-design-pattern/)

- Python의 프로토타입 디자인 패턴 (https://fkhadra.github.io/2017/02/01/python-prototype/)