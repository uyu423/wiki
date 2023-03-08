---
title: 코틀린 특징
description: 
published: true
date: 2023-02-17T18:00:06.759Z
tags: kotlin
editor: markdown
dateCreated: 2022-12-23T04:35:18.925Z
---

- [Features of Kotlin***English** version of this document is available*](/en/dev/Kotlin/feature-of-kotlin)
{.links-list}

Kotlin과 Java는 모두 다양한 애플리케이션을 구축하는 데 사용되는 널리 사용되는 프로그래밍 언어입니다. 각 언어는 유사점을 가지고 있지만 두 언어 사이에는 몇 가지 중요한 차이점도 있습니다. 다음은 Kotlin과 Java의 주요 기능을 비교한 것입니다.

### 구문 (Syntax)

- Kotlin은 Java보다 간결하고 표현력이 풍부한 구문을 가지고 있어 읽고 쓰기가 더 쉽습니다. Kotlin에는 유형 추론, 간소화된 반환 구문, 데이터 클래스 지원과 같은 기능이 있어 필요한 상용구 코드의 양을 줄여줍니다.

- 클래스 멤버의 접근을 제어하기 위한 `public`, `private` 및 `protected` 키워드가 없습니다. 대신 `internal`, `private` 및 `protected` 키워드를 사용하며 기본 접근 제어는 `public`입니다.

- 함수가 값을 반환하지 않음을 나타내는 `void` 키워드가 없습니다. 대신 Unit type을 사용하거나 함수가 값을 반환하지 않는 경우 반환 유형을 완전히 생략할 수 있습니다.

- 객체 생성을 위한 `new` 키워드가 없습니다. 대신 객체 키워드 또는 생성자 키워드를 사용하여 클래스의 인스턴스를 만들 수 있습니다.

- 클래스, 함수 및 변수를 정의하기 위한 보다 간결한 구문이 있습니다. 예를 들어 다음과 같이 한 줄의 코드에서 기본 생성자와 필드 선언을 사용하여 클래스를 정의할 수 있습니다.

```kt
class User(val name: String, val age: Int)
```

- 반복문 및 제어 흐름에 대해 보다 표현력이 풍부한 구문을 제공합니다. 예를 들어 `switch` 문에 대한 간결한 대안으로 `when` 식을 사용할 수 있으며 for 루프를 사용하여 범위 및 컬렉션을 반복할 수 있습니다.

```kt
val x = 10
when (x) {
    0 -> print("x is zero")
    in 1..9 -> print("x is between 1 and 9")
    else -> print("x is something else")
}
```

```kt
for (i in 1..10) {
    print(i)
}

val names = listOf("Alice", "Bob", "Charlie")
for (name in names) {
    print(name)
}
```

- Java에 비해 익명 클래스를 만들기 간결합니다. `new` 키워드와 `implements` 또는 `extends` 키워드를 사용하는 대신 람다 식이나 함수 참조를 사용하여 인터페이스나 클래스의 인스턴스를 만들 수 있습니다.

### Null로 부터 안전 (Null safety)

- Kotlin은 `null safety`을 기본적으로 지원하므로 null을 허용하는 유형과 null을 허용하지 않는 유형을 구분할 수 있습니다. 이는 Java에서 흔히 발생하는 null 참조 예외(`NullPointException`)를 방지하는 데 도움이 됩니다. 다음은 Kotlin에서 `nullable` 변수를 선언하는 방법의 예입니다.

```kt
val name: String? = null
```

- Java에서는 `javax.annotation` 패키지의 `@Nullable` 및 `@NotNull` 주석을 사용하여 유사한 효과를 얻을 수 있지만 언어에 내장되어 있지는 않습니다.

### 데이터 클래스

- Kotlin에는 추가적인 논리 로직 없이 데이터를 저장하는 클래스인 데이터 클래스를 정의하기 위한 간결한 구문이 있습니다. Kotlin에서는 다음과 같이 데이터 클래스를 정의할 수 있습니다.

```kt
data class User(val name: String, val age: Int)
```

- Java에서는 동일한 효과를 얻기 위해 훨씬 더 많은 코드를 작성해야 합니다. 클래스와 필드를 정의 한 후, `getter` 및 `setter`를 추가하고 `equals()`, `hashCode()` 및 `toString()` 메서드를 재정의(Override)해야 합니다.

### 확장 함수

- Kotlin을 사용하면 기존 클래스에서 상속하거나 데코레이터와 같은 디자인 패턴을 사용하지 않고도 기존 클래스에 새로운 함수을 추가할 수 있습니다. 이것은 확장 함수을 사용하여 수행됩니다. 다음은 Kotlin에서 확장 함수를 정의하는 방법의 예입니다.

```kt
fun String.isPalindrome(): Boolean {
    return this == this.reversed()
}
```

- Java에서 동일한 효과를 얻으려면 상속 또는 정적 메서드가 있는 유틸리티 클래스를 사용해야 합니다.

### 타입 추론

- Kotlin은 Java에 비해 타입 추론을 개선했습니다. 컴파일러가 사용되는 컨텍스트를 기반으로 변수 및 표현식의 타입을 추론할 수 있습니다. 이렇게 하면 코드를 더 간결하고 읽기 쉽게 만들 수 있습니다. 예를 들어 Kotlin에서는 다음과 같이 변수를 정의할 수 있습니다.

```kt
val name = "John"
```

- `name` 변수의 타입은 `String`으로 유추되므로 명시적으로 지정할 필요가 없습니다. Java에서는 `String name = "John"` 와 같이 타입을 명시해줘야합니다.

### 함수형 프로그래밍

- Kotlin은 고차 함수(High-order function), 람다(lambda) 및 함수 타입(function types)과 같은 함수형 프로그래밍 지원합니다. 이렇게 하면 간결하고 표현력이 풍부하며 추론하기 쉬운 코드를 더 쉽게 작성할 수 있습니다. 다음은 Kotlin에서 고차 함수를 사용하는 방법의 예입니다.

```kt
fun processData(data: List<Int>, processor: (Int) -> Int): List<Int> {
    return data.map(processor)
}
```

- `List<Int>`와 processer 함수를 인자로 받아 리스트의 각 요소에 processor 함수를 적용하는 함수입니다. processor 함수는 정수를 받아 정수를 반환하는 람다 표현식입니다.

### 동시성(코루틴)

- Kotlin은 `kotlinx.coroutines` 라이브러리를 통해 동시성을 기본적으로 지원합니다. 코루틴을 사용하면 비동기식 비차단 코드(synchronous, non-blocking code)를 절차지향 스타일로 작성할 수 있으므로 기본 스레드를 차단하지 않고 백그라운드에서 작업을 수행하는 코드를 더 쉽게 작성할 수 있습니다. 다음은 Kotlin에서 코루틴을 사용하는 방법의 예입니다.

```kt
suspend fun loadData(): Data {
     // 비동기로 수행할 로직
}
```

- `suspend` 키워드는 이 함수가 코루틴이며 함수 내부의 코드를 일시 중지했다가 나중에 재개할 수 있음을 나타냅니다. `async` 함수를 사용하여 코루틴을 시작하고 완료 시 코루틴 결과에 액세스하는 데 사용할 수 있는 `Deferred` 개체를 가져올 수 있습니다.

```kt
val deferredData = async { loadData() }
val data = deferredData.await()
```

- 이 예제에서 `async` 함수는 `loadData()` 함수를 호출하는 코루틴을 시작하고 `await()` 함수는 코루틴이 완료될 때까지 기다렸다가 결과를 반환합니다.

- Java에서 동일한 효과를 얻으려면 `RxJava` 또는 `CompletableFuture`와 같은 라이브러리 또는 프레임워크를 사용해야 합니다.

### Java와의 상호 운용성

- Kotlin은 Java와 완벽하게 상호 운용 가능하므로 동일한 프로젝트에서 Kotlin과 Java 코드를 함께 사용할 수 있습니다. Java에서 Kotlin 코드를 호출하거나 그 반대로도 호출할 수 있습니다. 따라서 Kotlin을 기존 Java 프로젝트에 쉽게 통합하거나 Java 코드베이스를 Kotlin으로 점진적으로 마이그레이션할 수 있습니다.

> 전반적으로 Kotlin은 Java의 강점을 기반으로 하면서 일부 약점을 해결하는 최신 프로그래밍 언어입니다. Kotlin은 더 간결하고 표현력이 풍부한 구문, null safety 및 함수형 프로그래밍에 대한 더 나은 지원, Java와의 우수한 상호 운용성을 제공하며, 동시성 및 고급 프로그래밍을 위한 추가적인 기능을 제공합니다.

![kotlin.jpeg](/kotlin.jpeg =500x){.align-center}