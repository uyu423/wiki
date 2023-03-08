---
title: Kotlin 테스트: 고급 주제 및 모범 사례
description: 
published: true
date: 2023-02-03T21:55:20.976Z
tags: 
editor: markdown
dateCreated: 2023-02-03T21:55:19.287Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin Testing: Advanced Topics and Best Practices***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-testing-advanced-topics-and-best-practices)
{.links-list}


# Kotlin 테스트: 고급 주제 및 모범 사례

Kotlin은 지난 몇 년 동안 인기를 얻고 있는 JVM 언어입니다. 간결한 구문과 강력한 기능으로 인해 많은 Android 개발자가 선택했습니다.

이 문서에서는 Kotlin 테스트의 몇 가지 고급 주제를 살펴보고 더 유지 관리하기 쉽고 읽기 쉬운 테스트를 작성하는 데 도움이 되는 몇 가지 모범 사례를 살펴봅니다.

## 목차

1. [코틀린 테스트NG](# kotlin-testng)
2. [JUnit 5](# junit-5)
3. [어설션](# assertions)
4. [모킹](# 모킹)
5. [안드로이드 테스트하기](# testing-android)

## 코틀린 테스트NG

Kotlin의 가장 인기 있는 테스트 프레임워크 중 하나는 TestNG입니다. TestNG는 많은 기능과 유연성을 제공하는 강력한 테스트 프레임워크입니다.

TestNG 사용의 장점 중 하나는 Kotlin과 함께 설정하고 사용하기 쉽다는 것입니다. 쉽게 시작할 수 있는 Kotlin TestNG 라이브러리가 많이 있습니다.

TestNG 사용의 또 다른 이점은 매개변수화된 테스트를 잘 지원한다는 것입니다. 즉, 입력 매개변수를 사용하고 출력 값을 반환하는 테스트를 쉽게 작성할 수 있습니다.

마지막으로 TestNG는 Maven 및 Gradle과 같은 널리 사용되는 많은 빌드 도구와 잘 통합됩니다. 이렇게 하면 Kotlin 테스트를 위한 지속적 통합(CI) 파이프라인을 쉽게 설정할 수 있습니다.

## JUnit 5

JUnit 5는 널리 사용되는 JUnit 테스트 프레임워크의 최신 버전입니다. JUnit 5는 람다 식 지원과 같은 많은 새로운 기능을 도입하는 주요 업데이트입니다.

JUnit 5는 Kotlin도 잘 지원합니다. 쉽게 시작할 수 있는 Kotlin JUnit 5 라이브러리가 많이 있습니다.

JUnit 5를 사용하는 이점 중 하나는 Kotlin과 함께 설정하고 사용하기 쉽다는 것입니다. 또 다른 장점은 JUnit 5가 Maven 및 Gradle과 같은 널리 사용되는 많은 빌드 도구와 잘 통합된다는 것입니다.

## 어설션

어설션은 테스트 작성의 중요한 부분입니다. 어설션을 사용하면 코드가 예상대로 작동하는지 확인할 수 있습니다.

Kotlin에서 사용할 수 있는 많은 어설션 라이브러리가 있습니다. 가장 인기 있는 어설션 라이브러리 중 일부는 AssertJ, Hamcrest 및 Truth입니다.

AssertJ는 많은 기능과 유연성을 제공하는 강력한 어설션 라이브러리입니다. Hamcrest는 보다 간결한 구문을 가진 인기 있는 어설션 라이브러리입니다. Truth는 Kotlin과 함께 사용하도록 설계된 새로운 어설션 라이브러리입니다.

## 조롱

모킹은 실제 개체의 동작을 시뮬레이션할 수 있는 기술입니다. 모킹은 종종 테스트에서 종속성 동작을 제거하는 데 사용됩니다.

Kotlin에 사용할 수 있는 조롱 프레임워크가 많이 있습니다. 가장 인기 있는 조롱 프레임워크는 Mockito, PowerMock 및 EasyMock입니다.

Mockito는 많은 기능과 유연성을 제공하는 인기 있는 조롱 프레임워크입니다. PowerMock은 모의 정적 메서드 지원과 같은 추가 기능을 제공하는 모의 프레임워크입니다. EasyMock은 Kotlin과 함께 사용하도록 설계된 간단한 모킹 프레임워크입니다.

## 안드로이드 테스트

Android는 Linux 커널을 기반으로 하는 널리 사용되는 모바일 플랫폼입니다. Android 애플리케이션은 Java 프로그래밍 언어로 작성됩니다.

Android 애플리케이션을 테스트하는 데 사용할 수 있는 많은 테스트 프레임워크가 있습니다. 가장 인기 있는 테스트 프레임워크는 Espresso, Robotium 및 Appium입니다.

Espresso는 Android 애플리케이션 테스트용으로 설계된 인기 있는 테스트 프레임워크입니다. Robotium은 Android를 포함한 여러 플랫폼 테스트를 지원하는 테스트 프레임워크입니다. Appium은 Android 애플리케이션 테스트를 지원하는 크로스 플랫폼 테스트 프레임워크입니다.

## 참조

1. [코틀린 테스트NG](https://kotlinlang.org/docs/tutorials/testing-with-testng.html)
2. [JUnit 5](https://junit.org/junit5/)
3. [AssertJ](http://joel-costigliola.github.io/assertj/)
4. [햄크레스트](http://hamcrest.org/)
5. [진실](https://github.com/google/truth)
6. [모키토](http://site.mockito.org/)
7. [파워목](http://powermock.github.io/)
8. [이지목](http://easymock.org/)
9. [에스프레소](https://developer.android.com/training/testing/espresso/)
10. [로보티움](https://github.com/RobotiumTech/robotium)
11. [아피움](http://appium.io/)