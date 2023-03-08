---
title: 035: Kotlin의 Tailrec 함수: 재귀 함수 최적화
description: 
published: true
date: 2023-02-16T09:32:34.425Z
tags: 
editor: markdown
dateCreated: 2023-02-16T09:32:26.413Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [035: Tailrec Functions in Kotlin: Optimizing Recursive Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/035-tailrec-functions-in-kotlin-optimizing-recursive-functions)
{.links-list}


# 035: Kotlin의 Tailrec 함수: 재귀 함수 최적화

이번 포스팅에서는 Kotlin에서 tailrec 함수를 사용하여 재귀 함수를 최적화하는 방법을 살펴보겠습니다.

재귀 함수는 직접 또는 간접적으로 자신을 호출하는 함수입니다. tailrec 함수는 함수의 마지막 명령문이 재귀 호출인 특별한 유형의 재귀 함수입니다.

Tailrec 함수는 여러 함수를 호출하는 대신 루프를 사용하도록 컴파일되기 때문에 일반 재귀 함수보다 효율적입니다. 이는 특히 여러 번 호출되는 재귀 함수의 경우 상당한 성능 향상을 가져올 수 있습니다.

Kotlin에서 tailrec 함수를 만들려면 함수 이름 앞에 tailrec 키워드를 사용합니다. 예를 들어 다음은 주어진 숫자의 계승을 계산하는 tailrec 함수입니다.

```kotlin
tailrec fun factorial(n: Int, result: Int = 1): Int {
    if (n == 1) return result
    return factorial(n - 1, n * result)
}
```

이 예에서는 fun 키워드 앞에 tailrec 키워드를 사용하고 있습니다. 또한 함수의 반환 유형(Int)을 지정하고 함수에 n과 결과라는 두 개의 매개변수를 지정했습니다.

결과 매개변수의 기본값은 1이며 함수가 처음 호출될 때 사용됩니다.

함수는 n 값이 1이 될 때까지 재귀적으로 자신을 호출합니다. 그 시점에서 함수는 결과 값을 반환합니다.

다른 값으로 호출하여 이 함수가 어떻게 작동하는지 확인할 수 있습니다.

```kotlin
factorial(5) // 120
factorial(10) // 3628800
```

보시다시피 tailrec 함수는 숫자의 계승을 계산하는 더 효율적인 방법입니다.

tailrec 함수에는 몇 가지 제한 사항이 있습니다.

- 함수는 클래스 또는 객체의 멤버여야 합니다.
- 함수는 tailrec 키워드로 표시되어야 합니다.
- 함수는 단일 매개변수를 가져야 합니다.
- 함수는 재귀적으로 자신을 호출해야 합니다.
- 함수는 매개변수와 동일한 유형을 반환해야 합니다.

이러한 기준을 충족하지 않는 tailrec 함수를 만들려고 하면 컴파일러 오류가 발생합니다.

## 추가 정보

다음은 도움이 될 수 있는 몇 가지 추가 리소스입니다.

- [코틀린의 꼬리 재귀](https://kotlinlang.org/docs/reference/tail-recursion.html)
- [Kotlin의 꼬리 호출 최적화](https://kotlinlang.org/docs/reference/tail-call-optimization.html)