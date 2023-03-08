---
title: Kotlin에서 람다 마스터하기
description: 
published: true
date: 2023-02-17T23:32:46.810Z
tags: 
editor: markdown
dateCreated: 2023-02-17T23:32:39.968Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Mastering Lambdas in Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/mastering-lambdas-in-kotlin)
{.links-list}


# 코틀린으로 람다 익히기

Lambda는 간결하고 효과적인 코드를 작성하는 데 도움이 되는 Kotlin의 강력한 도구입니다. 이 기사에서는 람다가 무엇인지, 어떻게 작동하는지, Kotlin 코드에서 효과적으로 사용하는 방법을 살펴보겠습니다.

## 람다는 무엇입니까?

람다는 익명 함수를 만드는 방법입니다. 함수를 다른 함수의 인수로 전달하는 방법으로 자주 사용됩니다. 예를 들어 다음 코드를 고려하십시오.

```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5)
    val doubledNumbers = numbers.map { it * 2 }
}
```

위의 코드에는 숫자 목록이 있고 원래 목록에 있는 각 숫자의 두 배를 포함하는 새 목록을 만들고 싶습니다. 숫자를 받아서 그 숫자의 두 배를 반환하는 함수를 만들어 이를 수행할 수 있습니다.

```kotlin
fun double(x: Int): Int {
    return x * 2
}
```

그런 다음 `map` 함수에서 해당 함수를 사용할 수 있습니다.

```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5)
    val doubledNumbers = numbers.map(::double)
}
```

그러나 이것은 약간 장황합니다. 람다를 사용하여 동일한 결과를 얻을 수 있습니다.

```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5)
    val doubledNumbers = numbers.map { it * 2 }
}
```

위의 코드에서 우리는 `Int`를 받아서 그 `Int`의 double을 반환하는 람다를 만들었습니다. 그런 다음 해당 람다를 `map` 함수에 전달했습니다. `map` 함수는 `number` 목록의 각 요소에 대해 람다를 호출하고 결과와 함께 새 목록을 반환합니다.

보시다시피 람다는 코드를 작성하는 간결하고 효과적인 방법이 될 수 있습니다.

## 람다는 어떻게 작동합니까?

람다는 익명 함수입니다. 즉, 이름이 없는 함수입니다.

람다는 종종 다른 함수에 인수로 전달될 함수를 만드는 데 사용됩니다. 이전 섹션에서 `map` 함수에 람다를 전달했을 때 이에 대한 예를 보았습니다.

람다는 두 가지 방법으로 만들 수 있습니다.

* 함수 본문으로
* 표현으로

### 함수 본문이 있는 람다

함수 본문이 있는 람다는 `{}` 구문을 사용하여 정의됩니다. 예를 들어, 다음은 `Int`를 사용하고 해당 `Int`의 double을 반환하는 람다입니다.

```kotlin
val lambda = { x: Int ->
    x * 2
}
```

위의 코드에서 우리는 `Int`를 받아서 그 `Int`의 double을 반환하는 람다를 정의했습니다. 그런 다음 다음과 같이 람다를 호출할 수 있습니다.

```kotlin
val result = lambda(2)
```

위의 코드에서 `Int` `2`로 람다를 호출하고 결과를 `result` 변수에 저장했습니다.

### 표현식이 있는 람다

표현식이 있는 람다는 `=` 구문을 사용하여 정의됩니다. 예를 들어, 다음은 `Int`를 사용하고 해당 `Int`의 double을 반환하는 람다입니다.

```kotlin
val lambda = { x: Int ->
    x * 2
}
```

위의 코드에서 우리는 `Int`를 받아서 그 `Int`의 double을 반환하는 람다를 정의했습니다. 그런 다음 다음과 같이 람다를 호출할 수 있습니다.

```kotlin
val result = lambda(2)
```

위의 코드에서 `Int` `2`로 람다를 호출하고 결과를 `result` 변수에 저장했습니다.

## 람다 사용 방법

이제 람다가 무엇이고 어떻게 작동하는지 살펴보았으므로 코드에서 효과적으로 사용하는 방법을 살펴보겠습니다.

### 단일 매개변수가 있는 람다

단일 매개변수가 있는 람다는 `it` 키워드를 사용하여 정의할 수 있습니다. 예를 들어 다음은 `String`을 사용하여 해당 `String`의 길이를 반환하는 람다입니다.

```kotlin
val lambda = { it: String ->
    it.length
}
```

위의 코드에서 우리는 `String`을 사용하여 해당 `String`의 길이를 반환하는 람다를 정의했습니다. 그런 다음 다음과 같이 람다를 호출할 수 있습니다.

```kotlin
val result = lambda("Hello, world!")
```

위의 코드에서 `String` `"Hello, world!"`을 사용하여 람다를 호출하고 결과를 `result` 변수에 저장했습니다.

### 여러 매개변수가 있는 람다

매개변수가 여러 개인 Lambda는 매개변수 이름을 사용하여 정의됩니다. 예를 들어, 다음은 두 개의 `Int`를 사용하고 해당 `Int`의 합계를 반환하는 람다입니다.

```kotlin
val lambda = { x: Int, y: Int ->
    x + y
}
```

위의 코드에서 우리는 두 개의 `Int`를 취하고 그 `Int`의 합을 반환하는 람다를 정의했습니다. 그런 다음 다음과 같이 람다를 호출할 수 있습니다.

```kotlin
val result = lambda(1, 2)
```

위의 코드에서 `Int`의 `1` 및 `2`로 람다를 호출하고 결과를 `result` 변수에 저장했습니다.

### 매개변수가 없는 람다

매개변수가 없는 람다는 `()` 구문을 사용하여 정의됩니다. 예를 들어 다음은 `"Hello, world!"` 문자열을 반환하는 람다입니다.

```kotlin
val lambda = {
    "Hello, world!"
}
```

위의 코드에서 `"Hello, world!"` 문자열을 반환하는 람다를 정의했습니다. 그런 다음 다음과 같이 람다를 호출할 수 있습니다.

```kotlin
val result = lambda()
```

위의 코드에서 우리는 람다를 호출하고 결과를 `result` 변수에 저장했습니다.

## 결론

Lambda는 간결하고 효과적인 코드를 작성하는 데 도움이 되는 Kotlin의 강력한 도구입니다. 이 기사에서는 람다가 무엇인지, 어떻게 작동하는지, 코드에서 효과적으로 사용하는 방법을 살펴보았습니다.