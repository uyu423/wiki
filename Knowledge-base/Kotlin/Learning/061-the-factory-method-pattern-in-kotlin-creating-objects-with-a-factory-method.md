---
title: 061: Kotlin의 팩토리 메소드 패턴: 팩토리 메소드로 객체 생성
description: 
published: true
date: 2023-01-31T09:04:58.712Z
tags: 
editor: markdown
dateCreated: 2023-01-31T09:04:57.087Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [061: The Factory Method Pattern in Kotlin: Creating Objects with a Factory Method***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/061-the-factory-method-pattern-in-kotlin-creating-objects-with-a-factory-method)
{.links-list}




# 061: Kotlin의 팩토리 메소드 패턴: 팩토리 메소드로 객체 만들기

소프트웨어 개발에서 팩토리 메소드 패턴은 팩토리 메소드를 사용하여 생성될 객체의 정확한 클래스를 지정하지 않고도 객체 생성 문제를 처리하는 생성 설계 패턴입니다. 이는 생성자를 호출하는 대신 팩터리 메서드를 통해 개체를 생성하여 수행됩니다.

이 기사에서는 팩토리 메소드 패턴과 이를 Kotlin에서 사용하여 객체를 생성하는 방법에 대해 설명합니다. 또한 이 패턴이 실제로 어떻게 사용될 수 있는지 보여주기 위해 몇 가지 코드 예제를 살펴보겠습니다.

# # 팩토리 메소드 패턴이란?

팩토리 메소드 패턴은 생성될 객체의 정확한 클래스를 지정하지 않고도 객체 생성 문제를 처리하기 위해 팩토리 메소드를 사용하는 생성 디자인 패턴입니다. 이는 생성자를 호출하는 대신 팩터리 메서드를 통해 개체를 생성하여 수행됩니다.

팩토리 메소드 패턴은 가상 생성자 패턴 및 팩토리 패턴이라고도 합니다. 객체 생성의 세부 사항을 추상화하고 클래스 이름을 하드 코딩할 필요 없이 새 객체를 생성할 수 있도록 하는 데 사용됩니다.

# # 팩토리 메소드 패턴은 어떻게 작동합니까?

팩토리 메소드 패턴은 작동하기 위해 상속에 의존합니다. 객체를 생성하기 위한 인터페이스 또는 추상 클래스를 정의하고, 인터페이스를 구현하거나 추상 클래스에서 상속하여 실제로 객체를 생성하는 구체적인 하위 클래스를 정의합니다.

Factory Method Pattern에 의해 생성된 객체를 사용하는 클라이언트 코드는 객체를 생성하는 데 사용되는 구체적인 클래스를 알거나 신경 쓸 필요가 없으며 인터페이스 또는 추상 클래스만 알면 됩니다.

# # 팩토리 메소드 패턴을 사용하는 경우

팩토리 메소드 패턴은 다음과 같은 상황에서 사용할 수 있습니다.

- 생성할 객체를 미리 알 수 없는 경우
- 생성할 객체를 사용할 코드의 다른 부분에서 생성해야 하는 경우
- 런타임까지 알 수 없는 데이터로부터 생성할 객체를 생성해야 하는 경우

# # 팩토리 메소드 패턴의 장점

팩토리 메소드 패턴에는 다음과 같은 이점이 있습니다.

- 클래스 이름을 하드 코딩하지 않고도 객체를 생성할 수 있습니다.
- 객체가 사용될 코드의 다른 부분에서 객체를 생성할 수 있습니다.
- 런타임까지 알려지지 않은 데이터에서 개체를 생성할 수 있습니다.

# # 팩토리 메소드 패턴의 단점

팩토리 메소드 패턴에는 다음과 같은 단점이 있습니다.

- 코드를 읽고 이해하기 어렵게 만들 수 있습니다.
- 코드를 디버깅하기 어렵게 만들 수 있습니다.
- 많은 코드 중복이 발생할 수 있습니다.

# # 코틀린 구현

Kotlin은 Factory Method Pattern을 기본적으로 지원하지 않지만 Kotlin에서 구현할 수 있습니다.

Kotlin에서 Factory Method Pattern을 구현하는 한 가지 방법은 컴패니언 객체를 사용하는 것입니다. 컴패니언 개체는 클래스와 연결된 개체입니다. 클래스는 컴패니언 객체를 하나만 가질 수 있으며 그 반대도 마찬가지입니다.

컴패니언 개체는 다음과 같이 팩토리 메서드 패턴을 구현하는 데 사용할 수 있습니다.

```kotlin
interface Shape {
    fun draw()
}

class Circle : Shape {
    override fun draw() {
        println("Circle.draw()")
    }
}

class Rectangle : Shape {
    override fun draw() {
        println("Rectangle.draw()")
    }
}

class Triangle : Shape {
    override fun draw() {
        println("Triangle.draw()")
    }
}

object ShapeFactory {
    fun getShape(shapeType: String): Shape? {
        if (shapeType == null) {
            return null
        }
        if (shapeType.equals("CIRCLE", ignoreCase = true)) {
            return Circle()
        } else if (shapeType.equals("RECTANGLE", ignoreCase = true)) {
            return Rectangle()
        } else if (shapeType.equals("TRIANGLE", ignoreCase = true)) {
            return Triangle()
        }
        return null
    }
}
```

위의 코드에서 우리는 Shape 인터페이스와 Shape 인터페이스를 구현하는 세 개의 구체적인 클래스를 정의했습니다. 우리는 또한 팩토리 메서드 getShape()를 포함하는 컴패니언 객체 ShapeFactory를 정의했습니다. 이 팩터리 메서드는 문자열 매개 변수 shapeType을 사용하고 Shape 유형의 개체를 반환합니다.

다음과 같이 ShapeFactory 동반 객체를 사용할 수 있습니다.

```kotlin
val circle = ShapeFactory.getShape("CIRCLE")
circle?.draw()

val rectangle = ShapeFactory.getShape("RECTANGLE")
rectangle?.draw()

val triangle = ShapeFactory.getShape("TRIANGLE")
triangle?.draw()
```

위의 코드에서 우리는 ShapeFactory 컴패니언 객체를 사용하여 각 유형별로 하나씩 세 개의 객체를 생성했습니다. 그런 다음 각 개체에 대해 draw() 메서드를 호출하여 해당 유형을 표시했습니다.

또는 객체 선언을 사용하여 다음과 같이 Factory 메서드 패턴을 구현할 수 있습니다.

```kotlin
interface Shape {
    fun draw()
}

class Circle : Shape {
    override fun draw() {
        println("Circle.draw()")
    }
}

class Rectangle : Shape {
    override fun draw() {
        println("Rectangle.draw()")
    }
}

class Triangle : Shape {
    override fun draw() {
        println("Triangle.draw()")
    }
}

object ShapeFactory {
    fun getShape(shapeType: String): Shape? {
        if (shapeType == null) {
            return null
        }
        if (shapeType.equals("CIRCLE", ignoreCase = true)) {
            return Circle()
        } else if (shapeType.equals("RECTANGLE", ignoreCase = true)) {
            return Rectangle()
        } else if (shapeType.equals("TRIANGLE", ignoreCase = true)) {
            return Triangle()
        }
        return null
    }
}

fun main(args: Array<String>) {
    val circle = ShapeFactory.getShape("CIRCLE")
    circle?.draw()

    val rectangle = ShapeFactory.getShape("RECTANGLE")
    rectangle?.draw()

    val triangle = ShapeFactory.getShape("TRIANGLE")
    triangle?.draw()
}
```

위의 코드에서 우리는 팩토리 메서드 getShape()를 포함하는 객체 선언 ShapeFactory를 정의했습니다. 이 팩터리 메서드는 문자열 매개 변수 shapeType을 사용하고 Shape 유형의 개체를 반환합니다.

다음과 같이 ShapeFactory 객체를 사용할 수 있습니다.

```kotlin
val circle = ShapeFactory.getShape("CIRCLE")
circle?.draw()

val rectangle = ShapeFactory.getShape("RECTANGLE")
rectangle?.draw()

val triangle = ShapeFactory.getShape("TRIANGLE")
triangle?.draw()
```

위의 코드에서 우리는 ShapeFactory 객체를 사용하여 각 유형별로 하나씩 세 개의 객체를 생성했습니다. 그런 다음 각 개체에 대해 draw() 메서드를 호출하여 해당 유형을 표시했습니다.

# # 추상 팩토리 패턴과의 비교

추상 팩토리 패턴은 팩토리 메소드 패턴과 유사하지만 목적이 다릅니다. 추상 팩토리 패턴은 관련 객체 또는 종속 객체의 패밀리를 생성하는 데 사용되는 반면, 팩토리 메서드 패턴은 개별 객체를 생성하는 데 사용됩니다.

추상 팩토리 패턴은 팩토리 메소드 패턴보다 더 복잡합니다. 추상 팩토리 패턴에는 하나 이상의 구체적인 팩토리가 필요하지만 팩토리 메소드 패턴에는 하나의 구체적인 팩토리만 필요합니다.

# # 결론

이 기사에서는 팩토리 메소드 패턴과 Kotlin에서 이를 사용하여 객체를 생성하는 방법에 대해 논의했습니다. 또한 이 패턴이 실제로 어떻게 사용될 수 있는지 보여주기 위해 몇 가지 코드 예제를 살펴보았습니다.