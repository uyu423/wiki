---
title: Kotlin 및 테스트 주도 개발(TDD): 실습 가이드
description: 
published: true
date: 2023-02-17T18:08:38.201Z
tags: 
editor: markdown
dateCreated: 2023-01-30T16:57:19.001Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kotlin and Test Driven Development (TDD): A Hands-on Guide***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-test-driven-development-tdd-a-hands-on-guide)
{.links-list}


# Kotlin 및 테스트 주도 개발(TDD): 실습 가이드

Kotlin은 JVM, Android, JavaScript 및 Native를 대상으로 하는 정적 유형 프로그래밍 언어입니다. Apache 2.0 라이선스에 따른 오픈 소스 프로젝트입니다. Kotlin은 또한 고차 함수가 있는 함수형 프로그래밍 언어입니다. 개발자는 기존의 모든 Java 라이브러리 및 프레임워크와 함께 Kotlin을 사용할 수 있습니다.

## 테스트 주도 개발(TDD)이란 무엇입니까?

테스트 주도 개발은 코드를 작성하기 전에 테스트를 먼저 작성해야 한다는 개발 방법론입니다. 이것의 목적은 코드가 테스트에서 지정한 요구 사항을 충족하는지 확인하는 것입니다. 이 방법론은 또한 코드를 보다 강력하고 리팩토링하기 쉽게 만들기 위한 것입니다.

## TDD에 Kotlin을 사용하는 이유는 무엇입니까?

Kotlin은 매우 간결한 언어이므로 전체적으로 적은 코드를 생성할 수 있습니다. 코드가 많을수록 모든 기능에 대한 테스트를 작성하는 데 더 많은 시간이 걸리므로 이는 테스트 작성에 중요합니다. 또한 Kotlin에는 null 안전 기능이 내장되어 있어 null 포인터 예외를 방지하는 데 도움이 됩니다. 이는 테스트에서 특히 중요합니다. 널 포인터가 있으면 테스트가 실패하기 때문입니다.

## TDD용 Kotlin 프로젝트 설정

IDE용 Kotlin 플러그인을 이미 설치했다고 가정하고 새 Kotlin 프로젝트를 만듭니다. 메시지가 표시되면 프로젝트 템플릿으로 "Java"를 선택합니다. 이 가이드에서는 Gradle 빌드 시스템을 사용합니다.

## 첫 Kotlin 테스트

이제 프로젝트가 설정되었으므로 첫 번째 테스트를 작성해 보겠습니다. 먼저 `MyFirstTest.kt`라는 `src/test/kotlin` 디렉토리에 파일을 생성합니다. 이 파일에서 Kotlin의 `sum` 함수가 예상대로 작동하는지 확인하는 테스트를 작성합니다.

```kotlin
import org.junit.Assert.*
import org.junit.Test

class MyFirstTest {
    @Test
    fun testSum() {
        assertEquals(4, sum(2, 2))
    }
}
```

여기에서는 테스트 작성에 사용할 `junit` 라이브러리를 가져왔습니다. 단일 `testSum` 메소드를 포함하는 `MyFirstTest` 클래스도 생성했습니다. 이 메소드는 `assertEquals` 함수를 사용하여 `2` 및 `2` 인수로 `sum`을 호출한 결과가 `4`와 같은지 확인합니다.

이 테스트를 실행하려면 `MyFirstTest.kt` 파일을 마우스 오른쪽 버튼으로 클릭하고 "'MyFirstTest' 실행"을 선택합니다. 테스트 실행을 확인하고 통과해야 합니다.

## 코드 작성

실패한 테스트가 있으므로 테스트를 통과하도록 코드를 작성할 차례입니다. `MyFirst.kt`라는 `src/main/kotlin` 디렉터리에 파일을 만듭니다. 이 파일에서 `sum` 함수를 작성합니다.

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

이제 테스트를 다시 실행하면 통과해야 합니다.

## 결론

이 기사에서는 TDD용 Kotlin 프로젝트를 설정하는 방법과 이를 통과하기 위한 첫 번째 테스트 및 코드를 작성하는 방법을 살펴보았습니다. TDD는 코드가 정확하고 리팩터링하기 쉬운지 확인하는 좋은 방법입니다. Kotlin의 간결한 구문과 내장된 null 안전 기능은 Kotlin을 TDD에 이상적인 언어로 만듭니다.