---
title: 100: Kotlin의 고급 유형 시스템: Kotlin 유형 시스템의 고급 기능 탐색.
description: 
published: true
date: 2023-02-06T13:18:00.521Z
tags: 
editor: markdown
dateCreated: 2023-02-06T13:17:54.912Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [100: Advanced Type System in Kotlin: Exploring the Advanced Features of the Kotlin Type System.***English** document is available*](/en/Knowledge-base/Kotlin/Learning/100-advanced-type-system-in-kotlin-exploring-the-advanced-features-of-the-kotlin-type-system-)
{.links-list}


Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어입니다. Android 애플리케이션, 서버 측 애플리케이션 등을 개발하는 데 사용할 수 있는 범용 언어입니다. Kotlin 유형 시스템은 유연하고 확장 가능하도록 설계되었으며 null 안전, 유형 추론, 제네릭과 같은 다양한 고급 기능을 지원합니다.

이 게시물에서는 Kotlin 유형 시스템의 일부 고급 기능을 살펴보겠습니다. null 안전, 형식 유추, 제네릭 및 형식 안전 빌더에 대해 알아봅니다. 이 게시물을 마치면 Kotlin 유형 시스템과 고급 기능을 사용하여 안전하고 읽기 쉬운 코드를 작성하는 방법을 잘 이해할 수 있습니다.

## Null 안전

Kotlin 유형 시스템의 가장 중요한 기능 중 하나는 null 안전입니다. Kotlin의 null 안전 시스템은 null 포인터 예외가 발생하지 않도록 설계되었습니다. Kotlin에서 모든 유형은 기본적으로 null을 허용하지 않습니다. 즉, 어떤 유형의 변수에도 null 값을 할당할 수 없습니다. 그렇게 하려고 하면 컴파일러 오류가 발생합니다.

형식을 nullable로 만들려면 nullable 형식 한정자를 사용해야 합니다. 예를 들어 다음 코드는 null 허용 문자열 변수를 정의합니다.

```kotlin
var s: String? = "foo"
```

이제 변수 s는 null이 아닌 문자열 값이나 null 값을 보유할 수 있습니다. null을 허용하지 않는 변수에 null 값을 할당하려고 하면 다시 컴파일러 오류가 발생합니다.

nullable 변수가 null인지 확인하려면 `isNullOrEmpty()` 함수를 사용할 수 있습니다.

```kotlin
if (s.isNullOrEmpty()) {
    // s is null or empty
}
```

nullable 변수의 값에 액세스하려면 `?.` 연산자를 사용해야 합니다. 이 연산자는 값에 액세스하기 전에 변수가 null인지 확인합니다. 예를 들어 다음 코드는 s가 null이 아니면 "foo"를 인쇄하고 s가 null이면 "bar"를 인쇄합니다.

```kotlin
println(s?.length ?: "bar")
```

`!!` 연산자를 사용하여 null 허용 변수를 강제로 래핑 해제할 수도 있습니다. 변수가 null이면 예외가 발생합니다. 예를 들어 다음 코드는 s가 null인 경우 예외를 발생시킵니다.

```kotlin
println(s!!.length)
```

## 유형 추론

Kotlin의 유형 추론 시스템은 초기화 표현식에서 변수의 유형을 자동으로 추론하도록 설계되었습니다. 예를 들어 다음 코드는 Int 유형의 변수를 정의합니다.

```kotlin
val x = 1
```

여기에서 변수 x의 유형은 이니셜라이저 표현식에서 Int로 유추됩니다. Kotlin의 유형 추론 시스템은 매우 강력하며 이니셜라이저 표현식이 복잡한 경우에도 종종 변수의 유형을 추론할 수 있습니다.

## 제네릭

제네릭은 유형에 안전한 코드를 정의할 수 있게 해주는 Kotlin 유형 시스템의 강력한 기능입니다. 제네릭을 사용하면 유형을 매개변수화할 수 있으므로 모든 유형에서 작동하는 코드를 작성할 수 있습니다. 예를 들어 다음 코드는 모든 유형의 목록을 가져와 해당 요소를 인쇄하는 일반 함수를 정의합니다.

```kotlin
fun <T> printList(list: List<T>) {
    for (element in list) {
        println(element)
    }
}
```

여기서 유형 매개변수 T는 목록의 유형을 매개변수화하는 데 사용됩니다. 이 함수는 예를 들어 Int 목록과 같은 모든 유형의 목록을 인쇄하는 데 사용할 수 있습니다.

```kotlin
val list = listOf(1, 2, 3)
printList(list)
```

Kotlin을 사용하면 고유한 일반 유형을 정의할 수도 있습니다. 예를 들어 다음 코드는 모든 유형의 목록을 만드는 데 사용할 수 있는 일반 클래스를 정의합니다.

```kotlin
class List<T> {
    fun add(element: T) {
        // ...
    }

    fun get(index: Int): T {
        // ...
    }
}
```

이 클래스는 문자열 목록과 같은 모든 유형의 목록을 만드는 데 사용할 수 있습니다.

```kotlin
val list = List<String>()
list.add("foo")
list.add("bar")
println(list.get(0)) // prints "foo"
```

## 안전한 빌더

Kotlin의 유형 안전 빌더는 복잡한 데이터 구조를 빌드할 때 유형 안전 코드를 작성할 수 있게 해주는 강력한 기능입니다. 예를 들어 다음 코드는 문자열 목록에 대해 형식이 안전한 빌더를 정의합니다.

```kotlin
fun buildStringList(builder: StringListBuilder.() -> Unit): List<String> {
    val stringListBuilder = StringListBuilder()
    stringListBuilder.builder()
    return stringListBuilder.toList()
}

class StringListBuilder {
    private val list = mutableListOf<String>()

    fun add(string: String) {
        list.add(string)
    }

    fun toList(): List<String> {
        return list
    }
}
```

이 빌더는 다음과 같이 문자열 목록을 작성하는 데 사용할 수 있습니다.

```kotlin
val list = buildStringList {
    add("foo")
    add("bar")
}
```

Kotlin의 유형 안전 빌더는 복잡한 데이터 구조를 빌드할 때 안전하고 읽기 쉬운 코드를 작성하는 좋은 방법입니다.