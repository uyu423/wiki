---
title: [Spring Boot + Mockito] 10. 자주 만나는 문제점 및 해결 방안
description: 
published: true
date: 2023-09-15T10:11:08.960Z
tags: 
editor: markdown
dateCreated: 2023-09-15T10:11:08.960Z
---

# 10.1. Stubbing 하지 않은 메소드 호출 시

Mockito를 사용하여 테스트 케이스를 작성할 때 가장 흔히 겪는 문제 중 하나는 Stubbing하지 않은 메소드를 호출하는 경우입니다. 이 문제를 이해하고 올바르게 처리하는 방법을 알아보겠습니다.

## 문제 상황

Mock 객체는 실제 구현체가 아니므로 메서드에 대한 기본적인 동작이 정의되지 않습니다. 때문에, Stubbing(행동 지정)을 해주지 않은 메서드를 호출하면 Mock 객체는 기본값(예: int의 경우 0, 객체의 경우 null)을 반환하게 됩니다.

```java
public interface BookRepository {
    Book findById(Long id);
}

...

@Mock
BookRepository bookRepository;

@Test
public void whenNotStubbed_thenReturnsDefault() {
    Book book = bookRepository.findById(1L);
    assertNull(book);  // 이 테스트는 통과합니다.
}
```

위의 예에서 `findById` 메서드는 Stubbing되지 않았으므로 null을 반환합니다.

## 왜 문제가 되는가?

- 기대하지 않은 Null 반환: 앞서 언급한 예시와 같이, Stubbing을 하지 않은 메소드는 기본값을 반환합니다. 이로 인해 NullPointer 예외가 발생할 가능성이 있습니다.

- 실제 로직과의 불일치: Mock 객체는 실제 객체의 로직을 모르기 때문에, Stubbing 없이 호출될 경우 실제 동작과 다른 결과를 보여줄 수 있습니다.

## 해결 방안

### 명시적인 Stubbing

가장 기본적인 방법은 호출하려는 메서드에 대해 Stubbing을 명시적으로 제공하는 것입니다.

```java
given(bookRepository.findById(1L)).willReturn(new Book(1L, "Sample Title", "Sample Author"));
```

### 빈 호출에 대한 기본 동작 설정

Mockito에서는 Mock 객체의 메서드가 Stubbing 없이 호출될 경우의 기본 동작을 설정할 수 있습니다.

```java
// 모든 메서드 호출에 대해 예외를 발생시킵니다.
Mockito.mock(BookRepository.class, Mockito.RETURNS_SMART_NULLS);
```

### Strict Stubbing 활성화

Mockito 2.x 버전부터는 strict stubbing 기능이 도입되었습니다. 이 기능을 활성화하면, Stubbing하지 않은 메서드가 호출되면 테스트가 실패하게 됩니다.

```java
MockitoJUnit.rule().strictness(Strictness.STRICT_STUBS);
```

> Spring Boot와 Mockito를 결합하여 테스트를 작성할 때는 다양한 문제 상황을 마주칠 수 있습니다. Stubbing하지 않은 메소드의 호출은 이러한 상황 중 하나로, 이를 효과적으로 다루는 방법을 알고 있어야 테스트의 신뢰도와 품질을 높일 수 있습니다. 위에서 소개한 방법들을 적절히 활용하여, 테스트 코드의 완결성을 높이고 잠재적인 문제점을 방지해보세요.

# 10.2. InOrder 사용 시 문제점

Mockito에서는 InOrder를 사용하여 여러 메소드 호출의 순서를 검증할 수 있습니다. 이는 복잡한 비즈니스 로직이나 외부 서비스 호출 등에서 특정 순서대로 메서드가 호출되는 것을 보장하고 싶을 때 유용합니다. 그러나 InOrder 사용 시 주의할 점과 자주 발생하는 문제들이 있습니다. 이번 항목에서는 이러한 문제점들과 그에 대한 해결 방안을 자세히 알아보겠습니다.

## 문제 상황

### 부분적인 순서 검증

InOrder를 사용하여 검증을 진행할 때 모든 메서드 호출을 포함하지 않고 일부만 검증하게 되면, 원치 않는 순서의 메서드 호출이 있을 수 있습니다.

### 같은 메서드의 여러 번 호출

동일한 메서드가 여러 번 호출되는 경우 InOrder를 사용하여 순서를 정확히 검증하는 것이 어려울 수 있습니다.

### 복잡한 순서 검증

여러 Mock 객체와 여러 메서드 호출에 대한 순서를 검증하려고 할 때 코드 복잡도가 증가할 수 있습니다.

```java
@Mock
OrderService orderService;
@Mock
PaymentService paymentService;

@Test
public void testOrderFlow() {
    orderService.createOrder();
    paymentService.processPayment();
    orderService.finalizeOrder();

    InOrder inOrder = inOrder(orderService, paymentService);
    inOrder.verify(orderService).createOrder();
    inOrder.verify(paymentService).processPayment();
    // 만약 finalizeOrder를 검증하지 않는다면 문제 발생 가능성이 있습니다.
}
```

## 해결 방안

### 완전한 순서 검증

InOrder를 사용할 때 가능한 모든 관련 메서드 호출을 포함시켜 검증합니다. 이를 통해 부분적인 순서 검증으로 인한 문제를 방지할 수 있습니다.

### 다중 호출 처리

동일한 메서드의 여러 번 호출을 검증할 때는 `times()`를 활용하여 호출 횟수를 명시적으로 지정합니다.

```java
inOrder.verify(orderService, times(2)).createOrder();
```

### 코드의 간결성 유지:

복잡한 순서 검증이 필요할 경우, 관련된 메서드 호출들을 그룹화하거나 별도의 검증 메서드로 분리하여 코드의 가독성과 유지 보수성을 높입니다.

> InOrder는 Mockito에서 제공하는 강력한 도구 중 하나이지만, 올바르게 사용하지 않으면 예기치 않은 문제를 초래할 수 있습니다. 따라서, 순서 검증 시에는 주의 깊게 검증을 구성하고 테스트의 완결성을 확보하는 것이 중요합니다. 이를 통해 실제 애플리케이션 로직의 정확한 순서 준수를 효과적으로 검증할 수 있습니다.

# 10.3. 실제 서비스 대신 Mock 사용시 발생하는 문제

Mock 객체는 테스트 환경에서 실제 객체 대신 사용되어 원하는 동작을 정의하고 결과를 예측할 수 있게 도와줍니다. 그러나 Mock 객체를 사용할 때 발생하는 일련의 문제점들이 있으며 이러한 문제들에 대응하는 방법을 알아보도록 하겠습니다.

## 문제 상황

### 실제 동작과의 불일치

Mock 객체는 실제 객체의 내부 동작을 모방하는 것이 아니므로, 실제 로직의 변경이 있을 때 Mock 객체의 동작이 변경되지 않습니다. 이로 인해 실제 서비스가 변경되었을 때 테스트는 여전히 통과하는 상황이 발생할 수 있습니다.

### 과도한 Mocking

너무 많은 Mock 객체를 사용하면 테스트 코드가 복잡해지고, 실제 시스템의 동작을 정확하게 반영하지 못할 수 있습니다.

### 외부 서비스와의 연동 문제

외부 서비스나 라이브러리를 Mocking 할 때, 해당 서비스의 API나 동작이 변경될 경우 Mock 객체와 실제 객체 간의 동작 차이가 발생할 수 있습니다.

### Mock 객체의 오버 스펙

Mock 객체를 사용하여 특정 메소드의 호출 여부, 호출 횟수, 인자 값 등을 상세하게 검증하게 되면, 테스트 코드가 과도하게 구체적이 되어 작은 변경에도 테스트 코드를 수정해야 하는 문제가 발생합니다.

```java
@Mock
PaymentService paymentService;

@Test
public void testPayment() {
    when(paymentService.processPayment(any())).thenReturn(true);

    // 실제 PaymentService의 내부 로직이 변경되어도 Mock은 동일하게 동작합니다.
}
```

## 해결 방안

### Mock 객체와 실제 객체의 동기화

실제 서비스나 라이브러리의 변경이 있을 때마다 Mock 객체의 동작도 업데이트하고 테스트를 재실행하여 동기화를 유지합니다.

### Integration Test의 활용

Mock 객체만을 사용하는 단위 테스트 외에도, 실제 서비스와의 연동을 검증하는 통합 테스트를 작성하여 실제 환경에서의 동작을 검증합니다.

### Mocking 범위 제한

필요한 경우에만 Mock 객체를 사용하고, 가능한 실제 객체나 서비스를 활용하여 테스트합니다.

### 테스트의 범용성 유지

테스트 코드는 애플리케이션의 주요 로직과 비즈니스 규칙을 검증하는 데 중점을 두어야 합니다. 따라서, Mock 객체에서의 구체적인 메서드 호출이나 인자 검증을 최소화하여 테스트 코드의 범용성을 유지합니다.

> Mockito를 활용한 Mock 객체는 테스트 환경에서 매우 유용하나, 그 동작이 실제 서비스와 항상 일치한다고 가정하면 안 됩니다. 따라서, 실제 환경과 테스트 환경 간의 차이를 이해하고, 테스트 전략을 잘 구성하여 두 환경 간의 간극을 최소화하는 것이 중요합니다.
