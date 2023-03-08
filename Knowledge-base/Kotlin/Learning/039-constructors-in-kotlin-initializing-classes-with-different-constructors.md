---
title: 039: Kotlin의 생성자: 다른 생성자로 클래스 초기화
description: 
published: true
date: 2023-02-16T11:32:51.436Z
tags: 
editor: markdown
dateCreated: 2023-02-16T11:32:49.860Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [039: Constructors in Kotlin: Initializing Classes with Different Constructors***English** document is available*](/en/Knowledge-base/Kotlin/Learning/039-constructors-in-kotlin-initializing-classes-with-different-constructors)
{.links-list}


# 039: Kotlin의 생성자: 다른 생성자로 클래스 초기화

Kotlin은 클래스 초기화와 관련하여 다양한 옵션을 제공합니다. 이 게시물에서는 Kotlin의 생성자를 살펴보고 다른 값으로 클래스를 초기화하는 데 어떻게 사용할 수 있는지 살펴보겠습니다.

생성자는 클래스를 초기화하는 데 사용되는 특수 함수입니다. Kotlin에는 기본 생성자와 보조 생성자라는 두 가지 유형의 생성자가 있습니다. 기본 생성자는 클래스가 처음 생성될 때 초기화하는 데 사용되는 생성자입니다. 클래스 본문보다 먼저 클래스 맨 위에 선언됩니다.

보조 생성자는 다른 값으로 클래스를 초기화하는 데 사용됩니다. 이들은 클래스 본문 내부에 선언됩니다.

클래스는 여러 보조 생성자를 가질 수 있지만 모두 기본 생성자를 호출해야 합니다. 이렇게 하면 클래스가 항상 최소한의 기본값으로 초기화됩니다.

기본 생성자로 클래스를 만들려면 'class'라는 키워드 뒤에 클래스 이름을 사용합니다. 그런 다음 괄호 안에 기본 생성자를 선언합니다. 기본 생성자 내에서 원하는 수의 매개변수를 선언할 수 있습니다. 이러한 매개변수는 val 또는 var일 수 있습니다.

```kotlin
class MyClass(val param1: String, var param2: Int) {

}
```

위의 예에서는 두 개의 매개 변수를 사용하는 기본 생성자로 `MyClass`라는 클래스를 만들었습니다. 첫 번째 매개변수는 `val`이고 두 번째 매개변수는 `var`입니다.

기본 생성자 없이 클래스를 만들 수도 있습니다. 이 경우 클래스는 각 매개변수의 기본값으로 초기화됩니다.

```kotlin
class MyClass {

}
```

보조 생성자를 생성하려면 'constructor' 키워드와 괄호 안의 매개변수를 사용합니다. 그런 다음 보조 생성자의 본문 내에서 다른 값으로 클래스를 초기화할 수 있습니다.

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

}
```

위의 예에서는 단일 매개변수를 사용하는 보조 생성자를 만들었습니다. 이 생성자는 기본 생성자를 호출하고 두 번째 매개 변수의 기본값을 전달합니다.

여러 보조 생성자를 사용하여 클래스를 만들 수도 있습니다. 이 경우 각 보조 생성자는 서로 다른 보조 생성자를 호출해야 합니다.

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

위의 예에서는 두 개의 보조 생성자가 있는 클래스를 만들었습니다. 첫 번째 생성자는 기본 생성자를 호출하고 두 번째 생성자는 첫 번째 보조 생성자를 호출합니다.

기본 생성자와 여러 보조 생성자를 사용하여 클래스를 만들 수도 있습니다. 이 경우 각 보조 생성자는 기본 생성자를 호출해야 합니다.

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

위의 예에서는 기본 생성자와 두 개의 보조 생성자가 있는 클래스를 만들었습니다. 첫 번째 보조 생성자는 기본 생성자를 호출하고 두 번째 보조 생성자는 첫 번째 보조 생성자를 호출합니다.

기본 생성자와 여러 보조 생성자를 사용하여 클래스를 만들 수도 있습니다. 이 경우 각 보조 생성자는 서로 다른 보조 생성자를 호출해야 합니다.

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

위의 예에서는 기본 생성자와 두 개의 보조 생성자가 있는 클래스를 만들었습니다. 첫 번째 보조 생성자는 기본 생성자를 호출하고 두 번째 보조 생성자는 첫 번째 보조 생성자를 호출합니다.

기본 생성자와 여러 보조 생성자를 사용하여 클래스를 만들 수도 있습니다. 이 경우 각 보조 생성자는 기본 생성자를 호출해야 합니다.

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

위의 예에서는 기본 생성자와 두 개의 보조 생성자가 있는 클래스를 만들었습니다. 첫 번째 보조 생성자는 기본 생성자를 호출하고 두 번째 보조 생성자는 첫 번째 보조 생성자를 호출합니다.