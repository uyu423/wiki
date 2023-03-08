---
title: 023: Kotlin의 유형 별칭: 긴 클래스 이름 단축
description: 
published: true
date: 2023-02-01T20:17:28.187Z
tags: 
editor: markdown
dateCreated: 2023-02-01T20:17:24.105Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [023: Type Aliases in Kotlin: Shortening Long Class Names***English** document is available*](/en/Knowledge-base/Kotlin/Learning/023-type-aliases-in-kotlin-shortening-long-class-names)
{.links-list}


# 023: Kotlin의 유형 별칭: 긴 클래스 이름 단축

Kotlin에는 긴 클래스 이름을 줄이는 데 사용할 수 있는 유형 별칭이라는 훌륭한 기능이 있습니다. 예를 들어 다음 클래스 이름을 고려하십시오.

```kotlin
class MyVeryLongClassName {
    // ...
}
```

이 클래스 이름은 꽤 긴데 줄여서 쓰면 좋을 것 같습니다. 유형 별칭을 사용하여 이를 수행할 수 있습니다.

```kotlin
typealias MyClass = MyVeryLongClassName

class MyClass {
    // ...
}
```

이제 `MyClass` 별칭은 긴 클래스 이름 대신 코드의 어디에서나 사용할 수 있습니다. 이는 제네릭 형식으로 작업할 때 특히 유용합니다.

```kotlin
typealias MyClass = MyVeryLongClassName

class MyClass<T> {
    // ...
}

fun main() {
    val myClass: MyClass<String> = MyClass()
}
```

위의 예에서 `MyVeryLongClassName` 클래스에 대한 유형 별칭을 정의했습니다. 그런 다음 제네릭 형식의 변수를 선언할 때 이 별칭을 사용할 수 있습니다. 이렇게 하면 코드를 훨씬 더 쉽게 읽고 이해할 수 있습니다.

유형 별칭을 사용할 때 염두에 두어야 할 몇 가지 사항이 있습니다.

- 유형 별칭은 클래스와 동일하지 않습니다. 유형에 다른 이름을 지정하는 방법일 뿐입니다.
- 유형 별칭은 새 유형을 만드는 데 사용할 수 없습니다. 기존 유형에 새 이름을 지정하는 데만 사용할 수 있습니다.
- 유형 별칭은 변수 유형을 변경하는 데 사용할 수 없습니다. 새 변수를 선언할 때만 사용할 수 있습니다.

전반적으로 유형 별칭은 긴 클래스 이름을 줄이고 코드를 더 읽기 쉽게 만드는 좋은 방법입니다. 제네릭 형식으로 작업할 때 특히 유용합니다.