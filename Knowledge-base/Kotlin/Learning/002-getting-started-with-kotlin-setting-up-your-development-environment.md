---
title: 002: Kotlin 시작하기: 개발 환경 설정
description: 
published: true
date: 2023-02-16T00:33:08.019Z
tags: 
editor: markdown
dateCreated: 2023-02-16T00:32:59.905Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [002: Getting Started with Kotlin: Setting up Your Development Environment***English** document is available*](/en/Knowledge-base/Kotlin/Learning/002-getting-started-with-kotlin-setting-up-your-development-environment)
{.links-list}


# Kotlin 개발 환경 설정

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어이며 JavaScript 소스 코드로 컴파일할 수도 있습니다. Kotlin은 JetBrains에서 개발했습니다.

## 시스템 요구 사항

Kotlin에서 개발하려면 다음이 필요합니다.

- 인터넷에 연결된 컴퓨터
- IntelliJ IDEA, Android Studio 또는 Eclipse와 같은 Kotlin 개발 환경
- JDK(자바 개발 키트)

## 설치

### IntelliJ IDEA

1. [IntelliJ IDEA](https://www.jetbrains.com/idea/) 웹사이트로 이동하여 최신 버전을 다운로드합니다.
2. 지침에 따라 IntelliJ IDEA를 설치합니다.
3. IntelliJ IDEA가 설치되면 프로그램을 열고 **Create New Project**를 선택합니다.
4. **새 프로젝트** 창의 프로젝트 유형 목록에서 **Kotlin/JVM**을 선택하고 **다음**을 클릭합니다.
5. **프로젝트 SDK** 필드에서 설치한 JDK를 선택하고 **다음**을 클릭합니다.
6. **프로젝트 이름** 필드에 프로젝트 이름을 입력하고 **마침**을 클릭합니다.

### 안드로이드 스튜디오

1. [Android Studio](https://developer.android.com/studio) 웹사이트로 이동하여 최신 버전을 다운로드합니다.
2. 안내에 따라 Android Studio를 설치합니다.
3. Android Studio가 설치되면 프로그램을 열고 **Create New Project**를 선택합니다.
4. **새 프로젝트** 창의 프로젝트 유형 목록에서 **Kotlin/JVM**을 선택하고 **다음**을 클릭합니다.
5. **프로젝트 SDK** 필드에서 설치한 JDK를 선택하고 **다음**을 클릭합니다.
6. **프로젝트 이름** 필드에 프로젝트 이름을 입력하고 **마침**을 클릭합니다.

### 이클립스

1. [Eclipse](https://www.eclipse.org/) 웹사이트로 이동하여 최신 버전을 다운로드합니다.
2. 지침에 따라 Eclipse를 설치합니다.
3. Eclipse가 설치되면 프로그램을 열고 **File > New > Project**를 선택합니다.
4. **새 프로젝트** 창의 프로젝트 유형 목록에서 **Kotlin/JVM**을 선택하고 **다음**을 클릭합니다.
5. **프로젝트 SDK** 필드에서 설치한 JDK를 선택하고 **다음**을 클릭합니다.
6. **프로젝트 이름** 필드에 프로젝트 이름을 입력하고 **마침**을 클릭합니다.

## 코틀린 프로젝트 만들기

원하는 Kotlin 개발 환경을 설치했으면 Kotlin 프로젝트를 만들 수 있습니다.

### IntelliJ IDEA

1. IntelliJ IDEA에서 **파일 > 새로 만들기 > 프로젝트**를 선택합니다.
2. **새 프로젝트** 창의 프로젝트 유형 목록에서 **Kotlin/JVM**을 선택하고 **다음**을 클릭합니다.
3. **프로젝트 SDK** 필드에서 설치한 JDK를 선택하고 **다음**을 클릭합니다.
4. **프로젝트 이름** 필드에 프로젝트 이름을 입력하고 **마침**을 클릭합니다.

### 안드로이드 스튜디오

1. Android 스튜디오에서 **파일 > 새로 만들기 > 프로젝트**를 선택합니다.
2. **새 프로젝트** 창의 프로젝트 유형 목록에서 **Kotlin/JVM**을 선택하고 **다음**을 클릭합니다.
3. **프로젝트 SDK** 필드에서 설치한 JDK를 선택하고 **다음**을 클릭합니다.
4. **프로젝트 이름** 필드에 프로젝트 이름을 입력하고 **마침**을 클릭합니다.

### 이클립스

1. Eclipse에서 **파일 > 새로 만들기 > 프로젝트**를 선택합니다.
2. **새 프로젝트** 창의 프로젝트 유형 목록에서 **Kotlin/JVM**을 선택하고 **다음**을 클릭합니다.
3. **프로젝트 SDK** 필드에서 설치한 JDK를 선택하고 **다음**을 클릭합니다.
4. **프로젝트 이름** 필드에 프로젝트 이름을 입력하고 **마침**을 클릭합니다.

## Kotlin 클래스 만들기

Kotlin 프로젝트를 만든 후에는 Kotlin 클래스를 만들 수 있습니다.

### IntelliJ IDEA

1. IntelliJ IDEA에서 **파일 > 새로 만들기 > Kotlin 파일/클래스**를 선택합니다.
2. **새 Kotlin 파일/클래스** 창에서 Kotlin 클래스의 이름을 입력하고 **확인**을 클릭합니다.

### 안드로이드 스튜디오

1. Android Studio에서 **File > New > Kotlin File/Class**를 선택합니다.
2. **새 Kotlin 파일/클래스** 창에서 Kotlin 클래스의 이름을 입력하고 **확인**을 클릭합니다.

### 이클립스

1. Eclipse에서 **파일 > 새로 만들기 > Kotlin 파일/클래스**를 선택합니다.
2. **새 Kotlin 파일/클래스** 창에서 Kotlin 클래스의 이름을 입력하고 **확인**을 클릭합니다.

## Kotlin 패키지 만들기

Kotlin 패키지는 Kotlin 클래스와 개체를 구성하는 네임스페이스입니다. 패키지는 일반적으로 관련 클래스와 개체를 함께 그룹화하는 데 사용됩니다.

### IntelliJ IDEA

1. IntelliJ IDEA에서 **파일 > 새로 만들기 > 패키지**를 선택합니다.
2. **새 패키지** 창에서 Kotlin 패키지의 이름을 입력하고 **확인**을 클릭합니다.

### 안드로이드 스튜디오

1. Android 스튜디오에서 **파일 > 새로 만들기 > 패키지**를 선택합니다.
2. **새 패키지** 창에서 Kotlin 패키지의 이름을 입력하고 **확인**을 클릭합니다.

### 이클립스

1. Eclipse에서 **파일 > 새로 만들기 > 패키지**를 선택합니다.
2. **새 패키지** 창에서 Kotlin 패키지의 이름을 입력하고 **확인**을 클릭합니다.

## Kotlin 객체 생성

Kotlin 객체는 싱글톤 클래스입니다. Kotlin 객체는 하나의 인스턴스만 가질 수 있는 클래스입니다. Kotlin 객체는 속성과 함수를 포함할 수 있습니다.

### IntelliJ IDEA

1. IntelliJ IDEA에서 **파일 > 새로 만들기 > Kotlin 파일/클래스**를 선택합니다.
2. **New Kotlin File/Class** 창에서 Kotlin 객체의 이름을 입력하고 **OK**를 클릭합니다.

### 안드로이드 스튜디오

1. Android Studio에서 **File > New > Kotlin File/Class**를 선택합니다.
2. **New Kotlin File/Class** 창에서 Kotlin 객체의 이름을 입력하고 **OK**를 클릭합니다.

### 이클립스

1. Eclipse에서 **파일 > 새로 만들기 > Kotlin 파일/클래스**를 선택합니다.
2. **New Kotlin File/Class** 창에서 Kotlin 객체의 이름을 입력하고 **OK**를 클릭합니다.

## Kotlin 함수 만들기

Kotlin 함수는 하나 이상의 매개변수를 사용하고 값을 반환하는 코드 블록입니다. 함수는 Kotlin 클래스, 객체 또는 패키지 내에서 정의할 수 있습니다.

### IntelliJ IDEA

1. IntelliJ IDEA에서 **파일 > 새로 만들기 > Kotlin 파일/클래스**를 선택합니다.
2. **New Kotlin File/Class** 창에서 Kotlin 함수의 이름을 입력하고 **OK**를 클릭합니다.

### 안드로이드 스튜디오

1. Android Studio에서 **File > New > Kotlin File/Class**를 선택합니다.
2. **New Kotlin File/Class** 창에서 Kotlin 함수의 이름을 입력하고 **OK**를 클릭합니다.

### 이클립스

1. Eclipse에서 **파일 > 새로 만들기 > Kotlin 파일/클래스**를 선택합니다.
2. **New Kotlin File/Class** 창에서 Kotlin 함수의 이름을 입력하고 **OK**를 클릭합니다.

## Kotlin 속성 만들기

Kotlin 속성은 클래스, 개체 또는 패키지와 연결된 변수입니다. 속성은 변경 가능(변경 가능)하거나 변경 불가능(변경 불가능)할 수 있습니다.

### IntelliJ IDEA

1. IntelliJ IDEA에서 **파일 > 새로 만들기 > Kotlin 파일/클래스**를 선택합니다.
2. **New Kotlin File/Class** 창에서 Kotlin 속성의 이름을 입력하고 **OK**를 클릭합니다.

### 안드로이드 스튜디오

1. Android Studio에서 **File > New > Kotlin File/Class**를 선택합니다.
2. **New Kotlin File/Class** 창에서 Kotlin 속성의 이름을 입력하고 **OK**를 클릭합니다.

### 이클립스

1. Eclipse에서 **파일 > 새로 만들기 > Kotlin 파일/클래스**를 선택합니다.
2. **New Kotlin File/Class** 창에서 Kotlin 속성의 이름을 입력하고 **OK**를 클릭합니다.

## 결론

이 문서에서는 Kotlin 개발 환경을 설정하는 방법을 배웠습니다. 또한 Kotlin 프로젝트, 클래스, 패키지, 개체, 함수 및 속성을 만드는 방법도 배웠습니다.