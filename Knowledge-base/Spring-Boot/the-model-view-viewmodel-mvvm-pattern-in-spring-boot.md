---
title: Spring Boot의 MVVM(Model-View-ViewModel) 패턴
description: 
published: true
date: 2023-02-08T12:32:37.756Z
tags: 
editor: markdown
dateCreated: 2023-02-08T12:32:36.158Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [The Model-View-ViewModel (MVVM) Pattern in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/the-model-view-viewmodel-mvvm-pattern-in-spring-boot)
{.links-list}


# Spring Boot의 MVVM(Model-View-ViewModel) 패턴

MVVM(Model-View-ViewModel)은 애플리케이션을 Model, View 및 ViewModel의 세 가지 주요 논리적 구성 요소로 분리하는 아키텍처 설계 패턴입니다.

MVVM의 기본 아이디어는 대량의 비즈니스 로직과 데이터 조작을 View 레이어에서 ViewModel 레이어로 옮기는 것입니다. 이렇게 하면 코드를 정리하고 분리하여 애플리케이션을 보다 유지 관리하고 테스트할 수 있습니다.

그런 다음 ViewModel은 Observable을 통해 View와 관련된 데이터를 노출합니다. ViewModel은 또한 View가 바인딩할 수 있는 명령을 노출합니다. 이렇게 하면 ViewModel에 대해 알 필요 없이 ViewModel에 View에 대한 전체 제어 권한이 부여됩니다.

## 모델

모델은 애플리케이션의 데이터 및 비즈니스 로직을 나타냅니다. MVVM 애플리케이션에서 모델은 ViewModel에 대해 알지 못하므로 ViewModel에 대한 종속성이 없습니다.

모델은 애플리케이션의 데이터 관리를 담당합니다. 데이터 요청에 응답하고 데이터가 변경되면 관찰자에게 알립니다.

모델에는 애플리케이션의 비즈니스 논리도 포함됩니다. 이것은 데이터를 조작하고 애플리케이션의 비즈니스 규칙을 적용하는 논리입니다.

## 보다

View는 ViewModel에서 데이터를 표시하고 작업을 호출하는 역할을 합니다.

보기에는 데이터를 조작하거나 애플리케이션의 비즈니스 규칙을 적용하는 논리가 포함되어서는 안 됩니다. 이 논리는 ViewModel에 포함되어야 합니다.

View는 또한 ViewModel의 존재를 인식하지 않아야 합니다. ViewModel은 View와 완전히 독립적이어야 합니다.

## 뷰모델

ViewModel은 View에 데이터를 제공하고 사용자 입력을 처리하는 역할을 합니다.

ViewModel은 Observable을 통해 View에 데이터를 노출합니다. ViewModel은 또한 View가 바인딩할 수 있는 명령을 노출합니다.

ViewModel에는 데이터를 조작하고 애플리케이션의 비즈니스 규칙을 적용하는 논리가 포함되어 있습니다. ViewModel에는 View에 특정한 코드도 포함되어 있습니다.

ViewModel은 View를 인식하지 않아야 합니다. ViewModel은 View와 완전히 독립적이어야 합니다.

## 데이터 바인딩

데이터 바인딩은 View와 ViewModel이 자동으로 동기화되도록 하는 메커니즘입니다.

데이터 바인딩을 사용하면 ViewModel의 데이터가 변경될 때 ViewModel이 자동으로 View를 업데이트할 수 있습니다. 또한 데이터 결합을 통해 사용자 입력이 변경될 때 View가 ViewModel을 자동으로 업데이트할 수 있습니다.

데이터 바인딩은 양방향 프로세스입니다. View의 데이터에 대한 변경 사항은 ViewModel에 전파됩니다. ViewModel의 데이터에 대한 변경 사항은 View로 전파됩니다.

데이터 바인딩은 View와 ViewModel을 동기화된 상태로 유지하는 데 도움이 되는 강력한 메커니즘입니다.

## 결론

MVVM(Model-View-ViewModel)은 애플리케이션을 Model, View 및 ViewModel의 세 가지 주요 논리적 구성 요소로 분리하는 아키텍처 설계 패턴입니다.

MVVM의 기본 아이디어는 대량의 비즈니스 로직과 데이터 조작을 View 레이어에서 ViewModel 레이어로 옮기는 것입니다. 이렇게 하면 코드를 정리하고 분리하여 애플리케이션을 보다 유지 관리하고 테스트할 수 있습니다.

그런 다음 ViewModel은 Observable을 통해 View와 관련된 데이터를 노출합니다. ViewModel은 또한 View가 바인딩할 수 있는 명령을 노출합니다. 이렇게 하면 ViewModel에 대해 알 필요 없이 ViewModel에 View에 대한 전체 제어 권한이 부여됩니다.

데이터 바인딩은 View와 ViewModel이 자동으로 동기화되도록 하는 메커니즘입니다. 데이터 바인딩은 View와 ViewModel을 동기화된 상태로 유지하는 데 도움이 되는 강력한 메커니즘입니다.

## 참조

1. [MVVM(Model-View-ViewModel) 패턴](https://msdn.microsoft.com/en-us/library/hh848246.aspx)
2. [모델 보기 ViewModel(MVVM) 설명](https://www.codeproject.com/Articles/100175/Model-View-ViewModel-MVVM-Explained)
3. [MVVM 라이트 툴킷](http://www.mvvmlight.net/)
4. [MVVM에서 데이터 바인딩](https://www.tutorialspoint.com/mvvm/mvvm_data_binding.htm)