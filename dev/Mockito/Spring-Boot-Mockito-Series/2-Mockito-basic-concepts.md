---
title: [Spring Boot + Mockito] 02. Mockito 기본 개념
description: 
published: true
date: 2023-09-15T10:12:15.354Z
tags: java, mockito, springboot
editor: markdown
dateCreated: 2023-09-15T08:57:56.887Z
---

# 2.1. Mocking 이란?

Mocking은 소프트웨어 개발의 테스트 영역에서 주요한 개념 중 하나입니다. Mocking의 기본 아이디어는 복잡한 실제 객체 대신 단순화된 가짜 객체를 사용하여 특정 기능 또는 동작을 시뮬레이트하는 것입니다. 이로써, 개발자는 특정 컴포넌트나 기능에 집중하여 테스트할 수 있습니다.

## 왜 Mocking이 필요한가?

1. **격리된 테스트 환경 제공**: 외부 서비스, 데이터베이스, 네트워크 통신 등과 같은 의존성을 갖는 코드를 테스트할 때, 해당 의존성들로 인해 테스트가 불안정해질 수 있습니다. Mocking을 통해 이러한 의존성을 격리하고, 원하는 상황과 데이터를 제공할 수 있습니다.

1. **테스트 속도 향상**: 실제 객체나 서비스를 사용하는 것보다 Mock 객체를 사용하여 테스트하는 것이 훨씬 빠르다. 이를 통해 개발자는 빠른 피드백 루프를 유지하며 테스트 주도 개발(TDD)를 효과적으로 수행할 수 있습니다.

1. **복잡한 상황 시뮬레이션**: 예외 처리나 특정 상황을 재현하기 위해 실제 환경을 조작하는 것은 번거롭습니다. Mocking을 통해 이러한 상황을 쉽게 시뮬레이트하고 검증할 수 있습니다.

## Mocking과 Spring Boot

Spring Boot 환경에서는 다양한 의존성과 컴포넌트를 관리하며, 이들 간의 상호 작용이 복잡할 수 있습니다. Mockito와 같은 Mocking 도구를 사용하면, 이러한 복잡성을 크게 줄이면서 각 컴포넌트를 격리하여 테스트할 수 있습니다.

## Mocking의 핵심 개념

1. **Mock 객체**: 원하는 방식으로 동작하도록 프로그래밍된 가짜 객체입니다. 이 객체는 실제 객체와 동일한 인터페이스를 가질 수 있으며, 테스트 중에 실제 객체의 위치를 대신할 수 있습니다.

1. **Stubbing**: Mock 객체가 어떻게 동작해야 하는지 정의하는 것입니다. 예를 들어, 특정 메서드 호출에 대해 원하는 값을 반환하도록 설정할 수 있습니다.

1. **Verification**: 테스트가 실행된 후 Mock 객체의 특정 메서드가 어떻게, 몇 번 호출되었는지 검증하는 것입니다.

Mocking은 테스트의 격리, 통제, 그리고 속도 향상을 위한 필수적인 도구입니다. Spring Boot 환경에서 Mockito를 활용하면, 어플리케이션의 각 부분을 격리하고 효과적으로 테스트하는 것이 가능해집니다. 다음 섹션에서는 Mocking의 다양한 방법, 즉 Stubbing, Spying 등의 개념과 그 차이점에 대해 더 깊게 살펴보겠습니다.

# 2.2. Stubbing vs Mocking vs Spying
Mockito를 이해하고 효과적으로 활용하기 위해서는 기본 개념인 Stubbing(스터빙), Mocking(모킹), 그리고 Spying(스파잉)의 차이를 명확하게 파악하는 것이 중요합니다. 이 세 가지 기법은 테스트 케이스를 작성할 때 필수적이며, 각각 특별한 목적과 활용 방안이 있습니다. 이 섹션에서는 이러한 기본 개념의 차이와 Spring Boot 환경에서의 활용 방법에 대해 살펴보겠습니다.

##  Stubbing (스터빙, Stubbing)

- **정의**: Stubbing은 Mock 객체의 메서드 호출에 대한 예상된 반응, 즉 반환 값을 미리 설정하는 작업을 의미합니다. 이를 통해 개발자는 특정 상황에 대한 테스트를 쉽게 구성할 수 있습니다.

- **활용 예**: 데이터베이스 연결이나 외부 API 호출과 같은 복잡한 연산을 생략하고 원하는 결과를 직접 지정할 수 있습니다.

- **Spring Boot에서의 활용**: Repository나 Service 클래스의 메서드를 Stubbing하여 DB 연결 없이 원하는 결과를 반환하도록 설정할 수 있습니다.

##  Mocking (모킹, Mocking)

- **정의**: Mocking은 실제 구현을 갖지 않는 가상의 객체를 생성하는 작업을 의미합니다. 이 객체는 특정 인터페이스나 클래스를 모방(Mock)하며, Stubbing을 통해 원하는 동작을 지정할 수 있습니다.

- **활용 예**: 외부 서비스나 다른 시스템과의 연동, 그리고 비용이 많이 드는 연산을 제외하고 테스트를 진행할 때 유용합니다.

- **Spring Boot에서의 활용**: Repository, Service, Controller 등의 컴포넌트를 Mock 객체로 생성하여 테스트 환경에서의 동작을 단순화할 수 있습니다.

##  Spying (스파잉, Spying)

- **정의**: Spying은 실제 객체를 기반으로 Mock 객체를 생성하는 작업입니다. Spy 객체는 실제 객체의 모든 기능을 그대로 가지며, 필요한 경우만 특정 메서드를 Stubbing하여 동작을 변경할 수 있습니다.

- **활용 예**: 실제 객체의 대부분의 동작을 그대로 유지하면서, 일부 메서드만 변경하여 테스트를 진행하고자 할 때 사용됩니다.

- **Spring Boot에서의 활용**: 실제 DB 연동과 같은 일부 동작을 유지하면서, 특정 메서드만 Stubbing하여 테스트의 복잡성을 줄일 수 있습니다.

> Stubbing, Mocking, 그리고 Spying은 Mockito를 활용한 테스트 작성의 핵심이며, 각 기법은 테스트 케이스의 요구 사항과 복잡성에 따라 선택하게 됩니다. Spring Boot 환경에서는 이러한 기법들을 적절히 조합하여, 더욱 견고하고 효율적인 테스트 케이스를 작성할 수 있습니다.

# 2.3. Mockito 핵심 API 소개
Mockito는 풍부한 API 집합을 제공하여 다양한 상황에서의 테스트 구성을 지원합니다. 이 섹션에서는 Spring Boot 환경에서 Mockito를 활용할 때 자주 사용되는 핵심 API들에 대해 소개하겠습니다.

## 1. Mock 객체 생성

- `@Mock`: 클래스나 인터페이스의 Mock 객체를 생성합니다.

```java
@Mock
private SampleService sampleService;
mock(Class<T> classToMock): 주어진 클래스의 Mock 객체를 생성합니다.
```

```java
SampleService sampleService = mock(SampleService.class);
```

## 2.Stubbing 메소드

- when(...).thenReturn(...): Mock 메소드가 호출될 때 반환할 값을 지정합니다.

```java
when(sampleService.getSample()).thenReturn("Hello Mockito!");
```

- when(...).thenThrow(...): Mock 메소드가 호출될 때 예외를 발생시킵니다.

```java
when(sampleService.getSample()).thenThrow(new RuntimeException());
```

## 3. 메소드 호출 검증

- verify(...): Mock 객체의 특정 메소드가 호출되었는지 검증합니다.

```java
verify(sampleService).getSample();
verify(..., times(N)): 메소드가 N번 호출되었는지 검증합니다.
```

```java
verify(sampleService, times(2)).getSample();
```

## 4. Spying

- `@Spy`: 실제 객체를 기반으로 Spy 객체를 생성합니다.

```java
@Spy
private SampleService realSampleService = new SampleServiceImpl();
```

- spy(Object object): 주어진 객체를 기반으로 Spy 객체를 생성합니다.

```java
SampleService spyService = spy(new SampleServiceImpl());
```

## 5. Argument Matchers

- `any()`: 어떠한 값도 허용하는 Argument Matcher입니다.

```java
when(sampleService.getDetail(any())).thenReturn("Detail Info");
```

- eq(...): 특정 값과 동일한 Argument를 허용합니다.

```java
when(sampleService.getDetail(eq("Specific"))).thenReturn("Specific Detail Info");
```

## 6. Mocking Void 메소드

- `doNothing()`, `doThrow(...)`, `doAnswer(...)`: void 메소드를 Stubbing할 때 사용합니다.

```java
doNothing().when(sampleService).performTask();
doThrow(new RuntimeException()).when(sampleService).performTask();
```

> Mockito의 핵심 API는 간결하면서도 강력합니다. 위의 API들을 익혀두면 대부분의 테스트 시나리오에서 원하는 행동을 Mock 객체에 적용할 수 있습니다. 그러나 Mockito의 기능은 이것보다 훨씬 더 다양하므로, 본 핸드북에서는 가장 자주 사용되는 핵심 기능들만 간략하게 소개하였습니다.

다음 섹션에서는 이러한 Mockito의 기본 기능들을 활용하여 실제로 Spring Boot 프로젝트에서 어떻게 테스트 코드를 작성하는지에 대해 살펴보겠습니다.
