---
title: Kotlin에서 유형 별칭 사용
description: 
published: true
date: 2023-02-08T12:17:17.314Z
tags: 
editor: markdown
dateCreated: 2023-02-08T12:17:15.698Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Using Type Aliases in Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/using-type-aliases-in-kotlin)
{.links-list}


# Kotlin에서 유형 별칭 사용

유형 별칭은 특히 긴 제네릭 유형으로 작업할 때 코드의 가독성을 향상시키는 좋은 방법입니다. Kotlin에서는 유형 별칭을 사용하여 유형에 대한 별칭을 생성할 수 있으며, 그런 다음 원래 유형 대신 사용할 수 있습니다. 이는 코드를 훨씬 쉽게 읽고 이해할 수 있도록 일반 유형으로 작업할 때 특히 유용할 수 있습니다.

유형 별칭을 만들려면 키워드 'typealias'를 사용하고 그 뒤에 별칭 이름과 별칭을 지정하려는 유형을 사용합니다. 예를 들어, 일반 유형 `Person<T>`이 있다고 가정해 보겠습니다. 여기서 `T`는 사람 이름의 유형입니다. 다음과 같이 이 유형에 대한 유형 별칭을 만들 수 있습니다.

```kotlin
typealias PersonName = Person<String>
```

이제 코드의 모든 곳에서 `Person<String>`을 사용하는 대신 `PersonName`을 사용할 수 있습니다. 이렇게 하면 `PersonName`이 참조하는 것이 명확하므로 코드를 훨씬 쉽게 읽을 수 있습니다.

유형 별칭이 일반 유형에만 국한되지 않는다는 점도 주목할 가치가 있습니다. 일반 클래스, 인터페이스 및 기타 유형 별칭을 포함하여 모든 유형에 사용할 수 있습니다.

유형 별칭에 대한 마지막 참고 사항은 원래 유형과 상호 교환할 수 없다는 것입니다. 이는 원래 유형이 예상되는 유형 별칭을 사용할 수 없음을 의미합니다. 예를 들어 다음 코드는 컴파일되지 않습니다.

```kotlin
fun main() {
    val list: List<String> = listOf("a", "b", "c")
    val personNameList: PersonNameList = list // Error: Type mismatch
}
```

이는 `List<String>`이 `PersonNameList`와 동일한 유형이 아니기 때문입니다. 원래 유형이 예상되는 유형 별칭을 사용하려면 `inline` 키워드를 사용할 수 있습니다. 이는 이 문서의 범위를 벗어나지만 [여기](https://kotlinlang.org/docs/reference/inline-classes.html)에서 자세한 내용을 읽을 수 있습니다.

## 참조

- [Kotlin 유형 별칭](https://kotlinlang.org/docs/reference/type-aliases.html)
- [Kotlin 인라인 클래스](https://kotlinlang.org/docs/reference/inline-classes.html)