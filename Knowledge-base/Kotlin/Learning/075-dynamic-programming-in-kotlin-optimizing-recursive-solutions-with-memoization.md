---
title: 075: Kotlin의 동적 프로그래밍: 메모이제이션으로 재귀 솔루션 최적화
description: 
published: true
date: 2023-01-31T18:04:34.440Z
tags: 
editor: markdown
dateCreated: 2023-01-31T18:04:32.799Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [075: Dynamic Programming in Kotlin: Optimizing Recursive Solutions with Memoization***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/075-dynamic-programming-in-kotlin-optimizing-recursive-solutions-with-memoization)
{.links-list}



# 075: Kotlin의 동적 프로그래밍: 메모이제이션으로 재귀 솔루션 최적화

동적 프로그래밍은 복잡한 문제를 더 작고 단순한 하위 문제로 분해하여 해결하는 강력한 기술입니다. 하위 문제의 결과를 다시 계산하는 대신 재사용할 수 있도록 저장하여 재귀 솔루션을 최적화하는 데 사용할 수 있습니다.

이 기사에서는 동적 프로그래밍을 사용하여 Kotlin에서 재귀 솔루션을 최적화하는 방법을 알아봅니다. 기술을 설명하기 위해 간단한 예제로 시작한 다음 더 복잡한 문제에 적용할 것입니다.

## 간단한 예

n 번째 피보나치 수를 계산하고 싶다고 가정합니다. 다음 코드를 사용하여 재귀적으로 이 작업을 수행할 수 있습니다.

```kotlin
fun fib(n: Int): Int {
    if (n <= 1) return n
    return fib(n - 1) + fib(n - 2)
}
```

그러나 이 코드는 하위 문제의 결과를 다시 계산하기 때문에 매우 비효율적입니다. 예를 들어 `fib(5)`를 계산할 때 `fib(4)` 및 `fib(3)`을 두 번 계산합니다.

![피보나치 계산](fibonacci.png)

동적 프로그래밍을 사용하여 하위 문제의 결과를 재사용할 수 있도록 저장하여 이 코드를 최적화할 수 있습니다. 이미 계산된 피보나치 수를 추적하기 위해 배열을 사용하여 이를 수행할 수 있습니다.

```kotlin
fun fib(n: Int): Int {
    if (n <= 1) return n
    val fibs = IntArray(n + 1)
    fibs[0] = 0
    fibs[1] = 1
    for (i in 2..n) {
        fibs[i] = fibs[i - 1] + fibs[i - 2]
    }
    return fibs[n]
}
```

이제 `fib(5)`를 계산할 때 `fib(4)` 및 `fib(3)`의 결과를 재사용할 수 있습니다.

![메모이제이션을 사용한 피보나치 계산](fibonacci-memoized.png)

이 코드는 하위 문제의 결과를 다시 계산할 필요가 없기 때문에 훨씬 더 효율적입니다.

## 좀 더 복잡한 예

이제 더 복잡한 문제인 배낭 문제에 동적 프로그래밍을 적용해 보겠습니다. 배낭 문제에서 우리는 각각 무게와 가치를 가진 일련의 항목을 받았습니다. 우리의 목표는 주어진 무게 제한을 유지하면서 총 가치를 최대화하는 항목의 하위 집합을 선택하는 것입니다.

예를 들어 다음 항목이 있다고 가정합니다.

| 항목 | 무게 | 가치 |
| --- | --- | --- |
| A | 2 | 6 |
| 비 | 2 | 10 |
| 씨 | 3 | 12 |

그리고 총 가중치가 5 이하이고 총 가치를 최대화하는 항목의 하위 집합을 찾고자 합니다. 이 경우 최적의 솔루션은 총 가중치가 5이고 총 값이 18인 항목 A와 C를 선택하는 것입니다.

동적 프로그래밍을 사용하여 배낭 문제를 해결할 수 있습니다. 배열을 사용하여 무게 제한까지 각 무게에 대해 달성할 수 있는 최대값을 추적합니다.

```kotlin
fun knapsack(items: Array<Item>, weightLimit: Int): Int {
    val values = IntArray(weightLimit + 1)
    for (i in items.indices) {
        val item = items[i]
        for (w in weightLimit downTo item.weight) {
            values[w] = max(values[w], values[w - item.weight] + item.value)
        }
    }
    return values[weightLimit]
}
```

이 코드에서 `values[w]`는 `w` 이하의 가중치로 얻을 수 있는 최대값을 나타냅니다. 각 항목을 차례로 고려하고 배낭에 추가할 가치가 있는지 확인하여 이 값을 계산합니다. 그렇다면 이에 따라 `values[w]`를 업데이트합니다.

예를 들어 가중치가 2이고 값이 6인 항목 A를 고려하고 있다고 가정합니다. `values[2]`를 6(항목 A의 값)으로 업데이트하고 `values[3]`을 8(항목 A의 값 + 가중치 1)로 얻을 수 있는 최상의 값입니다.

![배낭 계산](knapsack.png)

모든 항목을 고려할 때까지 이 프로세스를 계속합니다. 마지막으로 `values[weightLimit]`에는 `weightLimit` 이하의 가중치로 달성할 수 있는 최대값이 포함됩니다.

## 결론

이 기사에서는 동적 프로그래밍을 사용하여 Kotlin에서 재귀 솔루션을 최적화하는 방법을 배웠습니다. 우리는 메모이제이션을 사용하여 하위 문제의 결과를 저장하여 재사용할 수 있도록 하는 방법을 보았고 이 기술을 배낭 문제에 적용했습니다.