---
title: 096: Kotlin으로 모바일 개발: Kotlin 및 Android/iOS로 모바일 앱 빌드
description: 
published: true
date: 2023-02-14T12:18:36.616Z
tags: 
editor: markdown
dateCreated: 2023-02-14T12:18:29.042Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [096: Mobile Development in Kotlin: Building Mobile Apps with Kotlin and Android/iOS***English** document is available*](/en/Knowledge-base/Kotlin/Learning/096-mobile-development-in-kotlin-building-mobile-apps-with-kotlin-and-androidios)
{.links-list}


# 096: Kotlin으로 모바일 개발: Kotlin 및 Android/iOS로 모바일 앱 빌드

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어이며 JavaScript 소스 코드로 컴파일할 수도 있습니다. Kotlin은 IntelliJ IDEA Java IDE를 만든 회사인 JetBrains에서 개발했습니다.

Kotlin은 개선된 Java 버전으로 설계되었으며 Java에 없는 여러 기능을 제공합니다. Kotlin은 Java와 완벽하게 상호 운용되므로 Android 앱을 개발하는 데 사용할 수 있습니다.

이 게시물에서는 Kotlin 및 Android 개발을 시작하는 방법을 살펴보겠습니다. 간단한 "Hello, World!" 앱을 다운로드한 다음 Android 기기에서 실행합니다.

## 시작하기

시작하려면 IntelliJ IDEA용 Kotlin 플러그인을 설치해야 합니다. IDE 내에서 Preferences > Plugins로 이동하고 "Kotlin"을 검색하여 이 작업을 수행할 수 있습니다.

Kotlin 플러그인이 설치되면 파일 > 새로 만들기 > 프로젝트로 이동하고 프로젝트 템플릿 목록에서 "Kotlin/JVM"을 선택하여 새 Kotlin 프로젝트를 만들 수 있습니다.

## 코틀린 프로젝트 만들기

Kotlin 프로젝트를 만든 후에는 파일 > 새로 만들기 > Kotlin 파일/클래스로 이동하여 새 Kotlin 파일을 만들 수 있습니다.

프로젝트의 src/ 디렉터리에 "HelloWorld.kt"라는 파일을 생성해 보겠습니다. 파일에 기본 기능을 추가하여 시작하겠습니다.

```kotlin
fun main(args: Array<String>) {
    println("Hello, World!")
}
```

이 함수는 문자열 "Hello, World!"를 인쇄합니다. 콘솔에.

## 앱 실행

Kotlin 앱을 실행하려면 실행 구성을 만들어야 합니다. 실행 > 구성 편집으로 이동하고 "+" 버튼을 클릭하면 됩니다.

실행 구성 유형 목록에서 "Kotlin/JVM"을 선택합니다. 구성 이름을 "Hello, World!"로 지정합니다. 메인 클래스를 "HelloWorldKt"로 설정합니다.

마지막으로 앱을 실행할 기기를 선택해야 합니다. 실행 > 구성 편집으로 이동하고 "Hello, World!"를 선택하면 됩니다. 구성. "기기" 드롭다운에서 사용하려는 기기를 선택합니다.

이제 Android 기기에서 Kotlin 앱을 실행할 준비가 되었습니다!