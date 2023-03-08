---
title: 032: Kotlin의 원시 문자열: 이스케이프 없이 여러 줄 문자열 만들기
description: 
published: true
date: 2023-02-01T07:43:37.380Z
tags: 
editor: markdown
dateCreated: 2023-02-01T07:43:33.909Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [032: Raw Strings in Kotlin: Creating Multi-Line Strings Without Escaping***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/032-raw-strings-in-kotlin-creating-multi-line-strings-without-escaping)
{.links-list}


# 032: Kotlin의 원시 문자열: 이스케이프하지 않고 여러 줄 문자열 만들기

Kotlin의 원시 문자열은 여러 줄의 텍스트를 포함하는 문자열을 만들어야 할 때 유용합니다. 원시 문자열은 삼중 따옴표(""")로 묶여 있으며 여러 줄의 텍스트에 걸쳐 있을 수 있습니다.

일반 문자열과 달리 원시 문자열에는 줄 바꿈과 따옴표를 포함한 모든 문자가 포함될 수 있습니다. 따라서 여러 줄의 텍스트가 포함된 문자열을 만드는 데 이상적입니다.

원시 문자열을 만들려면 단순히 문자열을 삼중 따옴표로 묶습니다. 예를 들어:

```kotlin
val rawString = """
    This is a raw string.
    It can span multiple lines.
    It can contain any character, including newlines and quotes.
""".trimIndent()
```

보시다시피 원시 문자열에는 여러 줄의 텍스트가 포함되어 있습니다. 또한 따옴표(")와 줄 바꿈도 포함됩니다.

위의 원시 문자열은 `rawString` 변수에 할당됩니다. 이 변수의 내용을 콘솔에 출력할 수 있습니다.

```kotlin
println(rawString)
```

그러면 콘솔에 다음이 인쇄됩니다.

```
This is a raw string.
It can span multiple lines.
It can contain any character, including newlines and quotes.
```

보시다시피 원시 문자열에는 줄 바꿈과 따옴표를 포함한 모든 텍스트가 포함됩니다.

일반 문자열을 사용했다면 줄 바꿈과 따옴표가 이스케이프되어 다음과 같이 표시되었을 것입니다.

```
This is a raw string.\nIt can span multiple lines.\nIt can contain any character, including newlines and quotes.
```

보시다시피 개행과 따옴표는 백슬래시로 이스케이프 처리됩니다. 이는 일반 문자열이 개행 문자와 따옴표를 특수 문자로 취급하기 때문입니다.

반면 원시 문자열은 모든 문자를 리터럴로 취급합니다. 따라서 여러 줄의 텍스트가 포함된 문자열을 만드는 데 이상적입니다.

원시 문자열로 작업할 때 염두에 두어야 할 몇 가지 사항이 있습니다. 첫째, 모든 선행 및 후행 공백이 유지됩니다. 여기에는 줄 바꿈, 공백 및 탭이 포함됩니다.

둘째, 원시 문자열은 보간할 수 없습니다. 이는 원시 문자열 내에서 문자열 템플릿이나 변수를 사용할 수 없음을 의미합니다. 예를 들어 다음 코드는 컴파일되지 않습니다.

```kotlin
val name = "John"
val rawString = """
    Hello, $name!
""".trimIndent()
```

문자열을 보간해야 하는 경우 일반 문자열을 사용해야 합니다.

셋째, 원시 문자열은 연결할 수 없습니다. 이는 `+` 연산자를 사용하여 원시 문자열을 연결할 수 없음을 의미합니다. 예를 들어 다음 코드는 컴파일되지 않습니다.

```kotlin
val rawString1 = """
    This is a raw string.
""".trimIndent()

val rawString2 = """
    It can span multiple lines.
""".trimIndent()

val rawString = rawString1 + rawString2
```

원시 문자열을 연결해야 하는 경우 `trimMargin()` 또는 `trimIndent()` 메서드를 사용해야 합니다. 예를 들어:

```kotlin
val rawString1 = """
    |This is a raw string.
""".trimMargin()

val rawString2 = """
    |It can span multiple lines.
""".trimMargin()

val rawString = rawString1 + rawString2
```

`trimMargin()` 메서드는 줄 바꿈, 공백 및 탭을 포함하여 모든 선행 공백을 제거합니다. `trimIndent()` 메서드도 비슷하지만 첫 줄의 선행 공백만 제거합니다.

넷째, 원시 문자열은 `toString()` 메서드를 사용하여 일반 문자열로 변환할 수 있습니다. 예를 들어:

```kotlin
val rawString = """
    This is a raw string.
    It can span multiple lines.
    It can contain any character, including newlines and quotes.
""".trimIndent()

val regularString = rawString.toString()
```

`toString()` 메서드는 일반 문자열을 반환합니다. 이 문자열은 보간 및 연결될 수 있습니다.

마지막으로 원시 문자열은 `toByteArray()` 메서드를 사용하여 바이트 배열로 변환할 수 있습니다. 예를 들어:

```kotlin
val rawString = """
    This is a raw string.
    It can span multiple lines.
    It can contain any character, including newlines and quotes.
""".trimIndent()

val byteArray = rawString.toByteArray()
```

`toByteArray()` 메서드는 바이트 배열을 반환합니다. 이 바이트 배열을 사용하여 일반 문자열을 만들 수 있습니다.

원시 문자열은 Kotlin의 강력한 기능입니다. 여러 줄의 텍스트를 포함하는 문자열을 만드는 데 특히 유용합니다.