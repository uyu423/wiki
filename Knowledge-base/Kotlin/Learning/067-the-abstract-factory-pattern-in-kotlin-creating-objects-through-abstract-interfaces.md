---
title: 067: Kotlin의 추상 팩토리 패턴: 추상 인터페이스를 통해 객체 생성
description: 
published: true
date: 2023-02-06T22:17:40.556Z
tags: 
editor: markdown
dateCreated: 2023-02-06T22:17:33.765Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [067: The Abstract Factory Pattern in Kotlin: Creating Objects Through Abstract Interfaces***English** document is available*](/en/Knowledge-base/Kotlin/Learning/067-the-abstract-factory-pattern-in-kotlin-creating-objects-through-abstract-interfaces)
{.links-list}


# Kotlin의 추상 팩토리 패턴: 추상 인터페이스를 통해 객체 생성

추상 팩토리 패턴은 추상 인터페이스를 통해 객체를 생성할 수 있는 생성 디자인 패턴입니다. 이 패턴은 GUI나 데이터베이스와 같은 더 큰 시스템의 일부인 객체를 생성해야 할 때 특히 유용합니다.

이번 포스트에서는 Kotlin에서 Abstract Factory 패턴을 사용하는 방법에 대해 살펴보겠습니다. 이 패턴이 해결하는 문제부터 살펴보겠습니다. 그런 다음 Kotlin에서 패턴을 구현하는 방법을 살펴보겠습니다. 마지막으로 이 패턴을 사용할 때의 몇 가지 이점과 단점을 살펴보겠습니다.

## 문제

버튼이 있는 창으로 구성된 간단한 GUI 응용 프로그램을 고려하십시오. 다음과 같이 Abstract Factory 패턴을 사용하여 이 창을 만들 수 있습니다.

```kotlin
interface Window {
    fun draw()
}

class Button(val window: Window) {
    fun draw() {
        // ...
    }
}

class Application {
    val window: Window

    init {
        window = WindowFactory.createWindow()
    }

    fun addButton(button: Button) {
        // ...
    }
}

object WindowFactory {
    fun createWindow(): Window {
        // ...
    }
}
```

이 예제에는 창에 대한 인터페이스와 해당 인터페이스의 구체적인 구현이 있습니다. 창을 매개변수로 사용하는 버튼 클래스도 있습니다. 마지막으로 창을 만들고 여기에 버튼을 추가하는 Application 클래스가 있습니다.

추상 팩토리 패턴을 사용하면 나머지 응용 프로그램에서 창 생성을 분리할 수 있습니다. 이는 Windows 및 macOS와 같은 여러 플랫폼을 지원해야 할 때 특히 유용합니다. 우리는 단순히 각 플랫폼에 대해 새 WindowFactory를 만들 수 있으며 나머지 응용 프로그램은 이전과 같이 계속 작동합니다.

## 구현

이제 Kotlin에서 Abstract Factory 패턴을 구현하는 방법을 살펴보겠습니다. 창의 인터페이스부터 살펴보겠습니다.

```kotlin
interface Window {
    fun draw()
}
```

다음으로 Windows 플랫폼에 대한 이 인터페이스의 구체적인 구현을 만듭니다.

```kotlin
class WindowsWindow : Window {
    override fun draw() {
        // ...
    }
}
```

이제 WindowsWindow 클래스의 인스턴스를 반환하는 WindowsWindowFactory를 만들 수 있습니다.

```kotlin
class WindowsWindowFactory : WindowFactory {
    override fun createWindow(): Window {
        return WindowsWindow()
    }
}
```

이제 macOSWindow 클래스의 인스턴스를 반환할 macOSWindowFactory를 만들 수 있습니다.

```kotlin
class macOSWindowFactory : WindowFactory {
    override fun createWindow(): Window {
        return macOSWindow()
    }
}
```

마지막으로 새 WindowFactory를 사용하도록 Application 클래스를 업데이트할 수 있습니다.

```kotlin
class Application {
    val window: Window

    init {
        window = WindowFactory.createWindow()
    }

    fun addButton(button: Button) {
        // ...
    }
}
```

## 이익

추상 팩토리 패턴을 사용하면 다음과 같은 몇 가지 이점이 있습니다.

- 패턴을 사용하면 나머지 코드에서 객체 생성을 분리할 수 있습니다. 이는 여러 플랫폼을 지원해야 할 때 특히 유용합니다.

- 패턴은 확장하기 쉽습니다. 예를 들어 새 WindowFactory를 생성하여 새 플랫폼을 쉽게 추가할 수 있습니다.

- 패턴은 인터페이스 사용을 촉진합니다. 이는 코드 재사용 및 유지 관리에 도움이 될 수 있습니다.

## 단점

추상 팩토리 패턴을 사용하는 데는 몇 가지 단점도 있습니다.

- 패턴은 많은 상용구 코드로 이어질 수 있습니다.

- 패턴을 이해하고 사용하기 어려울 수 있습니다.