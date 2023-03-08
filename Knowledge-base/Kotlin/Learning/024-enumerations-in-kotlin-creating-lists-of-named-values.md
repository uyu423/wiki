---
title: 024: Kotlin의 열거형: 명명된 값 목록 만들기
description: 
published: true
date: 2023-02-16T07:33:05.551Z
tags: 
editor: markdown
dateCreated: 2023-02-16T07:32:57.678Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [024: Enumerations in Kotlin: Creating Lists of Named Values***English** document is available*](/en/Knowledge-base/Kotlin/Learning/024-enumerations-in-kotlin-creating-lists-of-named-values)
{.links-list}


# Kotlin의 열거형: 명명된 값 목록 만들기

Kotlin의 열거형은 이름이 지정된 값 목록을 만들기 위한 강력한 도구입니다. 열거형을 사용하면 코드에서 사용할 수 있는 형식이 안전한 불변 값 목록을 만들 수 있습니다.

열거형은 ```enum``` 키워드를 사용하여 선언됩니다. 열거형의 각 값을 ```enum 상수```라고 합니다. 열거형 상수는 쉼표로 구분됩니다.

다음은 Kotlin에서 열거형의 간단한 예입니다.

```kotlin
enum class Color {
    RED,
    GREEN,
    BLUE
}
```

이 예에서는 색상 열거를 만들었습니다. ```enum``` 키워드는 열거형을 선언하는 데 사용되고 ```class``` 키워드는 열거형 상수를 만드는 데 사용됩니다.

열거형은 변경할 수 없습니다. 즉, 일단 생성되면 변경할 수 없습니다. 이렇게 하면 코드에서 안전하게 사용할 수 있습니다.

열거형은 Kotlin에서 여러 가지 방법으로 사용할 수 있습니다. 이 게시물에서는 코드에서 열거형을 사용할 수 있는 몇 가지 방법을 살펴보겠습니다.

## 열거형 사용

열거형은 Kotlin에서 여러 가지 방법으로 사용할 수 있습니다. 이 섹션에서는 코드에서 열거형을 사용할 수 있는 몇 가지 방법을 살펴보겠습니다.

### 스위치 문

열거형은 Kotlin의 ```when``` 문에서 사용할 수 있습니다. ```When``` 문은 가능한 값 목록과 값을 일치시킬 수 있는 일종의 ```switch``` 문입니다.

다음은 열거형을 사용하는 ```when``` 문의 예입니다.

```kotlin
fun getColor(color: Color): String {
    when (color) {
        Color.RED -> return "Red"
        Color.GREEN -> return "Green"
        Color.BLUE -> return "Blue"
    }
}
```kotlin
val color: Color = Color.valueOf("RED")
```Color``` 열거형을 인수로 사용하는 함수를 만들었습니다. 그런 다음 ```when``` 문을 사용하여 가능한 값 목록에 대해 ```color```를 일치시킵니다.

```kotlin
for (color in Color.values()) {
    println(color)
}
```for``` 루프를 사용하여 반복할 수 있습니다. ```for``` 루프는 열거형의 모든 열거형 상수를 반복합니다.

다음은 열거형을 반복하는 방법의 예입니다.

```
RED
GREEN
BLUE
```

이 예제에서는 ```for``` 루프를 사용하여 ```Color``` 열거형을 반복합니다. 열거형의 각 값을 콘솔에 출력합니다.

이 코드는 콘솔에 다음을 인쇄합니다.

```kotlin
if (Color.RED in Color.values()) {
    println("Color.RED is in the Color enumeration")
}
```

### Enum 값 확인

```
Color.RED is in the Color enumeration
```코틀린
if (Color.values()의 Color.RED) {
    println("Color.RED는 Color 열거형에 있습니다.")
}
```

이 예제에서는 ```in``` 키워드를 사용하여 ```Color``` 열거형에 ```Color.RED``` 열거형 상수가 포함되어 있는지 확인합니다.

```kotlin
enum class MyEnum {
    FIRST_VALUE,
    SECOND_VALUE
}
```
Color.RED는 Color 열거형에 있습니다.
```kotlin
enum class MyEnum {
    FIRST_VALUE {
        override val property: Int
            get() = 1
    },
    SECOND_VALUE {
        override val property: Int
            get() = 2
    }

    abstract val property: Int
}
```valueOf()``` 함수를 사용하여 이름으로 enum 상수를 얻을 수 있습니다.

다음은 이름으로 enum 상수를 얻는 방법의 예입니다.

```kotlin
enum class MyEnum {
    FIRST_VALUE {
        override fun method(): String {
            return "First Value"
        }
    },
    SECOND_VALUE {
        override fun method(): String {
            return "Second Value"
        }
    }

    abstract fun method(): String
}
```

이 예제에서는 ```valueOf()``` 함수를 사용하여 ```Color``` 열거형에서 ```Color.RED``` 열거형 상수를 가져옵니다.

### 나만의 열거형 만들기

표준 Kotlin 열거형 외에도 고유한 사용자 지정 열거형을 만들 수도 있습니다.

다음은 사용자 지정 열거형을 만드는 방법의 예입니다.

```코틀린
열거형 클래스 MyEnum {
    FIRST_VALUE,
    SECOND_VALUE
}
```

이 예에서는 ```MyEnum```이라는 사용자 지정 열거형을 만들었습니다. 이 열거에는 ```FIRST_VALUE``` 및 ```SECOND_VALUE```의 두 값이 포함됩니다.

사용자 지정 속성 및 메서드를 사용하여 열거형을 만들 수도 있습니다.

다음은 사용자 지정 속성을 사용하여 열거형을 만드는 방법의 예입니다.

```코틀린
열거형 클래스 MyEnum {
    FIRST_VALUE {
        val 속성 재정의: Int
            가져오기() = 1
    },
    SECOND_VALUE {
        val 속성 재정의: Int
            가져오기() = 2
    }

    추상 값 속성: Int
}
```

이 예에서는 ```property```라는 사용자 지정 속성을 사용하여 열거형을 만들었습니다. 이 속성은 각 열거형 상수에 의해 재정의되어야 하는 ```추상``` 속성입니다.

이 예에서는 ```FIRST_VALUE``` 및 ```SECOND_VALUE``` enum 상수에 대한 ```property``` 속성을 재정의했습니다.

사용자 지정 메서드를 사용하여 열거형을 만들 수도 있습니다.

다음은 사용자 지정 메서드를 사용하여 열거형을 만드는 방법의 예입니다.

```코틀린
열거형 클래스 MyEnum {
    FIRST_VALUE {
        재정의 재미있는 방법(): 문자열 {
            "첫 번째 값" 반환
        }
    },
    SECOND_VALUE {
        재정의 재미있는 방법(): 문자열 {
            "두 번째 값" 반환
        }
    }

    추상적인 재미 메서드(): 문자열
}
```

이 예제에서는 ```method()```라는 사용자 지정 메서드를 사용하여 열거형을 만들었습니다. 이 메소드는 각각의 enum 상수로 재정의되어야 하는 ```추상``` 메소드입니다.

이 예제에서는 ```FIRST_VALUE``` 및 ```SECOND_VALUE``` 열거형 상수에 대해 ```method()``` 메서드를 재정의했습니다.

열거형은 Kotlin에서 명명된 값 목록을 생성하는 강력한 도구입니다. 열거형을 사용하면 코드에서 사용할 수 있는 형식이 안전한 불변 값 목록을 만들 수 있습니다.