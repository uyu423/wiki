---
title: [Spring Boot + Mockito] 07. Argument Matchers 활용
description: 
published: true
date: 2023-09-15T10:14:20.065Z
tags: java, mockito, springboot, test
editor: markdown
dateCreated: 2023-09-15T09:46:47.857Z
---

# 7.1. 기본적인 Argument Matchers 사용법

Argument Matchers(인자 매쳐)는 Mockito에서 제공하는 또 다른 강력한 기능 중 하나로, 메소드 호출 시 전달되는 인자값에 따라 동적으로 Stubbing이나 검증을 수행할 수 있게 합니다. 이를 통해 다양한 인자 조합에 따른 다양한 상황을 테스트 할 수 있게 됩니다.

## Argument Matchers란?

Argument Matchers는 메소드 호출 시 특정 인자값과 일치하는지, 혹은 특정 조건을 만족하는지를 확인하는데 사용되는 도구입니다. Mockito는 여러 가지 Argument Matchers를 제공하며, 사용자는 이를 활용하여 원하는 조건에 맞는 인자를 검증할 수 있습니다.

## 기본적인 Argument Matchers 사용법

Mockito는 다양한 기본 Argument Matchers를 제공합니다. 주로 사용되는 Argument Matchers는 다음과 같습니다:

- `any()`: 어떠한 값도 허용합니다.
- `eq(value)`: 특정 값과 일치하는 경우만 허용합니다.
- `anyInt()`, `anyLong()`, `anyDouble()` 등: 특정 타입의 값을 허용합니다.
- `isNull()`: null 값만 허용합니다.
- `isNotNull()`: null이 아닌 값만 허용합니다.

```java
@Mock
private SomeService someService;

@Test
public void basicMatchersTest() {
    when(someService.doSomething(any())).thenReturn("Response");
    when(someService.doSomething(eq("specificValue"))).thenReturn("SpecificResponse");

    assertEquals("Response", someService.doSomething("anyValue"));
    assertEquals("SpecificResponse", someService.doSomething("specificValue"));
}
```

## Argument Matchers 주의점

- **Argument Matchers의 일관성**: 한 메소드 호출에서 일부 인자에 Argument Matchers를 사용한다면, 나머지 모든 인자에도 Argument Matchers를 사용해야 합니다.

```java
// 잘못된 사용 예:
// when(someService.someMethod(any(), "specificValue")).thenReturn("Response");
// 위 코드는 오류를 발생시킵니다.

// 올바른 사용 예:
when(someService.someMethod(any(), eq("specificValue"))).thenReturn("Response");
```

- **실제 값과 함께의 사용**: 때로는 Argument Matchers와 실제 값을 함께 사용하고 싶을 때가 있습니다. 이런 경우, `eq()`를 사용하여 실제 값을 Argument Matcher 형태로 변환할 수 있습니다.
- **커스텀 Argument Matchers**: 기본적으로 제공되는 Argument Matchers만으로 충분하지 않은 경우, 사용자는 자신만의 Argument Matchers를 작성할 수 있습니다. 이에 대해서는 다음 항목인 "7.2. Custom Argument Matchers 작성하기"에서 자세히 다루겠습니다.

> Argument Matchers는 Mockito의 강력한 도구 중 하나로, 다양한 인자 조합에 대한 테스트를 간단하게 수행할 수 있게 도와줍니다. Argument Matchers를 효과적으로 사용하면, 테스트 코드의 가독성과 유연성을 크게 향상시킬 수 있습니다. 다음 섹션에서는 Argument Matchers를 활용하여 사용자 정의 매쳐를 작성하는 방법에 대해 알아보겠습니다.

# 7.2. Custom Argument Matchers 작성하기

Mockito의 기본 Argument Matchers는 다양한 상황을 커버하도록 설계되었지만, 때로는 특정 비즈니스 로직이나 도메인 특화적인 조건을 테스트하기 위해 사용자 정의 Argument Matchers를 작성할 필요가 있습니다. 이 섹션에서는 사용자 정의 Argument Matchers를 작성하는 방법에 대해 알아보겠습니다.

## 사용자 정의 Argument Matchers의 필요성

가령, 우리가 테스트하려는 메소드가 특정한 패턴의 문자열을 인자로 받아야 하는 경우, 기본 Argument Matchers만으로는 이를 충분히 검증하기 어렵습니다. 이런 상황에서 사용자 정의 Argument Matchers를 활용하면, 메소드가 올바른 패턴의 문자열을 받았는지 쉽게 확인할 수 있습니다.

## Custom Argument Matcher 작성하기

- **ArgumentMatcher 인터페이스 구현**: `org.mockito.ArgumentMatcher` 인터페이스를 구현하는 클래스를 작성합니다. `matches` 메소드를 오버라이드하여 원하는 조건을 정의합니다.

```java
import org.mockito.ArgumentMatcher;

public class StringPatternMatcher implements ArgumentMatcher<String> {
    private final String pattern;

    public StringPatternMatcher(String pattern) {
        this.pattern = pattern;
    }

    @Override
    public boolean matches(String argument) {
        if (argument == null) {
            return false;
        }
        return argument.matches(pattern);
    }
}
```

- **ArgumentCaptor와 함께 사용**: 위에서 작성한 Custom Argument Matcher를 `ArgumentCaptor`와 함께 사용하여 메소드 호출을 검증합니다.

```java
@Mock
private SomeService someService;

@Test
public void customMatcherTest() {
    when(someService.doSomething(argThat(new StringPatternMatcher("[a-z]+")))).thenReturn("Matched");

    assertEquals("Matched", someService.doSomething("test"));
    assertNull(someService.doSomething("Test123")); // 대문자나 숫자 포함 문자열은 매치되지 않습니다.
}
```

## Custom Argument Matcher 주의점

- **성능 이슈**: Argument Matcher 내부에서 복잡한 연산이나 무거운 로직을 수행하는 것은 테스트 성능에 영향을 줄 수 있으므로 주의가 필요합니다.
- **재사용성**: 가능하다면, Custom Argument Matcher는 재사용 가능하도록 설계하는 것이 좋습니다. 특히, 비슷한 유형의 테스트 케이스가 여러 개 있을 경우, 재사용성을 고려하여 코드 중복을 최소화하는 것이 효율적입니다.
- **명확한 의도 전달**: Custom Argument Matcher의 이름과 로직은 해당 Matcher가 어떤 조건을 검증하는지 명확하게 전달되어야 합니다. 그렇지 않으면, 다른 개발자들이 해당 테스트 코드를 읽을 때 혼란을 느낄 수 있습니다.

> 사용자 정의 Argument Matchers는 테스트 케이스 작성 시 특정 조건을 더 세밀하게 검증할 필요가 있을 때 매우 유용합니다. 기본 Argument Matchers로는 표현하기 어려운 복잡한 조건도 사용자 정의 Argument Matchers를 통해 쉽게 검증할 수 있게 되므로, Mockito를 활용한 테스트 코드 작성 시 반드시 숙지해야 할 중요한 기법 중 하나입니다.