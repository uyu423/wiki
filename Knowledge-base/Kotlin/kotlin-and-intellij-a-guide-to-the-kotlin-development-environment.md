---
title: Kotlin 및 IntelliJ: Kotlin 개발 환경 가이드
description: 
published: true
date: 2023-02-01T12:23:40.941Z
tags: 
editor: markdown
dateCreated: 2023-02-01T12:23:37.503Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Kotlin and IntelliJ: A Guide to the Kotlin Development Environment***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-intellij-a-guide-to-the-kotlin-development-environment)
{.links-list}



# Kotlin과 IntelliJ: Kotlin 개발 환경 가이드

Kotlin은 자바 가상 머신에서 실행되고 Android 앱을 개발하는 데 사용할 수 있는 정적으로 유형이 지정된 프로그래밍 언어입니다. IntelliJ IDEA는 Kotlin 애플리케이션 개발에 널리 사용되는 IDE입니다. 이 가이드에서는 IntelliJ IDEA를 사용하여 Kotlin 개발 환경을 설정하는 방법을 보여줍니다.

## IntelliJ IDEA 설치

먼저 IntelliJ IDEA를 [다운로드](https://www.jetbrains.com/idea/download/)하고 설치해야 합니다. Kotlin 개발에 필요한 모든 기능이 포함된 Ultimate Edition을 권장합니다.

IntelliJ IDEA를 설치했으면 Kotlin 플러그인을 설치해야 합니다. 이렇게 하려면 IntelliJ IDEA를 열고 _Configure > Plugins_로 이동합니다. _Marketplace_ 탭에서 `Kotlin`을 검색하고 플러그인을 설치합니다.

## 새 Kotlin 프로젝트 만들기

새 Kotlin 프로젝트를 만들려면 IntelliJ IDEA를 열고 _File > New > Project_를 선택합니다. _New Project_ 마법사에서 _Kotlin > JVM > Kotlin/JVM Project_를 선택하고 _Next_를 클릭합니다.

![새로운 Kotlin/JVM 프로젝트](https://kotlinlang.org/assets/images/tools/intellij/new-kotlin-project-2.png)

_프로젝트 설정_ 페이지에서 프로젝트 이름과 위치를 지정합니다. 프로젝트 SDK 및 Kotlin 버전의 기본 설정을 사용하는 것이 좋습니다.

![프로젝트 설정](https://kotlinlang.org/assets/images/tools/intellij/new-kotlin-project-3.png)

_ Libraries_ 페이지에서 _Java SDK_를 선택하고 _Next_를 클릭합니다.

![라이브러리](https://kotlinlang.org/assets/images/tools/intellij/new-kotlin-project-4.png)

_Framework Selection_ 페이지에서 _Kotlin DSL_을 선택하고 _Finish_를 클릭합니다.

![프레임워크 선택](https://kotlinlang.org/assets/images/tools/intellij/new-kotlin-project-5.png)

## Kotlin 컴파일러 구성

기본적으로 Kotlin 컴파일러는 _Java 1.6_ 바이트코드 수준을 사용합니다. 람다와 같은 일부 Kotlin 기능에 필요한 _Java 8_로 변경하는 것이 좋습니다. 이렇게 하려면 _프로젝트 구조_ 대화 상자( _파일 > 프로젝트 구조_)를 열고 _프로젝트 설정 > 모듈 > 소스_로 이동합니다. _Kotlin Compiler_ 섹션에서 _Target bytecode version_을 _1.8_로 변경하고 _Apply_를 클릭합니다.

![프로젝트 구조](https://kotlinlang.org/assets/images/tools/intellij/project-structure-1.png)

## Kotlin 스타일 구성

Kotlin에는 다음을 권장하는 [스타일 가이드라인](https://kotlinlang.org/docs/reference/coding-conventions.html) 세트가 있습니다. IntelliJ IDEA는 코드 검사 및 빠른 수정을 제공하여 이러한 지침을 따르는 데 도움을 줄 수 있습니다. 이러한 기능을 활성화하려면 _File > Settings > Editor > Inspections_로 이동하여 _Kotlin_ 검사 프로필을 선택합니다.

![검사](https://kotlinlang.org/assets/images/tools/intellij/inspections-1.png)

## 코틀린 REPL 사용하기

Kotlin REPL(Read-Eval-Print-Loop)은 Kotlin 코드를 빠르게 테스트할 수 있는 편리한 도구입니다. Kotlin REPL을 시작하려면 _Tools_ 메뉴를 열고 _Kotlin > Kotlin REPL_을 선택합니다.

![Kotlin REPL](https://kotlinlang.org/assets/images/tools/intellij/repl-1.png)

## 결론

이 가이드에서는 IntelliJ IDEA를 사용하여 Kotlin 개발 환경을 설정하는 방법을 설명했습니다. 또한 사용 가능한 몇 가지 기본 구성 옵션 및 기능에 대해서도 다루었습니다.