---
title: 029: Kotlin의 표준 라이브러리 함수: 일반적으로 사용되는 함수 활용
description: 
published: true
date: 2023-02-06T17:55:48.548Z
tags: 
editor: markdown
dateCreated: 2023-02-06T17:55:47.010Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [029: Standard Library Functions in Kotlin: Utilizing Commonly Used Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/029-standard-library-functions-in-kotlin-utilizing-commonly-used-functions)
{.links-list}


# 029: Kotlin의 표준 라이브러리 함수: 일반적으로 사용되는 함수 활용

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어이며 JavaScript 소스 코드로 컴파일할 수도 있습니다. Kotlin 표준 라이브러리는 추가 종속성 없이 사용할 수 있는 일반적으로 사용되는 함수 집합을 제공합니다.

이 게시물에서는 Kotlin 표준 라이브러리에서 가장 일반적으로 사용되는 몇 가지 기능과 이를 코드에서 활용하는 방법을 살펴보겠습니다.

## 컬렉션

Kotlin은 데이터 컬렉션 작업을 위한 일련의 함수를 제공합니다. 이러한 함수는 ```kotlin.collections``` 패키지에서 사용할 수 있습니다.

### 컬렉션 만들기

```kotlin
val array = arrayOf("a", "b", "c")
```코틀린
값 배열 = arrayOf("a", "b", "c")
```kotlin
val list = listOf(1, 2, 3)
```코틀린
값 목록 = listOf(1, 2, 3)
```kotlin
val mutableList = mutableListOf(1.0f, 2.0f, 3.0f)
```코틀린
val mutableList = mutableListOf(1.0f, 2.0f, 3.0f)
```kotlin
val firstElement = array[0]
```get()``` 함수를 사용하여 컬렉션의 요소에 액세스할 수 있습니다. 이 함수는 ```Int``` 인덱스를 사용하고 해당 인덱스에 있는 요소를 반환합니다.

예를 들어 다음과 같이 배열의 첫 번째 요소에 액세스할 수 있습니다.

```kotlin
val lastElement = list[list.size - 1]
```

다음과 같이 목록의 마지막 요소에 액세스할 수 있습니다.

```kotlin
val middleElement = mutableList[mutableList.size / 2]
```

그리고 다음과 같이 변경 가능한 목록의 중간 요소에 액세스할 수 있습니다.

```kotlin
mutableList.add("d")
```

### 컬렉션에서 요소 추가 및 제거

```kotlin
mutableList.removeAt(0)
```코틀린
mutableList.add("d")
```kotlin
mutableList.removeAt(mutableList.size - 1)
```코틀린
mutableList.removeAt(0)
```kotlin
val string = String(42)
```코틀린
mutableList.removeAt(mutableList.size - 1)
```kotlin
val string = "Hello" + "World"
```kotlin.text``` 패키지에서 사용할 수 있습니다.

### 문자열 만들기

```kotlin
val firstCharacter = string[0]
```코틀린
값 문자열 = 문자열(42)
```kotlin
val lastCharacter = string[string.length - 1]
```코틀린
val string = "안녕하세요" + "세계"
```kotlin
val middleCharacter = string[string.length / 2]
```get()``` 함수를 사용하여 문자열의 문자에 액세스할 수 있습니다. 이 함수는 ```Int``` 인덱스를 사용하여 해당 인덱스에 있는 문자를 반환합니다.

예를 들어 다음과 같이 문자열의 첫 번째 문자에 액세스할 수 있습니다.

```kotlin
val exclamationString = string + "!"
```

다음과 같이 문자열의 마지막 문자에 액세스할 수 있습니다.

```kotlin
val noFirstCharacterString = string.drop(1)
```

다음과 같이 문자열의 중간 문자에 액세스할 수 있습니다.

```kotlin
val noLastCharacterString = string.dropLast(1)
```

### 문자열에서 문자 추가 및 제거

```plus()``` 및 ```minus()``` 함수를 사용하여 문자열에서 문자를 추가하고 제거할 수 있습니다. ```plus()``` 함수는 문자열 끝에 문자를 추가하고 ```minus()``` 함수는 문자열에서 문자를 제거합니다.

예를 들어 문자 "!"를 추가할 수 있습니다. 다음과 같이 문자열의 끝까지:

```코틀린
val exclamationString = 문자열 + "!"
```

다음과 같이 문자열에서 첫 번째 문자를 제거할 수 있습니다.

```코틀린
val noFirstCharacterString = string.drop(1)
```

다음과 같이 문자열에서 마지막 문자를 제거할 수 있습니다.

```코틀린
val noLastCharacterString = string.dropLast(1)
```

## 결론

이 게시물에서는 Kotlin 표준 라이브러리에서 가장 일반적으로 사용되는 함수 중 일부를 살펴보았습니다. 컬렉션을 만들고 조작하는 방법, 문자열로 작업하는 방법, Kotlin에서 일반적으로 사용되는 다른 함수를 사용하는 방법을 살펴보았습니다.