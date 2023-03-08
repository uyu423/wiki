---
title: 074: Kotlin의 프록시 패턴: 다른 개체에 대리자 또는 자리 표시자 제공
description: 
published: true
date: 2023-01-31T12:17:34.408Z
tags: 
editor: markdown
dateCreated: 2023-01-31T12:17:32.700Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [074: The Proxy Pattern in Kotlin: Providing a Surrogate or Placeholder for Another Object***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/074-the-proxy-pattern-in-kotlin-providing-a-surrogate-or-placeholder-for-another-object)
{.links-list}


  "리소스" 섹션에 원본 문서에 대한 링크를 추가합니다.

# 074: Kotlin의 프록시 패턴: 다른 개체에 대리자 또는 자리 표시자 제공

프록시 패턴은 서로게이트 또는 자리 표시자 개체를 다른 개체에 제공하는 소프트웨어 디자인 패턴입니다. 프록시 패턴에서 클래스는 다른 클래스의 기능을 나타냅니다. 이러한 유형의 디자인 패턴은 구조적 패턴에 속합니다.

프록시 패턴에는 네 가지 유형이 있습니다.

- 가상 프록시: 가상 프록시는 다른 개체를 나타내는 개체입니다. 예를 들어 실제 개체를 나타내는 아이콘입니다.
- 원격 프록시: 원격 프록시는 다른 주소 공간에 있는 개체에 대한 로컬 대표를 제공합니다. 예를 들어 웹 서비스에 액세스합니다.
- 보호 프록시: 보호 프록시는 중요한 마스터 개체에 대한 액세스를 제어합니다. "서로게이트" 개체는 실제 주체가 액세스되기 전에 액세스 가능한지 확인합니다.
- 스마트 프록시: 스마트 프록시는 프록시에 추가 논리를 추가합니다. 예를 들어, 참조 카운팅.

이 기사에서는 가상 프록시 패턴에 중점을 둘 것입니다.

## 가상 프록시 패턴이란 무엇입니까?

가상 프록시는 다른 개체를 나타내는 개체입니다. 실제 개체는 필요할 때만 생성됩니다. 예를 들어 원격 서버에서 로드 중인 이미지입니다. 이미지는 프록시 객체로 표현됩니다. 프록시 개체는 이미지에 대한 요청을 처리합니다. 이미지가 로드되면 프록시 개체가 실제 이미지 개체로 대체됩니다.

가상 프록시를 사용하여 다음을 수행할 수 있습니다.

- 고가의 개체 생성을 지연시켜 성능을 향상시킵니다.
- 개체의 복잡성을 숨깁니다.
- 아직 사용할 수 없는 개체에 대한 자리 표시자를 제공합니다.

## Kotlin에서 가상 프록시 패턴을 구현하는 방법은 무엇입니까?

다음 예제를 사용하여 가상 프록시 패턴을 시연합니다. 사용자를 나타내는 User 클래스가 있습니다. User 클래스에는 이름과 아바타가 있습니다. 아바타는 이미지입니다. 가상 프록시를 사용하여 아바타 이미지를 나타냅니다.

```kotlin
class User(val name: String, val avatar: Image)
```

Image 클래스는 이미지를 나타냅니다. Image 클래스에는 너비와 높이가 있습니다.

```kotlin
class Image(val width: Int, val height: Int)
```

ImageProxy 클래스는 Image 클래스의 프록시입니다. ImageProxy 클래스에는 Image 클래스에 대한 참조가 있습니다. ImageProxy 클래스에는 로딩 플래그도 있습니다. 로딩 플래그는 Image 클래스가 로딩 중인지 여부를 추적하는 데 사용됩니다.

```kotlin
class ImageProxy(val image: Image) {
    val loading = false
}
```

loadImage() 함수는 Image 클래스를 로드하는 데 사용됩니다. loadImage() 함수는 이미지 URL과 콜백 함수를 사용합니다. 콜백 함수는 이미지가 로드될 때 호출됩니다.

```kotlin
fun loadImage(imageUrl: String, callback: (Image) -> Unit) {
    // TODO: load image from URL
}
```

main() 함수는 ImageProxy 객체로 User 객체를 생성합니다. ImageProxy 개체는 아바타 이미지를 나타냅니다. loadImage() 함수는 아바타 이미지를 로드하는 데 사용됩니다. 이미지가 로드되면 ImageProxy 개체가 Image 개체로 대체됩니다.

```kotlin
fun main() {
    val user = User("Alice", ImageProxy(null))

    loadImage("avatar.jpg") { image ->
        user.avatar = image
    }
}
```

## 가상 프록시 패턴은 언제 사용하나요?

가상 프록시 패턴은 다음과 같은 경우에 사용해야 합니다.

- 개체를 만드는 것은 비용이 많이 듭니다.
- 개체가 자주 사용되지 않습니다.
- 개체를 즉시 사용할 수 없습니다.

## 가상 프록시 패턴의 장점

가상 프록시 패턴에는 다음과 같은 이점이 있습니다.

- 고가의 객체 생성을 지연시켜 성능을 향상시킵니다.
- 개체의 복잡성을 숨깁니다.

## 가상 프록시 패턴의 단점

가상 프록시 패턴에는 다음과 같은 단점이 있습니다.

- 복잡성을 유발할 수 있습니다.

## 자원

- [위키백과](https://en.wikipedia.org/wiki/Proxy_pattern)
- [소스 메이킹](https://sourcemaking.com/design_patterns/proxy)