---
title: 062: Kotlin의 싱글톤 패턴: 클래스의 인스턴스가 하나만 존재하도록 보장
description: 
published: true
date: 2023-02-16T23:32:26.287Z
tags: 
editor: markdown
dateCreated: 2023-02-16T23:32:18.297Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [062: The Singleton Pattern in Kotlin: Ensuring Only One Instance of a Class Exists***English** document is available*](/en/Knowledge-base/Kotlin/Learning/062-the-singleton-pattern-in-kotlin-ensuring-only-one-instance-of-a-class-exists)
{.links-list}


# Kotlin의 싱글톤 패턴: 클래스의 인스턴스가 하나만 존재하도록 보장

싱글톤 패턴은 클래스의 인스턴스화를 하나의 개체로 제한하는 소프트웨어 디자인 패턴입니다. 이는 공유 리소스를 관리하거나 전역 상태를 처리하거나 시스템 전체에서 작업을 조정해야 하는 경우와 같이 응용 프로그램에 대한 클래스 인스턴스가 하나만 필요한 경우에 유용합니다.

Kotlin에서는 객체 선언을 사용하여 싱글톤을 구현할 수 있습니다. 개체 선언은 인스턴스를 저장하기 위한 전용 생성자와 공용 정적 필드가 있는 일반 클래스의 구문 설탕입니다.

다음은 Kotlin의 싱글톤 클래스에 대한 간단한 예입니다.

```kotlin
object MySingleton {
    fun doSomething() {
        // ...
    }
}
```

개체 이름을 사용하여 싱글톤 인스턴스에 액세스할 수 있습니다.

```kotlin
MySingleton.doSomething()
```

일부 매개변수로 싱글톤을 초기화해야 하는 경우 컴패니언 객체를 사용할 수 있습니다.

```kotlin
class MySingleton private constructor(val param: String) {
    companion object {
        fun getInstance(param: String): MySingleton {
            return MySingleton(param)
        }
    }

    fun doSomething() {
        // ...
    }
}
```

그런 다음 컴패니언 객체의 이름을 사용하여 싱글톤 인스턴스에 액세스할 수 있습니다.

```kotlin
MySingleton.getInstance("some param").doSomething()
```

Kotlin에서 개체 선언은 스레드로부터 안전하지 않다는 점에 유의해야 합니다. 클래스의 인스턴스가 하나만 생성되도록 해야 하는 경우 동기화된 블록을 사용해야 합니다.

```kotlin
object MySingleton {
    @Volatile
    private var instance: MySingleton? = null

    fun getInstance(): MySingleton {
        return instance ?: synchronized(this) {
            instance ?: MySingleton().also { instance = it }
        }
    }

    fun doSomething() {
        // ...
    }
}
```

그런 다음 개체 이름을 사용하여 싱글톤 인스턴스에 액세스할 수 있습니다.

```kotlin
MySingleton.getInstance().doSomething()
```

싱글톤 패턴은 전역 상태 및 리소스를 관리하는 데 유용한 도구입니다. 그러나 밀접하게 결합된 코드와 테스트하기 어려운 코드로 이어질 수 있으므로 주의해서 사용해야 합니다.

## 추가 정보

* [위키백과: 싱글톤 패턴](https://en.wikipedia.org/wiki/Singleton_pattern)
* [Kotlin 언어 문서: 객체](https://kotlinlang.org/docs/reference/objects.html)

## 더 읽을 수 있는 리소스

* [Kotlin의 디자인 패턴: 싱글톤 패턴](https://antonioleiva.com/kotlin-singleton/)
* [영역: Kotlin 싱글톤 토론](https://academy.realm.io/posts/kotlin-singleton-debate/)
* [Android 개발자: 싱글톤 및 메모리 누수](https://developer.android.com/training/articles/memory.html# LeakCanary)