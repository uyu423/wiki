---
title: 043: Kotlin의 중첩 및 내부 클래스: 클래스 내에 클래스 만들기
description: 
published: true
date: 2023-02-16T13:32:30.824Z
tags: 
editor: markdown
dateCreated: 2023-02-16T13:32:29.311Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [043: Nested and Inner Classes in Kotlin: Creating Classes within Classes***English** document is available*](/en/Knowledge-base/Kotlin/Learning/043-nested-and-inner-classes-in-kotlin-creating-classes-within-classes)
{.links-list}


# 043: Kotlin의 중첩 및 내부 클래스: 클래스 내에 클래스 만들기

Kotlin은 다른 클래스 내에서 만들 수 있는 중첩 클래스와 내부 클래스라는 두 가지 유형의 클래스를 지원합니다. 이번 포스트에서는 Kotlin에서 중첩 클래스와 내부 클래스의 차이점과 각 유형의 클래스를 만드는 방법을 살펴보겠습니다.

## 중첩 클래스

중첩 클래스는 다른 클래스 내에 정의된 클래스입니다. 중첩 클래스는 자신이 정의된 클래스의 멤버가 아닙니다. 그들은 단순히 다른 클래스 내에서 정의된 클래스입니다.

다음은 Kotlin의 중첩 클래스 예입니다.

```kotlin
class OuterClass {
    class NestedClass {
        // ...
    }
}
```

위의 예에서 `NestedClass`는 `OuterClass`의 구성원이 아닙니다. 단순히 `OuterClass` 내에 정의된 클래스입니다.

중첩 클래스는 관련 클래스를 함께 그룹화하는 데 사용할 수 있습니다. 예를 들어 자동차를 나타내는 클래스가 있는 경우 자동차 엔진을 나타내는 중첩 클래스를 만들 수 있습니다.

중첩 클래스를 사용하여 클래스의 정적 멤버를 만들 수도 있습니다. 아래 예에서 `NestedClass`에는 `foo`라는 정적 멤버가 있습니다.

```kotlin
class OuterClass {
    class NestedClass {
        companion object {
            val foo = "bar"
        }
    }
}
```

위의 예에서 `NestedClass`에는 `foo`라는 정적 멤버가 있습니다. 이는 `OuterClass` 인스턴스 없이 `NestedClass`에 액세스할 수 있음을 의미합니다.

## 내부 클래스

내부 클래스는 다른 클래스 내에서 정의되고 해당 클래스의 구성원인 클래스입니다. 내부 클래스는 자신이 정의된 클래스의 멤버에 액세스할 수 있습니다.

다음은 Kotlin의 내부 클래스 예입니다.

```kotlin
class OuterClass {
    inner class InnerClass {
        // ...
    }
}
```

위의 예에서 `InnerClass`는 `OuterClass`의 멤버입니다. 이는 `InnerClass`가 `OuterClass`의 구성원에 액세스할 수 있음을 의미합니다.

내부 클래스는 클래스의 특정 인스턴스와 연결된 개체를 만드는 데 사용할 수 있습니다. 예를 들어 자동차를 나타내는 클래스가 있는 경우 자동차 엔진을 나타내는 내부 클래스를 만들 수 있습니다.

내부 클래스를 사용하여 익명 클래스를 만들 수도 있습니다. 익명 클래스는 이름 없이 정의된 클래스입니다. 익명 클래스는 클래스의 특정 인스턴스와 연결되지 않은 개체를 만드는 데 유용합니다.

다음은 Kotlin의 익명 내부 클래스의 예입니다.

```kotlin
class OuterClass {
    val anonymousInnerClass = object: SomeType {
        // ...
    }
}
```

위의 예에서는 `SomeType` 인터페이스를 구현하는 익명 내부 클래스가 생성됩니다.

## 결론

이 게시물에서는 Kotlin의 중첩 클래스와 내부 클래스의 차이점을 살펴보았습니다. 또한 각 유형의 클래스를 만드는 방법도 살펴보았습니다.