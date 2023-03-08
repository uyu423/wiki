---
title: 057: Kotlin의 예외 처리: 오류 및 예외 처리
description: 
published: true
date: 2023-02-01T16:23:24.676Z
tags: 
editor: markdown
dateCreated: 2023-02-01T16:23:22.982Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [057: Exception Handling in Kotlin: Dealing with Errors and Exceptions***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/057-exception-handling-in-kotlin-dealing-with-errors-and-exceptions)
{.links-list}


# 코틀린 예외 처리

예외는 정상적인 명령 흐름을 방해하는 프로그램 실행 중에 발생하는 이벤트입니다. Kotlin은 예외를 처리하는 강력한 메커니즘을 제공합니다. 이 기사에서는 Kotlin에서 예외를 처리하는 방법을 살펴보겠습니다.

## 예외란 무엇인가요?

예외는 정상적인 명령 흐름을 방해하는 프로그램 실행 중에 발생하는 이벤트입니다. 예외가 발생하면 프로그램이 갑자기 종료됩니다.

예외에는 두 가지 유형이 있습니다: 선택됨과 선택되지 않음. 확인된 예외는 파일을 찾을 수 없는 경우와 같이 컴파일 시간에 발생하는 예외입니다. 확인되지 않은 예외는 0으로 나누기 오류가 발생하는 경우와 같이 런타임에 발생하는 예외입니다.

## 예외 처리

Kotlin은 예외를 처리하는 강력한 메커니즘을 제공합니다. try/catch 블록은 예외를 처리하는 데 사용됩니다. try 블록에는 예외를 throw할 수 있는 코드가 포함되어 있습니다. catch 블록에는 예외를 처리하는 코드가 포함되어 있습니다.

```kotlin
try {
   // code that may throw an exception
} catch (e: Exception) {
   // code that handles the exception
}
```

try 블록에서 예외가 발생하면 catch 블록이 실행됩니다. 예외가 발생하지 않으면 catch 블록을 건너뜁니다.

다른 유형의 예외를 처리하기 위해 여러 개의 catch 블록을 가질 수도 있습니다.

```kotlin
try {
   // code that may throw an exception
} catch (e: FileNotFoundException) {
   // code that handles the FileNotFoundException
} catch (e: IOException) {
   // code that handles the IOException
}
```

## 마지막으로 차단

finally 블록은 선택 사항입니다. 예외 발생 여부에 관계없이 실행됩니다.

```kotlin
try {
   // code that may throw an exception
} catch (e: Exception) {
   // code that handles the exception
} finally {
   // code that is always executed
}
```

## 예외 던지기

예외는 throw 키워드를 사용하여 명시적으로 throw할 수 있습니다.

```kotlin
throw FileNotFoundException()
```

## 사용자 지정 예외 만들기

Exception 클래스를 확장하여 사용자 정의 예외를 생성할 수 있습니다.

```kotlin
class MyException: Exception() {
}
```

## 자원

- [Kotlin 문서 - 예외 처리](https://kotlinlang.org/docs/reference/exceptions.html)
- [JavaWorld - Kotlin의 예외 처리](https://www.javaworld.com/article/3240006/learn-java/exception-handling-in-kotlin.html)
- [Stack Overflow - Kotlin에서 맞춤 예외를 어떻게 생성하나요?](https://stackoverflow.com/questions/44487193/how-do-i-create-a-custom-exception-in-kotlin)