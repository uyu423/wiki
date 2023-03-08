---
title: 018: Kotlin의 컴패니언 객체: 클래스의 정적 멤버
description: 
published: true
date: 2023-02-16T05:32:16.536Z
tags: 
editor: markdown
dateCreated: 2023-02-16T05:32:14.980Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [018: Companion Objects in Kotlin: Static Members in Classes***English** document is available*](/en/Knowledge-base/Kotlin/Learning/018-companion-objects-in-kotlin-static-members-in-classes)
{.links-list}


# Kotlin의 컴패니언 객체: 클래스의 정적 멤버

Kotlin 컴패니언 객체를 사용하면 클래스에서 정적 멤버를 정의할 수 있습니다. 이번 포스팅에서는 컴패니언 오브젝트가 무엇이고 어떻게 사용하는지 알아보도록 하겠습니다.

## 컴패니언 객체란?

 컴패니언 개체는 클래스와 연결된 개체입니다. 정적 멤버를 클래스에 저장하는 데 사용됩니다.

정적 멤버는 클래스의 인스턴스가 아닌 클래스와 연결된 멤버입니다. 즉, 클래스의 인스턴스를 만들지 않고도 액세스할 수 있습니다.

 컴패니언 객체는 `컴패니언 객체` 키워드를 사용하여 선언됩니다. 상수, 유틸리티 함수 및 팩토리 메서드를 저장하는 데 사용할 수 있습니다.

## 컴패니언 객체 사용 방법

컴패니언 객체는 `컴패니언 객체` 키워드를 사용하여 선언됩니다. 상수, 유틸리티 함수 및 팩토리 메서드를 저장하는 데 사용할 수 있습니다.

컴패니언 객체의 멤버에 액세스하려면 클래스 이름을 한정자로 사용합니다. 예를 들어 `MyClass.kt`라는 파일에 `MyClass`라는 컴패니언 객체가 있는 경우 다음과 같이 해당 멤버에 액세스합니다.

```kotlin
MyClass.Companion.myFunction()
```

클래스 내에서 컴패니언 객체의 멤버에 액세스하려면 `companion` 키워드를 생략할 수 있습니다. 예를 들어:

```kotlin
class MyClass {
    companion object {
        fun myFunction() {
            // ...
        }
    }
}
```

## 결론

이번 포스팅에서는 컴패니언 오브젝트가 무엇이고 어떻게 사용하는지 알아보았습니다. 컴패니언 개체는 정적 멤버를 클래스에 저장하는 좋은 방법입니다.