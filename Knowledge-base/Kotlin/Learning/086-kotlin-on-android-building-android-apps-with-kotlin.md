---
title: 086: Android의 Kotlin: Kotlin으로 Android 앱 빌드
description: 
published: true
date: 2023-02-15T12:18:01.113Z
tags: 
editor: markdown
dateCreated: 2023-02-15T12:17:59.344Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [086: Kotlin on Android: Building Android Apps with Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/Learning/086-kotlin-on-android-building-android-apps-with-kotlin)
{.links-list}


# 086: Android의 Kotlin: Kotlin으로 Android 앱 빌드

Kotlin은 Android 앱을 빌드하는 데 사용할 수 있는 강력한 프로그래밍 언어입니다. 이 게시물에서는 Android에서 Kotlin을 시작하는 방법을 살펴보겠습니다.

## 코틀린 설치하기

Android에서 Kotlin을 시작하려면 먼저 Kotlin 플러그인을 설치해야 합니다. 파일 > 설정 > 플러그인으로 이동하고 Kotlin 플러그인을 검색하여 Android Studio 내에서 이 작업을 수행할 수 있습니다. 플러그인을 설치했으면 Android Studio를 다시 시작해야 합니다.

Android Studio가 다시 시작되면 새로운 Kotlin 프로젝트를 생성할 수 있습니다. 이렇게 하려면 파일 > 새로 만들기 > 새 프로젝트로 이동하고 프로젝트 유형 목록에서 Kotlin 옵션을 선택합니다.

## 코틀린 프로젝트 만들기

Kotlin 플러그인을 설치하면 새로운 Kotlin 프로젝트를 생성할 수 있습니다. 이렇게 하려면 파일 > 새로 만들기 > 새 프로젝트로 이동하고 프로젝트 유형 목록에서 Kotlin 옵션을 선택합니다.

새 Kotlin 프로젝트를 만들 때 프로젝트 SDK뿐만 아니라 프로젝트의 이름과 위치를 지정하라는 메시지가 표시됩니다. 이러한 세부 정보를 지정했으면 마침 버튼을 클릭하여 프로젝트를 만듭니다.

## 코틀린 파일 생성

Kotlin 프로젝트를 생성했으면 Kotlin 파일을 생성할 수 있습니다. 이렇게 하려면 파일 > 새로 만들기 > Kotlin 파일/클래스로 이동합니다.

새 Kotlin 파일을 만들 때 파일의 이름과 위치를 지정하라는 메시지가 표시됩니다. Kotlin 파일 형식을 지정하라는 메시지도 표시됩니다. 네 가지 Kotlin 파일 유형이 있습니다.

- 코틀린 클래스
- 코틀린 파일
- 코틀린 객체
- 코틀린 인터페이스

파일의 이름과 위치를 지정했으면 완료 버튼을 클릭하여 파일을 생성합니다.

## Kotlin 코드 작성

이제 Kotlin 프로젝트와 Kotlin 파일을 만들었으므로 Kotlin 코드 작성을 시작할 준비가 되었습니다.

Kotlin 코드는 확장자가 .kt인 파일로 작성됩니다. Kotlin 파일은 하나 이상의 최상위 선언을 포함할 수 있습니다. 최상위 선언은 클래스, 개체 또는 인터페이스 내부에 없는 선언입니다.

Kotlin은 Android 앱 개발을 위한 훌륭한 선택이 되도록 하는 풍부한 기능 세트를 갖추고 있습니다. 이러한 기능 중 일부는 다음과 같습니다.

- 널 안전
- 확장 기능
- 데이터 클래스
- 코루틴

다음 섹션에서는 이러한 기능 중 일부를 보다 자세히 살펴보겠습니다.

## 널 안전

Kotlin의 가장 중요한 기능 중 하나는 null 안전입니다. Null 안전은 null 포인터 예외가 발생하지 않도록 방지하는 기능입니다.

변수를 null safe로 만들려면 ? 운영자. 예를 들어 다음 코드는 name 변수가 null일 수 있으므로 컴파일되지 않습니다.

```kotlin
var name: String = "John"
name = null
```

코드를 null safe로 만들려면 ? 운영자:

```kotlin
var name: String? = "John"
name = null
```

이제 name 변수가 null일 수 있으므로 코드가 컴파일됩니다.

## 확장 기능

Kotlin의 또 다른 중요한 기능은 확장 기능입니다. 확장 함수를 사용하면 하위 클래스를 만들 필요 없이 새로운 기능으로 클래스를 확장할 수 있습니다.

예를 들어 클래스가 비어 있으면 true를 반환하고 그렇지 않으면 false를 반환하는 isEmpty() 함수가 있는 클래스가 있다고 가정합니다. isEmpty()의 반대를 반환하는 새로운 isNotEmpty() 함수를 사용하여 이 클래스를 확장할 수 있습니다.

```kotlin
fun isNotEmpty(): Boolean {
    return !isEmpty()
}
```

새 함수를 사용하려면 클래스의 인스턴스에서 호출하기만 하면 됩니다.

```kotlin
val list = ArrayList<String>()
list.isNotEmpty() // returns false
```

## 데이터 클래스

Kotlin은 데이터 클래스도 지원합니다. 데이터 클래스는 데이터를 보유하도록 설계된 클래스입니다. JavaBeans와 유사하지만 생성 및 사용이 훨씬 간단합니다.

데이터 클래스를 생성하려면 data 키워드를 사용해야 합니다.

```kotlin
data class User(val name: String, val age: Int)
```

이 코드는 name과 age라는 두 가지 속성이 있는 데이터 클래스를 생성합니다. 속성은 val 키워드를 사용하여 선언되며 이는 속성이 읽기 전용임을 의미합니다.

데이터 클래스의 인스턴스를 생성하려면 생성자를 호출하기만 하면 됩니다.

```kotlin
val user = User("John", 30)
```

데이터 클래스의 속성에 액세스하려면 점 표기법을 사용할 수 있습니다.

```kotlin
user.name // returns "John"
user.age // returns 30
```

데이터 클래스에는 toString(), hashCode() 및 equals()와 같은 여러 가지 유용한 함수도 있습니다.

```kotlin
user.toString() // returns "User(name=John, age=30)"
user.hashCode() // returns -1234
user.equals(other) // returns true if the two objects are equal
```

## 코루틴

코루틴은 비동기 코드를 더 쉽게 작성할 수 있게 해주는 Kotlin의 새로운 기능입니다. 코루틴은 스레드와 비슷하지만 훨씬 가볍고 스레드를 차단하지 않고 일시 중지할 수 있습니다.

코루틴을 사용하려면 kotlinx.coroutines 패키지를 가져와야 합니다.

```kotlin
import kotlinx.coroutines.*
```

그런 다음 launch() 함수를 사용하여 새 코루틴을 시작할 수 있습니다.

```kotlin
GlobalScope.launch {
    // suspendable code
}
```

launch() 함수 내에서 정지 가능한 코드를 작성할 수 있습니다. 이 코드는 스레드를 차단하지 않고 일시 중지할 수 있습니다.

코루틴을 일시 중지하려면 delay() 함수를 사용할 수 있습니다.

```kotlin
GlobalScope.launch {
    delay(1000) // suspend for 1 second
    // resume here
}
```

delay() 함수는 밀리초 단위의 시간 인수를 사용합니다. 지정된 시간이 경과하면 코루틴이 다시 시작됩니다.

또한 yield() 함수를 사용하여 코루틴을 일시 중단하고 다른 코루틴이 실행되도록 할 수 있습니다.

```kotlin
GlobalScope.launch {
    yield() // suspend and allow other coroutines to run
    // resume here
}
```

## 결론

이 게시물에서는 Android에서 Kotlin을 시작하는 방법을 살펴보았습니다. Kotlin 플러그인을 설치하고, Kotlin 프로젝트를 만들고, Kotlin 코드를 작성하는 방법을 살펴보았습니다. 또한 Kotlin을 Android 앱 개발에 탁월한 선택으로 만드는 몇 가지 기능도 확인했습니다.