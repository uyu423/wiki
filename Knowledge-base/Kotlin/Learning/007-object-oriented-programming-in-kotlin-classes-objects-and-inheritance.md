---
title: 007: Kotlin의 객체 지향 프로그래밍: 클래스, 객체 및 상속
description: 
published: true
date: 2023-01-31T05:10:52.083Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:10:50.471Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [007: Object-Oriented Programming in Kotlin: Classes, Objects, and Inheritance***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/007-object-oriented-programming-in-kotlin-classes-objects-and-inheritance)
{.links-list}




Kotlin은 JVM에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어이며 JavaScript로 컴파일할 수도 있습니다. Kotlin은 Java와 상호 운용이 가능하도록 설계되었으므로 Android 애플리케이션 개발에 탁월한 선택입니다.

객체 지향 프로그래밍은 데이터와 메서드를 모두 포함하는 데이터 구조인 객체 개념을 기반으로 하는 프로그래밍 패러다임입니다. Kotlin은 객체 지향 언어이므로 클래스, 객체 및 상속을 지원합니다.

## 클래스, 객체, 상속

Kotlin에서 클래스는 객체를 생성하기 위한 템플릿입니다. 클래스는 멤버라고도 하는 속성과 메서드를 포함할 수 있습니다. 속성은 클래스와 관련된 데이터 조각이고 메서드는 개체에서 호출할 수 있는 함수입니다.

Kotlin에서 클래스를 만들려면 'class'라는 키워드를 사용하고 그 뒤에 클래스 이름을 씁니다. 예를 들어 다음 코드는 `Person`이라는 클래스를 만듭니다.

```kotlin
class Person {

}
```

클래스는 멤버라고도 하는 속성과 메서드를 포함할 수 있습니다. 속성은 클래스와 관련된 데이터 조각이고 메서드는 개체에서 호출할 수 있는 함수입니다.

클래스에 속성을 추가하려면 `var` 또는 `val` 키워드를 사용하고 그 뒤에 속성 이름과 해당 유형을 입력합니다. 예를 들어 다음 코드는 `String` 유형의 `name`이라는 속성을 만듭니다.

```kotlin
class Person {
    var name: String
}
```

메서드를 클래스에 추가하려면 `fun` 키워드 다음에 메서드 이름과 해당 매개 변수가 사용됩니다. 예를 들어, 다음 코드는 `String` 유형의 `name` 매개변수를 사용하는 `greet`라는 메서드를 생성합니다.

```kotlin
class Person {
    fun greet(name: String) {
        println("Hello, $name!")
    }
}
```

클래스에서 객체를 생성하기 위해 `new` 키워드와 클래스 이름이 사용됩니다. 예를 들어 다음 코드는 `Person` 클래스에서 개체를 만듭니다.

```kotlin
val person = Person()
```

객체에서 메소드를 호출하기 위해 `.` 연산자가 사용되며 그 뒤에 메소드 이름과 해당 매개변수가 옵니다. 예를 들어, 다음 코드는 `person` 객체에서 `greet` 메서드를 호출하여 인사할 사람의 `name`을 전달합니다.

```kotlin
person.greet("John")
```

## 상속

상속은 한 클래스가 다른 클래스에서 파생될 수 있는 메커니즘입니다. 파생되는 클래스를 수퍼 클래스라고 하고 파생하는 클래스를 하위 클래스라고 합니다.

Kotlin에서 하위 클래스는 `:` 연산자와 상위 클래스 이름을 사용하여 정의할 수 있습니다. 예를 들어 다음 코드는 `Person` 클래스에서 상속되는 `Student` 클래스를 정의합니다.

```kotlin
class Student: Person {

}
```

하위 클래스는 상위 클래스의 모든 속성과 메서드를 상속하며 자체 속성과 메서드를 정의할 수도 있습니다.

예를 들어 `Student` 클래스는 자체 `enroll` 메소드를 정의할 수 있을 뿐만 아니라 다음 코드와 같이 `Person` 클래스의 `greet` 메소드를 재정의할 수 있습니다.

```kotlin
class Student: Person {
    fun enroll() {
        // enroll student in class
    }

    override fun greet(name: String) {
        println("Hello, $name! I'm a student.")
    }
}
```

## 결론

Kotlin은 클래스, 객체 및 상속을 지원하는 정적으로 유형이 지정된 객체 지향 프로그래밍 언어입니다. Kotlin은 Java와 상호 운용이 가능하도록 설계되었으므로 Android 애플리케이션 개발에 탁월한 선택입니다.