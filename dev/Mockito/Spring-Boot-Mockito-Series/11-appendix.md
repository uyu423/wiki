---
title: [Spring Boot + Mockito] 11. 부록 (TextureMonkey)
description: 
published: true
date: 2023-10-06T07:17:34.025Z
tags: java
editor: markdown
dateCreated: 2023-10-06T07:17:34.025Z
---

# 11.1. FixtureMonkey 라이브러리와의 결합

Mockito는 테스트를 위한 가상 객체 생성에 탁월한 도구입니다. 하지만 때로는 복잡한 데이터 구조나 다양한 상황의 데이터 셋을 준비하는 것이 어려울 수 있습니다. 이러한 문제를 해결하기 위해 FixtureMonkey라는 라이브러리가 등장하였습니다. FixtureMonkey는 객체 생성을 위한 간결하고 유연한 API를 제공하여 Mockito와 결합하여 테스트 준비를 더욱 쉽게 만들어 줍니다.

## FixtureMonkey란?

FixtureMonkey는 자바와 코틀린(JVM) 테스트 환경에서 쉽게 테스트 데이터를 생성할 수 있도록 도와주는 라이브러리입니다. 이 라이브러리는 랜덤 값, 지정된 규칙, 또는 사용자 정의 규칙에 따라 객체를 생성해 줍니다.

## Spring Boot 환경에서의 설정

FixtureMonkey는 Maven이나 Gradle을 사용하여 프로젝트에 쉽게 추가할 수 있습니다.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.github.javafaker</groupId>
    <artifactId>javafaker</artifactId>
    <version>${fixturemonkey.version}</version>
    <scope>test</scope>
</dependency>
```

```gradle
// Gradle
testImplementation 'com.github.javafaker:javafaker:${fixturemonkey.version}'
```

## FixtureMonkey의 주요 기능:

- 간단한 객체 생성: FixtureMonkey를 사용하면 복잡한 객체도 몇 줄의 코드로 쉽게 생성할 수 있습니다.

```java
Order order = FixtureMonkey.create(Order.class)
```

- 사용자 정의 값 설정: 특정 필드에 원하는 값을 주입할 수 있습니다.

```java
Order customOrder = FixtureMonkey.giveMeBuilder(Order.class)
    .set("price", 10000)
    .set("orderDate", LocalDate.now())
    .sample();
```

- 컬렉션 생성: 여러 개의 객체를 한번에 생성할 수 있습니다.

```java
List<Order> orders = FixtureMonkey.giveMeBuilder(Order.class).samples(10);
```

## FixtureMonkey와 Mockito의 결합:

FixtureMonkey를 사용하면 Mockito의 `@Mock` 또는 `@Spy`로 생성된 객체에 필요한 데이터를 쉽게 주입할 수 있습니다. 예를 들어, 서비스 레이어에서의 테스트 중에 특정 메소드가 특정 데이터를 반환하도록 모킹하고 싶을 때, FixtureMonkey로 데이터를 준비하고 Mockito의 `when(...).thenReturn(...)`을 사용하여 이 데이터를 반환하도록 설정할 수 있습니다.

```java
Order mockOrder = FixtureMonkey.create(Order.class);
when(orderRepository.findById(anyLong())).thenReturn(Optional.of(mockOrder));
```

이렇게 FixtureMonkey와 Mockito를 결합하면, 테스트 코드의 가독성과 유지보수성을 크게 향상시킬 수 있습니다.

> FixtureMonkey는 데이터 준비의 복잡함을 줄이며, Mockito와의 결합을 통해 더욱 강력한 테스트 코드를 작성할 수 있게 도와줍니다. 데이터 생성의 고민을 줄이고 더욱 집중적으로 로직의 검증에 초점을 맞출 수 있게 해 주는 FixtureMonkey를 활용하여 효과적인 테스트 환경을 구축해 보세요.
  
# 11.2. FixtureMonkey giveMe() 관련 기능 심화

이전 장에서는 FixtureMonkey 라이브러리의 기본적인 사용 방법과 그 효과에 대해 알아보았습니다. 이번 장에서는 `giveMe()` 함수를 중심으로 FixtureMonkey의 다양한 기능을 더 깊게 다뤄보겠습니다. 이 기능을 활용하면 더욱 다양하고 복잡한 테스트 케이스를 간결하게 준비할 수 있습니다.

## 기본적인 giveMe() 사용:

FixtureMonkey의 `giveMe()` 함수는 주어진 클래스의 인스턴스를 생성하는 가장 간단한 방법입니다.

```java
User user = FixtureMonkey.giveMe(User.class);
```

## 특정 속성을 가진 객체 생성:

`giveMe()` 함수와 함께 사용되는 `with()` 메소드를 사용하면, 특정 조건을 만족하는 객체를 생성할 수 있습니다.

```java
// 'John Doe'라는 이름을 가진 User 객체 생성
User john = FixtureMonkey.giveMe(User.class, with("name", "John Doe"));
```

## 제약 조건 추가:

`giveMe()` 함수에 여러 제약 조건을 추가하여 원하는 특성을 갖는 객체를 생성할 수 있습니다.

```java
// 20세 이상이며, 'Doe'라는 성을 가진 User 객체 생성
User adultDoe = FixtureMonkey.giveMe(User.class, with("age", greaterThan(20)), with("lastName", "Doe"));
```

## 커스텀 조건의 객체 생성:

`giveMe()` 함수는 사용자 정의 조건을 사용하여 객체를 생성할 수 있도록 확장성을 제공합니다.

```java
// Custom 조건을 정의
SpecimenSpec<User> isAdult = user -> user.getAge() >= 20;

User adultUser = FixtureMonkey.giveMe(User.class, isAdult);
```

## 반복적인 객체 생성:

`giveMe()`를 활용하여 일련의 객체들을 생성할 수 있습니다. 이 기능은 리스트나 배열 같은 컬렉션을 테스트할 때 유용합니다.

```java
List<User> users = FixtureMonkey.giveMeList(User.class, 10);
```

## FixtureMonkey와 Mockito의 통합:

`giveMe()` 함수로 생성된 객체는 Mockito를 활용한 테스트에서도 이용될 수 있습니다. 예를 들어, Repository에서 특정 조건을 만족하는 User 객체를 반환하도록 모킹할 때, `giveMe()`로 객체를 생성하고 `when()`과 함께 사용할 수 있습니다.

```java
User mockUser = FixtureMonkey.giveMe(User.class, with("name", "John Doe"));
when(userRepository.findByName("John Doe")).thenReturn(Optional.of(mockUser));
```

> FixtureMonkey의 `giveMe()` 함수는 테스트 데이터 생성에 있어 굉장한 유연성과 확장성을 제공합니다. 다양한 조건과 함께 사용하면, 복잡한 테스트 케이스를 간결하게 준비할 수 있습니다. 특히, Spring Boot와 Mockito 환경에서는 이러한 기능이 테스트의 품질과 효율성을 높이는 데 큰 도움이 됩니다. FixtureMonkey의 다양한 기능을 적극 활용하여 더욱 견고한 테스트 코드를 작성해보시기 바랍니다.