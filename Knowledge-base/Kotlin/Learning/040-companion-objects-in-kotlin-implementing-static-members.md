---
title: 040: Kotlin의 컴패니언 객체: 정적 멤버 구현
description: 
published: true
date: 2023-02-16T12:33:00.021Z
tags: 
editor: markdown
dateCreated: 2023-02-16T12:32:58.120Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [040: Companion Objects in Kotlin: Implementing Static Members***English** document is available*](/en/Knowledge-base/Kotlin/Learning/040-companion-objects-in-kotlin-implementing-static-members)
{.links-list}




컴패니언 객체는 Kotlin에서 정적 멤버를 구현하는 좋은 방법입니다. 컴패니언 개체를 사용하면 각 정적 멤버에 대해 별도의 클래스를 만들지 않아도 됩니다.

컴패니언 개체를 만들려면 개체 선언 앞에 "companion" 키워드를 추가하기만 하면 됩니다. 예를 들어 "MyClass"라는 클래스에 대한 컴패니언 개체를 만들려면 다음 코드를 추가합니다.

```kotlin
class MyClass {
    companion object {
        // ...
    }
}
```

컴패니언 객체 내에서 원하는 정적 멤버를 추가할 수 있습니다. 예를 들어 다음과 같은 정적 필드를 추가할 수 있습니다.

```kotlin
class MyClass {
    companion object {
        val myField = "Hello, world!"
    }
}
```

정적 메소드를 추가할 수도 있습니다. 예를 들어 다음과 같이 "myMethod"라는 정적 메서드를 추가할 수 있습니다.

```kotlin
class MyClass {
    companion object {
        fun myMethod() {
            // ...
        }
    }
}
```

동반 객체의 멤버에 액세스하려면 클래스 이름 뒤에 동반 객체 이름을 사용합니다. 예를 들어 "myField" 필드에 액세스하려면 다음 코드를 사용합니다.

```kotlin
MyClass.myField // "Hello, world!"
```

"myMethod" 메서드를 호출하려면 다음 코드를 사용합니다.

```kotlin
MyClass.myMethod()
```

컴패니언 개체를 사용하는 한 가지 이점은 이름 충돌을 피할 수 있다는 것입니다. 예를 들어 "Foo"라는 클래스와 "Bar"라는 다른 클래스가 있다고 가정합니다. 두 클래스 모두 "myField"라는 정적 필드가 있는 경우 다음 코드를 사용하여 각 필드에 액세스할 수 있습니다.

```kotlin
Foo.myField // accesses the "myField" field in the "Foo" class
Bar.myField // accesses the "myField" field in the "Bar" class
```

컴패니언 개체를 사용하는 또 다른 이점은 개체 외부에서 컴패니언 개체의 전용 멤버에 액세스할 수 있다는 것입니다. 예를 들어 "myField"라는 비공개 필드가 있는 컴패니언 개체가 있다고 가정합니다.

```kotlin
class MyClass {
    companion object {
        private val myField = "Hello, world!"
    }
}
```

다음 코드를 사용하여 동반 개체 외부에서 이 필드에 액세스할 수 있습니다.

```kotlin
MyClass.Companion.myField // "Hello, world!"
```

동반 개체의 인스턴스를 반환하는 정적 팩터리 메서드를 만들려는 경우에 유용할 수 있습니다. 예를 들어 다음과 같이 "create"라는 정적 팩터리 메서드를 만들 수 있습니다.

```kotlin
class MyClass {
    companion object {
        private val myField = "Hello, world!"
        
        fun create(): MyClass {
            return MyClass()
        }
    }
}
```

그런 다음 다음 코드를 사용하여 동반 객체 외부에서 이 메서드를 호출할 수 있습니다.

```kotlin
MyClass.Companion.create() // creates and returns an instance of the "MyClass" class
```

컴패니언 개체를 사용할 때의 한 가지 단점은 코드를 읽기 어렵게 만들 수 있다는 것입니다. 예를 들어 동반 개체가 있는 "Foo"라는 클래스가 있다고 가정합니다. 동반 개체의 구성원에 액세스하려면 개체의 전체 이름을 사용해야 합니다.

```kotlin
Foo.Companion.myField // accesses the "myField" field in the "Foo" class
```

이것은 특히 컴패니언 개체의 멤버에 자주 액세스하는 경우 코드를 읽기 어렵게 만들 수 있습니다.

컴패니언 개체 사용의 또 다른 단점은 상속할 수 없다는 것입니다. 예를 들어 동반 개체가 있는 "Foo"라는 클래스가 있다고 가정합니다. "Foo"의 하위 클래스를 만드는 경우 하위 클래스는 동반 개체를 상속하지 않습니다.

```kotlin
class Foo {
    companion object {
        // ...
    }
}

class FooSubclass: Foo {
    // does not inherit the companion object from the "Foo" class
}
```

하위 클래스에서 정적 팩터리 메서드를 만들려는 경우 문제가 될 수 있습니다. 예를 들어 "FooSubclass"의 인스턴스를 반환하는 "FooSubclass"에서 정적 팩터리 메서드를 생성한다고 가정합니다. "FooSubclass"는 "Foo" 클래스에서 컴패니언 객체를 상속하지 않기 때문에 이렇게 할 수 없습니다.

```kotlin
class Foo {
    companion object {
        // ...
    }
}

class FooSubclass: Foo {
    companion object {
        fun create(): FooSubclass { // error: does not inherit the companion object from the "Foo" class
            return FooSubclass()
        }
    }
}
```

컴패니언 개체를 상속할 수 있으려면 중첩 클래스를 대신 사용할 수 있습니다. 예를 들어 다음과 같이 "Companion"이라는 중첩 클래스를 만들 수 있습니다.

```kotlin
class Foo {
    class Companion {
        // ...
    }
}
```

그런 다음 "Companion" 클래스는 하위 클래스에 의해 상속될 수 있습니다.

```kotlin
class Foo {
    class Companion {
        // ...
    }
}

class FooSubclass: Foo() {
    class Companion: Foo.Companion() {
        fun create(): FooSubclass {
            return FooSubclass()
        }
    }
}
```

요약하면 컴패니언 객체는 Kotlin에서 정적 멤버를 구현하는 좋은 방법입니다. 이름 충돌을 피할 수 있고 개체 외부에서 개인 멤버에 액세스할 수 있다는 이점이 있습니다. 그러나 읽기 어렵고 상속할 수 없다는 단점이 있습니다.