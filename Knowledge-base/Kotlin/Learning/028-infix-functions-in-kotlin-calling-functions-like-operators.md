---
title: 028: Kotlin의 중위 함수: 연산자와 같은 함수 호출
description: 
published: true
date: 2023-02-01T17:23:30.437Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:23:28.850Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [028: Infix Functions in Kotlin: Calling Functions Like Operators***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/028-infix-functions-in-kotlin-calling-functions-like-operators)
{.links-list}



#028: Kotlin의 중위 함수: 연산자와 같은 함수 호출
Kotlin은 JVM, Android 및 브라우저용 정적 유형 프로그래밍 언어입니다. 상호 운용성, 안전성, 도구 지원 및 간결한 구문으로 유명합니다.

Kotlin에는 고유하고 개발자에게 매력적인 여러 기능이 있으며 그 중 하나는 중위 함수입니다.

중위 함수는 일반적인 점 표기법을 사용하지 않고 호출할 수 있는 함수입니다. 즉, 코드를 더 간결하고 읽기 쉽게 만들 수 있는 연산자처럼 호출할 수 있습니다.

중위 함수는 infix 키워드로 표시됩니다. 멤버 함수 또는 확장 함수여야 합니다. 하나의 매개변수만 가질 수 있습니다.

다음은 중위 함수의 간단한 예입니다.

```kotlin
infix fun Int.times(str: String) = str.repeat(this)

println(2 times "Bye ") // Prints "Bye Bye "
```

위의 예에서 `times` 함수는 `2` 및 `"Bye "` 매개변수와 함께 호출됩니다. `times` 함수는 `2`번 반복된 `"Bye "` 문자열을 반환합니다.

중위 함수는 코드를 더 읽기 쉽게 만드는 데 매우 유용할 수 있습니다. 예를 들어 `+` 연산자는 문자열을 연결하는 데 자주 사용됩니다. 그러나 추가에도 사용할 수 있습니다. Kotlin에 익숙하지 않은 개발자에게는 혼란스러울 수 있습니다.

중위 함수를 사용하면 문자열 연결을 위한 자체 `+` 연산자를 정의할 수 있으므로 코드를 더 읽기 쉽게 만들 수 있습니다.

```kotlin
infix fun String.plus(str: String) = this + str

println("Hello" plus " world") // Prints "Hello world"
```

위의 예에서 문자열 연결을 위한 중위 함수를 정의했습니다. 이제 `+` 연산자를 사용하여 두 문자열을 연결할 수 있습니다. 이렇게 하면 코드를 더 읽기 쉽고 간결하게 만들 수 있습니다.

중위 함수도 비교에 사용할 수 있습니다. 예를 들어 `compareTo` 함수를 사용하여 두 문자열을 비교할 수 있습니다.

```kotlin
infix fun String.compareTo(str: String) = this.compareTo(str)

println("a" compareTo "b") // Prints -1
println("b" compareTo "a") // Prints 1
println("a" compareTo "a") // Prints 0
```

위의 예에서 문자열 비교를 위한 중위 함수를 정의했습니다. 이제 `compareTo` 함수를 사용하여 두 문자열을 비교할 수 있습니다. 이렇게 하면 코드를 더 읽기 쉽고 간결하게 만들 수 있습니다.

중위 함수는 Kotlin 코드를 더 읽기 쉽고 간결하게 만들 수 있는 강력한 도구입니다. 그러나 과도하게 사용하면 코드 가독성이 떨어질 수 있으므로 주의해서 사용해야 합니다.