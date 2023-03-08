---
title: Kotlin에서 생성자 및 속성 구현
description: 
published: true
date: 2023-02-02T02:18:21.310Z
tags: 
editor: markdown
dateCreated: 2023-02-02T02:18:19.498Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Implementing Constructors and Properties in Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/implementing-constructors-and-properties-in-kotlin)
{.links-list}


# Kotlin에서 생성자와 속성 구현

Kotlin은 개발 커뮤니티에서 인기를 얻고 있는 비교적 새로운 프로그래밍 언어입니다. JVM(Java Virtual Machine)에서 실행되는 정적 유형의 객체 지향 언어입니다. Kotlin은 기존의 모든 Java 라이브러리 및 프레임워크와 호환되며 광범위한 개발 작업에 사용할 수 있습니다.

Kotlin의 주요 기능 중 하나는 생성자 기반 프로그래밍을 지원한다는 것입니다. Kotlin에서 클래스는 하나 이상의 생성자를 가질 수 있습니다. 기본 생성자는 클래스 헤더에 정의되고 보조 생성자는 클래스 본문 내부에 정의됩니다.

생성자는 클래스의 개체를 초기화하는 데 사용됩니다. 변수, 호출 메서드 등에 대한 초기 값을 설정하는 데 사용할 수 있습니다. Kotlin에서는 클래스에 이니셜라이저가 없으면 생성자가 필요하지 않습니다. 그러나 클래스에 이니셜라이저가 있는 경우 하나 이상의 생성자를 정의해야 합니다.

다음은 기본 생성자와 두 개의 보조 생성자가 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person(val name: String) {
  
    var age: Int = 0
    
    constructor(name: String, age: Int) : this(name) {
        this.age = age
    }
    
    constructor(name: String, age: Int, gender: String) : this(name, age) {
        // ...
    }
}
```

위의 예에서 기본 생성자는 이름이라는 단일 인수를 사용합니다. 보조 생성자는 각각 2개와 3개의 인수를 사용합니다. 모든 생성자는 this 키워드를 사용하여 기본 생성자를 호출합니다.

생성자는 클래스의 속성을 초기화하는 데에도 사용할 수 있습니다. 위의 예에서 name 속성은 기본 생성자에 의해 초기화되고 age 속성은 보조 생성자에 의해 초기화됩니다.

Kotlin의 또 다른 기능은 속성 지원입니다. 속성은 클래스와 관련된 변수입니다. 클래스 헤더 또는 클래스 본문에서 선언할 수 있습니다.

다음은 name과 age라는 두 가지 속성이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person {
  
    var name: String = ""
    
    var age: Int = 0
}
```

위의 예에서 name 및 age 속성은 클래스 헤더에 선언됩니다. 둘 다 기본값 ""과 0으로 각각 초기화됩니다.

기본값이 아닌 값으로 속성을 초기화할 수도 있습니다. 다음 예에서 name 속성은 값 "John"으로 초기화되고 age 속성은 값 30으로 초기화됩니다.

```kotlin
class Person {
  
    var name: String = "John"
    
    var age: Int = 30
}
```

Kotlin은 속성의 지연 초기화도 지원합니다. 지연 초기화는 처음 액세스할 때까지 속성의 초기화를 지연시키는 기술입니다. Kotlin에서 지연 초기화는 by 키워드를 사용하여 수행됩니다.

다음은 지연 초기화 속성 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person {
  
    val name: String by lazy {
        // ...
    }
}
```

위의 예에서 name 속성은 val(불변)로 선언되고 느리게 초기화됩니다. 이니셜라이저는 속성에 처음 액세스할 때 호출되는 람다 식입니다.

Kotlin은 위임 속성도 지원합니다. 위임된 속성은 대리자 개체에 의해 구현되는 속성입니다. Kotlin에서 위임된 속성은 by 키워드를 사용하여 선언됩니다.

다음은 위임된 속성 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

위의 예에서 name 속성은 대리자 개체에 의해 구현됩니다. 대리자 개체는 람다 식에 의해 지연 초기화됩니다.

Kotlin은 확장 속성도 지원합니다. 확장 속성은 클래스의 확장으로 선언된 속성입니다. Kotlin에서 확장 속성은 by 키워드를 사용하여 선언됩니다.

다음은 확장 속성 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

위의 예에서 name 속성은 extension() 메서드를 호출하는 지연 람다 식으로 확장됩니다.

Kotlin은 후기 초기화 속성도 지원합니다. 늦게 초기화된 속성은 처음 액세스할 때까지 초기화되지 않는 속성입니다. Kotlin에서 늦게 초기화된 속성은 by 키워드를 사용하여 선언됩니다.

다음은 늦게 초기화된 속성 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person {
  
    lateinit var name: String
    
    fun init() {
        name = "John"
    }
}
```

위의 예에서 name 속성은 lateinit var(변경 가능)로 선언됩니다. init() 메서드가 호출될 때까지 초기화되지 않습니다.

Kotlin은 nullable 유형도 지원합니다. Nullable 유형은 null 값을 보유할 수 있는 유형입니다. Kotlin에서 nullable 유형은 ? 운영자.

다음은 null 허용 속성인 name이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person {
  
    var name: String? = null
}
```

위의 예에서 name 속성은 nullable 형식으로 선언됩니다. null 값을 보유할 수 있습니다.

Kotlin은 불변 속성도 지원합니다. 불변 속성은 초기화 후 변경할 수 없는 속성입니다. Kotlin에서 불변 속성은 val 키워드를 사용하여 선언됩니다.

다음은 변경할 수 없는 속성인 name이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person(val name: String) {
  
}
```

위의 예에서 name 속성은 val(불변)로 선언됩니다. 초기화 후에는 변경할 수 없습니다.

Kotlin은 변경 가능한 속성도 지원합니다. 가변 속성은 초기화 후 변경할 수 있는 속성입니다. Kotlin에서 변경 가능한 속성은 var 키워드를 사용하여 선언됩니다.

다음은 변경 가능한 속성인 name이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person {
  
    var name: String = ""
}
```

위의 예에서 name 속성은 var(변경 가능)로 선언됩니다. 초기화 후 변경할 수 있습니다.

Kotlin은 지원 필드도 지원합니다. 지원 필드는 속성 값을 저장하는 데 사용되는 변수입니다. Kotlin에서 지원 필드는 field 키워드를 사용하여 선언됩니다.

다음은 지원 필드 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person {
  
    var name: String = ""
        private set
}
```

위의 예에서 이름 속성에는 지원 필드가 있습니다. 지원 필드는 개인 집합으로 선언되며 이는 속성의 setter에 의해서만 수정될 수 있음을 의미합니다.

Kotlin은 위임 속성도 지원합니다. 위임된 속성은 대리자 개체에 의해 구현되는 속성입니다. Kotlin에서 위임된 속성은 by 키워드를 사용하여 선언됩니다.

다음은 위임된 속성 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

위의 예에서 name 속성은 대리자 개체에 의해 구현됩니다. 대리자 개체는 람다 식에 의해 지연 초기화됩니다.

Kotlin은 확장 속성도 지원합니다. 확장 속성은 클래스의 확장으로 선언된 속성입니다. Kotlin에서 확장 속성은 by 키워드를 사용하여 선언됩니다.

다음은 확장 속성 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

위의 예에서 name 속성은 extension() 메서드를 호출하는 지연 람다 식으로 확장됩니다.

Kotlin은 후기 초기화 속성도 지원합니다. 늦게 초기화된 속성은 처음 액세스할 때까지 초기화되지 않는 속성입니다. Kotlin에서 늦게 초기화된 속성은 by 키워드를 사용하여 선언됩니다.

다음은 늦게 초기화된 속성 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person {
  
    lateinit var name: String
    
    fun init() {
        name = "John"
    }
}
```

위의 예에서 name 속성은 lateinit var(변경 가능)로 선언됩니다. init() 메서드가 호출될 때까지 초기화되지 않습니다.

Kotlin은 nullable 유형도 지원합니다. Nullable 유형은 null 값을 보유할 수 있는 유형입니다. Kotlin에서 nullable 유형은 ? 운영자.

다음은 null 허용 속성인 name이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person {
  
    var name: String? = null
}
```

위의 예에서 name 속성은 nullable 형식으로 선언됩니다. null 값을 보유할 수 있습니다.

Kotlin은 불변 속성도 지원합니다. 불변 속성은 초기화 후 변경할 수 없는 속성입니다. Kotlin에서 불변 속성은 val 키워드를 사용하여 선언됩니다.

다음은 변경할 수 없는 속성인 name이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person(val name: String) {
  
}
```

위의 예에서 name 속성은 val(불변)로 선언됩니다. 초기화 후에는 변경할 수 없습니다.

Kotlin은 변경 가능한 속성도 지원합니다. 가변 속성은 초기화 후 변경할 수 있는 속성입니다. Kotlin에서 변경 가능한 속성은 var 키워드를 사용하여 선언됩니다.

다음은 변경 가능한 속성인 name이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person {
  
    var name: String = ""
}
```

위의 예에서 name 속성은 var(변경 가능)로 선언됩니다. 초기화 후 변경할 수 있습니다.

Kotlin은 지원 필드도 지원합니다. 지원 필드는 속성 값을 저장하는 데 사용되는 변수입니다. Kotlin에서 지원 필드는 field 키워드를 사용하여 선언됩니다.

다음은 지원 필드 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person {
  
    var name: String = ""
        private set
}
```

위의 예에서 이름 속성에는 지원 필드가 있습니다. 지원 필드는 개인 집합으로 선언되며 이는 속성의 setter에 의해서만 수정될 수 있음을 의미합니다.

Kotlin은 위임 속성도 지원합니다. 위임된 속성은 대리자 개체에 의해 구현되는 속성입니다. Kotlin에서 위임된 속성은 by 키워드를 사용하여 선언됩니다.

다음은 위임된 속성 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

위의 예에서 name 속성은 대리자 개체에 의해 구현됩니다. 대리자 개체는 람다 식에 의해 지연 초기화됩니다.

Kotlin은 확장 속성도 지원합니다. 확장 속성은 클래스의 확장으로 선언된 속성입니다. Kotlin에서 확장 속성은 by 키워드를 사용하여 선언됩니다.

다음은 확장 속성 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

위의 예에서 name 속성은 extension() 메서드를 호출하는 지연 람다 식으로 확장됩니다.

Kotlin은 후기 초기화 속성도 지원합니다. 늦게 초기화된 속성은 처음 액세스할 때까지 초기화되지 않는 속성입니다. Kotlin에서 늦게 초기화된 속성은 by 키워드를 사용하여 선언됩니다.

다음은 늦게 초기화된 속성 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person {
  
    lateinit var name: String
    
    fun init() {
        name = "John"
    }
}
```

위의 예에서 name 속성은 lateinit var(변경 가능)로 선언됩니다. init() 메서드가 호출될 때까지 초기화되지 않습니다.

Kotlin은 nullable 유형도 지원합니다. Nullable 유형은 null 값을 보유할 수 있는 유형입니다. Kotlin에서 nullable 유형은 ? 운영자.

다음은 null 허용 속성인 name이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person {
  
    var name: String? = null
}
```

위의 예에서 name 속성은 nullable 형식으로 선언됩니다. null 값을 보유할 수 있습니다.

Kotlin은 불변 속성도 지원합니다. 불변 속성은 초기화 후 변경할 수 없는 속성입니다. Kotlin에서 불변 속성은 val 키워드를 사용하여 선언됩니다.

다음은 변경할 수 없는 속성인 name이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person(val name: String) {
  
}
```

위의 예에서 name 속성은 val(불변)로 선언됩니다. 초기화 후에는 변경할 수 없습니다.

Kotlin은 변경 가능한 속성도 지원합니다. 가변 속성은 초기화 후 변경할 수 있는 속성입니다. Kotlin에서 변경 가능한 속성은 var 키워드를 사용하여 선언됩니다.

다음은 변경 가능한 속성인 name이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person {
  
    var name: String = ""
}
```

위의 예에서 name 속성은 var(변경 가능)로 선언됩니다. 초기화 후 변경할 수 있습니다.

Kotlin은 지원 필드도 지원합니다. 지원 필드는 속성 값을 저장하는 데 사용되는 변수입니다. Kotlin에서 지원 필드는 field 키워드를 사용하여 선언됩니다.

다음은 지원 필드 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person {
  
    var name: String = ""
        private set
}
```

위의 예에서 이름 속성에는 지원 필드가 있습니다. 지원 필드는 개인 집합으로 선언되며 이는 속성의 setter에 의해서만 수정될 수 있음을 의미합니다.

Kotlin은 위임 속성도 지원합니다. 위임된 속성은 대리자 개체에 의해 구현되는 속성입니다. Kotlin에서 위임된 속성은 by 키워드를 사용하여 선언됩니다.

다음은 위임된 속성 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

위의 예에서 name 속성은 대리자 개체에 의해 구현됩니다. 대리자 개체는 람다 식에 의해 지연 초기화됩니다.

Kotlin은 확장 속성도 지원합니다. 확장 속성은 클래스의 확장으로 선언된 속성입니다. Kotlin에서 확장 속성은 by 키워드를 사용하여 선언됩니다.

다음은 확장 속성 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

위의 예에서 name 속성은 extension() 메서드를 호출하는 지연 람다 식으로 확장됩니다.

Kotlin은 후기 초기화 속성도 지원합니다. 늦게 초기화된 속성은 처음 액세스할 때까지 초기화되지 않는 속성입니다. Kotlin에서 늦게 초기화된 속성은 by 키워드를 사용하여 선언됩니다.

다음은 늦게 초기화된 속성 이름이 있는 Kotlin 클래스의 간단한 예입니다.

```코틀린
클래스 사람 {
  
    lateinit 변수 이름: 문자열
    
    재미있는 초기화() {
        이름 = "존"
    }
}
``