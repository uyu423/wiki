---
title: 082: Kotlin 테스트: Kotlin 코드 테스트 작성 및 실행
description: 
published: true
date: 2023-02-10T22:55:25.990Z
tags: 
editor: markdown
dateCreated: 2023-02-10T22:55:24.344Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [082: Testing in Kotlin: Writing and Running Tests for Your Kotlin Code***English** document is available*](/en/Knowledge-base/Kotlin/Learning/082-testing-in-kotlin-writing-and-running-tests-for-your-kotlin-code)
{.links-list}


# 082: Kotlin 테스트: Kotlin 코드 테스트 작성 및 실행

테스트는 소프트웨어 개발 프로세스의 중요한 부분입니다. 코드가 정확하고 예상대로 작동하는지 확인하는 데 도움이 됩니다. 이 게시물에서는 Kotlin 코드에 대한 테스트를 작성하고 실행하는 방법을 알아봅니다.

## 테스트 작성

테스트는 [JUnit](https://junit.org/) 프레임워크를 사용하여 Kotlin으로 작성됩니다. JUnit은 Kotlin 프로젝트에 사용할 수 있는 널리 사용되는 Java용 테스트 프레임워크입니다.

테스트를 작성하려면 프로젝트에서 새 Kotlin 파일을 만들고 `@Test` 주석으로 주석을 추가합니다. 이 주석은 JUnit 프레임워크에 이 파일의 코드가 테스트임을 알려줍니다.

```kotlin
@Test
fun test() {
    // code for the test goes here
}
```

테스트는 일반적으로 설정, 실행 및 검증의 세 부분으로 구성됩니다. 설정 단계에서 테스트에 필요한 개체 또는 데이터를 초기화합니다. 실행 단계에서는 테스트 중인 코드를 실행합니다. 확인 단계에서 코드가 예상대로 작동하는지 확인합니다.

간단한 예를 살펴보겠습니다. 숫자의 계승을 계산하는 함수가 있다고 가정합니다. 다음 템플릿을 사용하여 이 함수에 대한 테스트를 작성할 수 있습니다.

```kotlin
@Test
fun test() {
    // setup
    val input = 5

    // execution
    val output = factorial(input)

    // verification
    assertEquals(120, output)
}
```

설정 단계에서 `input` 변수를 만들고 `5`로 설정합니다. 실행 단계에서 `input`을 인수로 사용하여 `factorial` 함수를 호출합니다. 이 함수는 `output` 변수에 저장하는 `input`의 계승을 반환합니다. 검증 단계에서 `assertEquals` 함수를 사용하여 `output`이 `120`과 같다고 어설션합니다.

이 테스트를 실행하고 통과하면 `factorial` 기능이 올바르게 작동한다고 확신할 수 있습니다.

## 테스트 실행

테스트는 명령줄 또는 IDE 내에서 실행할 수 있습니다. 명령줄에서 테스트를 실행하려면 [Gradle](https://gradle.org/) 빌드 도구를 사용해야 합니다. Gradle은 Kotlin 프로젝트에 사용할 수 있는 Java 프로젝트용 빌드 도구입니다.

명령줄에서 테스트를 실행하려면 프로젝트의 루트 디렉터리로 이동하고 다음 명령을 실행합니다.

```
gradle test
```

이렇게 하면 프로젝트의 모든 테스트가 실행됩니다.

IDE 내에서 테스트를 실행하려면 IDE용 [JUnit 플러그인](https://plugins.gradle.org/plugin/org.junit.platform.idea)을 설치해야 합니다. 플러그인이 설치되면 IDE 내에서 테스트를 실행할 수 있어야 합니다.

## 추가 정보

- [JUnit 웹사이트](https://junit.org/)
- [JUnit 문서](https://junit.org/junit5/docs/current/user-guide/)
- [그래들 홈페이지](https://gradle.org/)
- [Gradle 설명서](https://docs.gradle.org/current/userguide/userguide.html)