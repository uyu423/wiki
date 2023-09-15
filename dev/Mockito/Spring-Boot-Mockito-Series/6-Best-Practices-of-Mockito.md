---
title: [Spring Boot + Mockito] 06. Mocking의 Best Practices
description: 
published: true
date: 2023-09-15T10:14:11.491Z
tags: java, mockito, springboot, test
editor: markdown
dateCreated: 2023-09-15T09:33:03.488Z
---

# 6.1. 오버-모킹 피하기 (Over-mocking)

오버-모킹(Over-mocking)은 테스트에서 필요 이상으로 많은 객체나 메소드를 모킹하는 것을 의미합니다. 이로 인해 테스트의 가독성이 떨어지고, 필요한 부분만을 집중적으로 테스트하기 어렵게 됩니다. 오버-모킹의 주요 원인과 이를 피하는 방법에 대해 알아봅시다.

## 오버-모킹의 원인
- **복잡한 아키텍처**: 의존성이 많거나 복잡한 클래스를 테스트할 때 모킹을 과도하게 사용할 수 있습니다.
- **불필요한 모킹**: 테스트의 목적과 관련이 없는 부분까지 모킹하는 경우입니다.
- **테스트 범위의 불명확**: 어떤 부분을 집중적으로 테스트해야 할지 판단하지 못해 모든 것을 모킹하는 경우입니다.

## 오버-모킹의 문제점

- **가독성 저하**: 테스트 코드에서 많은 모킹 설정으로 인해 실제 테스트하려는 로직을 파악하기 어렵게 됩니다.
- **유지보수 어려움**: 테스트가 복잡해지면, 코드 변경 시 테스트 코드도 함께 수정해야 하는 경우가 많아집니다.
- **실제 로직 테스트 부족**: 과도한 모킹으로 인해 실제 로직이 제대로 동작하는지 확인하기 어렵습니다.

## 오버-모킹을 피하는 방법

- **필요한 부분만 모킹하기**: 테스트의 목적과 직접적으로 관련된 부분만 모킹하고, 그 외에는 실제 객체를 사용하세요.
- **@Mock과 @InjectMocks 활용**: Mockito에서 제공하는 `@Mock`과 `@InjectMocks` 어노테이션을 활용하여 테스트 대상 객체와 관련된 의존성만 모킹할 수 있습니다.

```java
@InjectMocks
private SomeService someService;

@Mock
private SomeRepository someRepository;
```

- **테스트 범위 명확히 정의**: 테스트하려는 기능의 범위를 명확히 정의하고, 그 범위 내에서만 모킹을 진행하세요.
- **Thin Controller, Thick Service 원칙 준수**: Controller 계층은 가능한 얇게 유지하고, 비즈니스 로직은 Service 계층에 구현하여 테스트의 복잡성을 줄이세요.

> 오버-모킹은 테스트의 복잡성을 높이고, 실제 로직의 동작을 제대로 검증하지 못하는 문제를 야기할 수 있습니다. 따라서 Mockito를 사용할 때는 최소한의 모킹만을 활용하며, 테스트의 목적과 범위를 명확히 정의하여 효과적인 단위 테스트를 작성해야 합니다. 다음 섹션에서는 Stubbing의 재사용에 대해 알아보겠습니다.

# 6.2. Stubbing의 재사용 (Reusing Stubbing)

Mockito에서 Stubbing은 특정 메소드 호출에 대한 예상되는 동작을 정의하는 과정입니다. Stubbing의 재사용은 여러 테스트 케이스에서 동일한 Stubbing 설정을 반복적으로 활용하려는 경우에 중요한 주제입니다. 이 장에서는 Stubbing을 효과적으로 재사용하는 방법에 대해 알아봅니다.

## Stubbing 재사용의 필요성

- **중복 코드 감소**: 여러 테스트 메소드에서 비슷한 Stubbing이 필요할 때, 코드 중복을 방지하고 가독성을 향상시킬 수 있습니다.
- **일관성 유지**: 동일한 Stubbing을 여러 테스트에서 사용하면, 코드의 일관성을 유지하면서 예상 동작을 보장할 수 있습니다.

## Stubbing 재사용 방법
- **@BeforeEach 사용**: JUnit 5에서 제공하는 `@BeforeEach` 어노테이션을 사용하여 각 테스트 메소드 실행 전에 공통의 Stubbing을 설정할 수 있습니다.

```java
@Mock
private SomeRepository someRepository;

@BeforeEach
public void setUp() {
    when(someRepository.findByName("testName")).thenReturn(Optional.of(new Entity()));
}
```

- **헬퍼 메소드 정의**: 공통 Stubbing 로직을 헬퍼 메소드로 분리하고, 필요한 테스트 메소드에서 호출합니다.

```java
private void stubDefaultBehavior() {
    when(someRepository.findById(1L)).thenReturn(Optional.of(new Entity()));
}

@Test
public void someTest() {
    stubDefaultBehavior();
    // ...
}
```

- **테스트 유틸리티 클래스 활용**: 여러 테스트 클래스에서 동일한 Stubbing이 필요한 경우, 별도의 테스트 유틸리티 클래스를 생성하여 재사용 가능한 메소드를 정의하십시오.

## 주의 사항

- **과도한 재사용 피하기**: Stubbing의 재사용은 중복을 줄이는 데 유용하지만, 각 테스트의 독립성을 해칠 수 있습니다. 과도한 재사용은 테스트의 의도와 동작을 알아보기 어렵게 만들 수 있으므로 적절한 수준에서 활용하십시오.
- **테스트의 명확성 유지**: 재사용을 위해 복잡한 헬퍼 메소드나 유틸리티 클래스를 사용할 때, 테스트의 의도가 불명확해질 수 있습니다. 테스트 코드의 명확성과 의도를 항상 최우선으로 생각하십시오.

> Stubbing의 재사용은 Mockito를 사용하여 Spring Boot 환경에서 테스트를 작성할 때 중요한 고려사항 중 하나입니다. 적절한 재사용은 코드의 중복을 줄이고 유지보수를 용이하게 만들지만, 과도한 재사용은 테스트의 의도와 가독성을 해칠 수 있습니다. 따라서 적절한 균형을 찾아 재사용을 진행하십시오. 다음 섹션에서는 Mock 객체의 리셋에 대해 알아보겠습니다.

# 6.3. Mock 객체의 리셋 (Resetting Mock Objects)

Mock 객체는 Mockito를 사용하여 생성되며, 테스트 케이스의 실행 동안 해당 객체에 대한 호출 및 반환 값을 기록합니다. 때로는 여러 테스트에서 동일한 Mock 객체를 재사용하려는 경우나, 특정 테스트의 특정 부분에서 Mock의 상태를 초기화하고 싶을 때가 있습니다. 이러한 경우, Mock 객체의 리셋이 필요합니다.

## Mock 객체 리셋의 필요성

- **상태 초기화**: 같은 Mock 객체를 여러 테스트나 테스트의 여러 부분에서 사용하려는 경우, 이전의 상태가 새로운 테스트에 영향을 줄 수 있습니다. 이를 피하기 위해 Mock 객체의 상태를 초기화 할 수 있습니다.
- **가독성 및 명확성 향상**: 특정 테스트에서만 필요한 복잡한 Stubbing이 다른 테스트에 영향을 주지 않도록 하기 위해 리셋을 사용합니다.

## Mockito에서 Mock 객체 리셋하기

- Mockito는 `reset()` 메서드를 통해 Mock 객체를 쉽게 리셋할 수 있습니다.

```java
@Mock
private SomeService someService;

@Test
public void testMethodA() {
    when(someService.method()).thenReturn("ResponseA");
    // 테스트 로직...
    reset(someService); // Mock 객체 리셋
}

@Test
public void testMethodB() {
    when(someService.method()).thenReturn("ResponseB");
    // 테스트 로직...
}
```

## 리셋의 주의점

- **과도한 사용 피하기**: 리셋은 유용하지만 과도하게 사용되면 테스트의 복잡성을 높일 수 있습니다. 가능하면, 각 테스트 케이스마다 새로운 Mock 객체를 생성하는 것을 권장합니다.
- **리셋 후 재-Stubbing**: Mock 객체를 리셋한 후에는 모든 Stubbing이 제거됩니다. 따라서 리셋 후 필요한 Stubbing을 다시 설정해야 합니다.
- **@BeforeEach 활용**: JUnit 5의 `@BeforeEach` 어노테이션을 활용하여 테스트 메소드 실행 전에 자동으로 Mock 객체를 초기화하게 설정하는 것이 좋습니다.


> Mock 객체의 리셋은 Mockito의 고급 기능 중 하나로, 특정 상황에서 매우 유용할 수 있습니다. 그러나 남용은 테스트의 복잡성을 높일 수 있으므로 신중하게 사용해야 합니다. 테스트의 독립성과 명확성을 유지하기 위해서는 각 테스트 케이스에서 독립적인 Mock 객체를 사용하는 것이 가장 좋습니다. 다음 섹션에서는 Argument Matchers의 활용에 대해 알아보겠습니다.