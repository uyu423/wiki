---
title: 092: Kotlin의 IntelliJ IDEA: IntelliJ IDEA IDE로 Kotlin 코드 개발
description: 
published: true
date: 2023-02-17T21:32:31.092Z
tags: 
editor: markdown
dateCreated: 2023-02-17T21:32:29.086Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [092: The IntelliJ IDEA in Kotlin: Developing Kotlin Code with the IntelliJ IDEA IDE***English** document is available*](/en/Knowledge-base/Kotlin/Learning/092-the-intellij-idea-in-kotlin-developing-kotlin-code-with-the-intellij-idea-ide)
{.links-list}


# 092: Kotlin의 IntelliJ IDEA: IntelliJ IDEA IDE로 Kotlin 코드 개발

Kotlin은 IntelliJ IDEA IDE를 만든 JetBrains에서 만든 JVM 언어입니다. Kotlin은 JVM에서 실행되고 Android 앱, 서버측 애플리케이션 등을 개발하는 데 사용할 수 있는 정적으로 유형이 지정된 언어입니다.

이 게시물에서는 IntelliJ IDEA IDE를 사용하여 Kotlin 코드를 개발하는 방법을 살펴보겠습니다. 다음 주제를 다룹니다.

* IntelliJ IDEA에서 Kotlin 플러그인 설정
* IntelliJ IDEA에서 Kotlin 프로젝트 생성
* IntelliJ IDEA에서 Kotlin 코드 작성
* IntelliJ IDEA에서 Kotlin 코드 실행

## IntelliJ IDEA에서 Kotlin 플러그인 설정

Kotlin 플러그인은 기본적으로 IntelliJ IDEA와 함께 번들로 제공되지 않습니다. 하지만 Kotlin 플러그인을 설치하는 것은 쉽습니다.

Kotlin 플러그인을 설치하려면:

1. IntelliJ IDEA를 열고 _파일 > 설정_으로 이동합니다.
2. _설정_ 창에서 _플러그인_으로 이동합니다.
3. _Plugins_ 창에서 _Browse repositories_ 버튼을 클릭합니다.
4. _Browse Repositories_ 창에서 `kotlin`을 검색합니다.
5. 검색 결과에서 _Kotlin_ 플러그인을 선택하고 _Install_ 버튼을 클릭합니다.
6. _Install Plugin_ 창에서 _Restart IntelliJ IDEA_ 버튼을 클릭합니다.

IntelliJ IDEA를 다시 시작하면 Kotlin 플러그인이 설치되고 사용할 준비가 됩니다.

## IntelliJ IDEA에서 Kotlin 프로젝트 만들기

이제 Kotlin 플러그인이 설치되었으므로 Kotlin 프로젝트를 생성해 보겠습니다.

Kotlin 프로젝트를 만들려면 다음 안내를 따르세요.

1. IntelliJ IDEA를 열고 _File > New > Project_로 이동합니다.
2. _New Project_ 창에서 _Kotlin > Kotlin/JVM_을 선택하고 _Next_ 버튼을 클릭합니다.
3. _New Kotlin/JVM Project_ 창에서 _Project name_을 입력하고 _Finish_ 버튼을 클릭합니다.

다음 구조로 새 Kotlin 프로젝트가 생성됩니다.

```
src/
    main/
        kotlin/
            Main.kt
    test/
        kotlin/
            MainTest.kt
```

## IntelliJ IDEA에서 Kotlin 코드 작성

이제 Kotlin 프로젝트가 있으므로 Kotlin 코드를 작성해 보겠습니다.

`Main.kt` 파일을 열고 내용을 다음 코드로 바꿉니다.

```kotlin
fun main(args: Array<String>) {
    println("Hello, world!")
}
```

이 코드는 "Hello, world!"를 출력합니다. 콘솔에.

이 코드를 실행하려면:

1. _실행 > '메인' 실행_으로 이동합니다.
2. _Run/Debug Configurations_ 창에서 _Run_ 버튼을 클릭합니다.

코드가 컴파일되고 실행되며 출력이 _Run_ 창에 표시됩니다.

## IntelliJ IDEA에서 Kotlin 코드 실행

IntelliJ IDEA _Run_ 창에서 Kotlin 코드를 실행할 수도 있습니다.

_Run_ 창에서 Kotlin 코드를 실행하려면:

1. _실행 > '메인' 실행_으로 이동합니다.
2. _Run/Debug Configurations_ 창에서 _Run_ 버튼을 클릭합니다.
3. _Run_ 창에서 `println("Hello, world!")`을 입력하고 _Enter_를 누릅니다.

코드가 컴파일되고 실행되며 출력이 _Run_ 창에 표시됩니다.

## 결론

이 게시물에서는 IntelliJ IDEA IDE를 사용하여 Kotlin 코드를 개발하는 방법을 살펴보았습니다. 지금까지 Kotlin 플러그인 설치 방법, Kotlin 프로젝트 생성 방법, Kotlin 코드 작성 방법, Kotlin 코드 실행 방법을 살펴보았습니다.