---
title: 025: Kotlin의 유형 추론: 컴파일러가 유형을 추론하게 하기
description: 
published: true
date: 2023-02-16T08:32:43.990Z
tags: 
editor: markdown
dateCreated: 2023-02-16T08:32:35.997Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [025: Type Inference in Kotlin: Letting the Compiler Infer Types***English** document is available*](/en/Knowledge-base/Kotlin/Learning/025-type-inference-in-kotlin-letting-the-compiler-infer-types)
{.links-list}


# Kotlin의 유형 추론: 컴파일러가 유형을 추론하게 함

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어입니다. Java와 완벽하게 상호 운용 가능하며 Android 앱을 개발하는 데 사용할 수 있습니다.

Kotlin의 기능 중 하나는 컴파일러가 변수 및 표현식의 유형을 유추할 수 있는 유형 유추입니다. 이는 작성해야 하는 코드의 양을 줄이는 데 도움이 될 수 있습니다.

## 유형 추론이란 무엇입니까?

형식 유추는 컴파일러가 변수 및 식의 형식을 유추할 수 있도록 하는 일부 프로그래밍 언어의 기능입니다. 이는 작성해야 하는 코드의 양을 줄이는 데 도움이 될 수 있습니다.

Kotlin에서는 유형 추론을 사용하여 변수 및 표현식의 유형을 추론합니다. Kotlin 컴파일러는 변수가 사용되는 컨텍스트에서 변수 유형을 유추할 수 있습니다. 예를 들어 변수에 Int 유형의 값이 할당된 경우 Kotlin 컴파일러는 변수가 Int 유형이라고 추론합니다.

## 유형 추론은 어떻게 작동합니까?

Kotlin의 유형 추론 시스템은 Hindley-Milner 유형 추론 알고리즘을 기반으로 합니다. 이 알고리즘은 Haskell 및 ML과 같은 많은 기능적 프로그래밍 언어에서 사용됩니다.

Hindley-Milner 유형 추론 알고리즘은 사용되는 컨텍스트에서 변수 및 표현식의 유형을 유추하여 작동합니다. 예를 들어 변수에 Int 유형의 값이 할당된 경우 Kotlin 컴파일러는 변수가 Int 유형이라고 추론합니다.

## 유형 추론의 이점은 무엇입니까?

형식 유추는 작성해야 하는 코드의 양을 줄이는 데 도움이 될 수 있습니다. 또한 변수와 식의 유형을 명시적으로 지정하여 코드를 더 읽기 쉽게 만들 수 있습니다.

## 타입 추론의 한계는 무엇인가요?

형식 유추는 변수 및 식의 형식을 암시적으로 만들어 코드를 읽기 어렵게 만드는 경우가 있습니다. 또한 변수와 식의 유형이 항상 명확하지 않기 때문에 코드를 디버그하기가 더 어려워질 수 있습니다.

## Kotlin에서 유형 추론을 사용하는 방법은 무엇입니까?

Kotlin의 유형 추론 시스템은 Hindley-Milner 유형 추론 알고리즘을 기반으로 합니다. 이 알고리즘은 Haskell 및 ML과 같은 많은 기능적 프로그래밍 언어에서 사용됩니다.

Hindley-Milner 유형 추론 알고리즘은 사용되는 컨텍스트에서 변수 및 표현식의 유형을 유추하여 작동합니다. 예를 들어 변수에 Int 유형의 값이 할당된 경우 Kotlin 컴파일러는 변수가 Int 유형이라고 추론합니다.

Kotlin에서 유형 추론을 사용하려면 유형을 지정하지 않고 변수를 선언하기만 하면 됩니다. Kotlin 컴파일러는 변수가 사용되는 컨텍스트에서 변수 유형을 유추합니다.

## Kotlin의 유형 추론 예시

다음은 Kotlin의 유형 추론에 대한 몇 가지 예입니다.

```kotlin
// The Kotlin compiler will infer that the type of the variable is Int
val x = 1

// The Kotlin compiler will infer that the type of the variable is String
val y = "Hello, world!"

// The Kotlin compiler will infer that the type of the variable is List<Int>
val z = listOf(1, 2, 3)
```

## 추가 정보

형식 유추는 컴파일러가 변수 및 식의 형식을 유추할 수 있도록 하는 일부 프로그래밍 언어의 기능입니다. 이는 작성해야 하는 코드의 양을 줄이는 데 도움이 될 수 있습니다.

Kotlin에서는 유형 추론을 사용하여 변수 및 표현식의 유형을 추론합니다. Kotlin 컴파일러는 변수가 사용되는 컨텍스트에서 변수 유형을 유추할 수 있습니다. 예를 들어 변수에 Int 유형의 값이 할당된 경우 Kotlin 컴파일러는 변수가 Int 유형이라고 추론합니다.

Kotlin의 유형 추론 시스템은 Hindley-Milner 유형 추론 알고리즘을 기반으로 합니다. 이 알고리즘은 Haskell 및 ML과 같은 많은 기능적 프로그래밍 언어에서 사용됩니다.

Hindley-Milner 유형 추론 알고리즘은 사용되는 컨텍스트에서 변수 및 표현식의 유형을 유추하여 작동합니다. 예를 들어 변수에 Int 유형의 값이 할당된 경우 Kotlin 컴파일러는 변수가 Int 유형이라고 추론합니다.

형식 유추는 작성해야 하는 코드의 양을 줄이는 데 도움이 될 수 있습니다. 또한 변수와 식의 유형을 명시적으로 지정하여 코드를 더 읽기 쉽게 만들 수 있습니다.

형식 유추는 변수 및 식의 형식을 암시적으로 만들어 코드를 읽기 어렵게 만드는 경우가 있습니다. 또한 변수와 식의 유형이 항상 명확하지 않기 때문에 코드를 디버그하기가 더 어려워질 수 있습니다.

Kotlin에서 유형 추론을 사용하려면 유형을 지정하지 않고 변수를 선언하기만 하면 됩니다. Kotlin 컴파일러는 변수가 사용되는 컨텍스트에서 변수 유형을 유추합니다.