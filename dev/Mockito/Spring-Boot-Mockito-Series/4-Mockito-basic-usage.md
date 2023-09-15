---
title: [Spring Boot + Mockito] 4. Mockito 기본 사용 방법
description: 
published: true
date: 2023-09-15T09:15:08.299Z
tags: java, mockito, springboot, test
editor: markdown
dateCreated: 2023-09-15T09:15:08.299Z
---

# 4.1. Mock 객체 생성
Mock 객체는 실제 객체의 동작을 모방하는 가짜 객체로, 단위 테스트를 작성할 때 주로 사용됩니다. Mockito를 사용하면 이러한 Mock 객체를 손쉽게 생성할 수 있습니다. Spring Boot 환경에서의 Mock 객체 생성 방법을 상세하게 살펴보겠습니다.

## 1. @Mock 애너테이션 활용

`@Mock` 애너테이션은 클래스나 인터페이스에 대한 Mock 객체를 생성하기 위해 사용됩니다. 이 애너테이션을 사용하면 Mockito는 해당 타입의 Mock 객체를 자동으로 생성해줍니다.

```java
@RunWith(MockitoJUnitRunner.class) // Mockito 확장자 사용
public class SampleTest {

    @Mock
    private SampleService sampleService; // Mock 객체 자동 생성

    // ...
}
```

## 2. Mockito.mock() 메서드 활용

`Mockito.mock()` 메서드를 사용하여 명시적으로 Mock 객체를 생성할 수 있습니다. 이 방법은 `@Mock` 애너테이션을 사용하지 않고 Mock 객체를 생성할 때 유용합니다.

```java
public class SampleTest {

    SampleService sampleService = Mockito.mock(SampleService.class); // Mock 객체 생성

    // ...
}
```

## 3. Mock 객체의 기본 동작 설정

Mock 객체는 기본적으로 Java의 모든 값(예: 0, false, null 등)을 반환합니다. 이 동작은 `Mockito.RETURNS_DEFAULTS` 전략을 사용하여 구현됩니다. 필요한 경우, `Mockito.mock()` 메서드의 두 번째 인자로 다른 반환 전략을 설정할 수 있습니다.

```java
SampleService sampleService = Mockito.mock(SampleService.class, Mockito.RETURNS_SMART_NULLS);
```

여기서 `RETURNS_SMART_NULLS` 전략은 메서드 호출이 null을 반환할 경우, 해당 타입에 맞는 '스마트 null'을 반환하도록 합니다. 이는 `NullPointerException`을 방지하며, 추가적인 정보도 제공합니다.

## 4. Mock 객체의 행동 정의 (Stubbing)

Mock 객체의 행동을 정의하려면 `when()` 메서드와 함께 `thenReturn()`, `thenThrow()`, `thenAnswer()` 등의 메서드를 사용할 수 있습니다. 이에 대한 자세한 내용은 4.2. Stubbing 방법에서 다루겠습니다.

Mock 객체는 단위 테스트에서 실제 객체의 동작을 대체하는 중요한 역할을 합니다. Mockito를 사용하면 Mock 객체를 쉽게 생성하고 관리할 수 있습니다. Spring Boot 환경에서는 Mockito와 함께 다양한 테스트 유틸리티를 활용하여 더욱 효과적인 테스트 코드를 작성할 수 있습니다.

# 4.2. Stubbing 방법
Stubbing이란 Mock 객체가 특정 메소드 호출에 대하여 원하는 동작 또는 결과를 반환하도록 설정하는 과정을 말합니다. Mockito에서는 `when()` 함수를 사용하여 Mock 객체의 메소드 호출을 Stub하게 됩니다.

## 1. 기본적인 Stubbing

Mock 객체의 메소드 호출 결과를 설정하려면 `when()` 함수와 `thenReturn()` 함수를 조합하여 사용합니다.

```java
@Test
public void basicStubbing() {
    List<String> mockList = Mockito.mock(List.class);

    Mockito.when(mockList.size()).thenReturn(10);

    assertEquals(10, mockList.size());
}
```

이 예에서, `mockList.size()` 호출 결과가 항상 10을 반환하도록 설정되었습니다.

## 2. 연속적인 호출에 대한 Stubbing (Consecutive Stubbing)

여러 번의 호출에 대하여 다른 값을 반환하거나 다른 동작을 하게 하려면, `thenReturn()` 함수를 연속적으로 사용합니다.

```java
@Test
public void consecutiveStubbing() {
    List<String> mockList = Mockito.mock(List.class);

    Mockito.when(mockList.size()).thenReturn(10).thenReturn(20).thenReturn(30);

    assertEquals(10, mockList.size());
    assertEquals(20, mockList.size());
    assertEquals(30, mockList.size());
}
```

## 3. 예외 발생시키기

Mock 객체의 메소드 호출 시 예외를 발생시키려면 `thenThrow()` 함수를 사용합니다.

```java
@Test(expected = RuntimeException.class)
public void throwExceptionStubbing() {
    List<String> mockList = Mockito.mock(List.class);

    Mockito.when(mockList.get(Mockito.anyInt())).thenThrow(new RuntimeException("예외 발생!"));

    mockList.get(1);  // RuntimeException 발생
}
```

## 4. 메소드에 인자값을 사용한 Stubbing (Argument Matchers)

특정 인자값에 대한 메소드 호출만 Stub하려면, Argument Matchers를 사용합니다. `any()`, `eq()`, `anyString()` 등의 함수들이 있습니다.

```java
@Test
public void argumentMatchersStubbing() {
    Map<String, String> mockMap = Mockito.mock(Map.class);

    Mockito.when(mockMap.put(Mockito.eq("키1"), Mockito.anyString())).thenReturn("값1");

    assertEquals("값1", mockMap.put("키1", "임의의 값"));
}
```

## 5. Void 메소드 Stubbing

Void 반환 타입을 가진 메소드를 Stub할 경우, `doThrow()`, `doNothing()`, `doAnswer()` 등의 메소드를 사용합니다.

```java
@Test(expected = RuntimeException.class)
public void voidMethodStubbing() {
    List<String> mockList = Mockito.mock(List.class);

    Mockito.doThrow(new RuntimeException("예외 발생!")).when(mockList).clear();

    mockList.clear();  // RuntimeException 발생
}
```

## 6. Real Method 호출하기 (Spies)

Mock 객체의 메소드 중 일부를 실제로 실행하게 하려면 `thenCallRealMethod()` 함수를 사용합니다. 이 기능은 Spy 객체에서 주로 사용됩니다.

```java
@Test
public void realMethodStubbing() {
    List<String> spyList = Mockito.spy(new ArrayList<>());

    spyList.add("원본 데이터");
    Mockito.when(spyList.size()).thenCallRealMethod();

    assertEquals(1, spyList.size());
}
```

Mockito에서 Stubbing은 Mock 객체의 동작을 커스터마이징하는 핵심 기능 중 하나입니다. 다양한 Stubbing 방법을 이해하고 적절히 활용하면, 단위 테스트의 퀄리티와 유용성을 크게 높일 수 있습니다. 다음 섹션에서는 메소드 호출의 확인 방법에 대해 다룰 예정입니다.
  
# 4.3. 메소드 호출 확인하기
메소드의 호출을 확인하는 것은 단위 테스트의 중요한 부분입니다. Mockito에서는 `verify()` 메소드를 사용하여 Mock 객체의 특정 메소드가 어떻게 호출되었는지를 검증할 수 있습니다.

## 1. 기본적인 메소드 호출 확인

Mock 객체의 메소드가 호출되었는지 확인하려면 `verify()` 함수를 사용합니다.

```java
@Test
public void basicVerification() {
    List<String> mockList = Mockito.mock(List.class);

    mockList.add("테스트");

    Mockito.verify(mockList).add("테스트");
}
```

이 예에서는 `mockList.add("테스트")` 가 호출되었는지를 확인합니다.

## 2. 메소드 호출 횟수 확인

특정 메소드가 몇 번 호출되었는지를 검증할 수 있습니다.

```java
@Test
public void verificationWithTimes() {
    List<String> mockList = Mockito.mock(List.class);

    mockList.add("테스트1");
    mockList.add("테스트1");
    mockList.add("테스트2");

    Mockito.verify(mockList, Mockito.times(2)).add("테스트1");
    Mockito.verify(mockList, Mockito.times(1)).add("테스트2");
}
```

## 3. 특정 시간 안에 메소드 호출 확인

메소드 호출이 특정 시간 안에 이루어졌는지 확인할 수 있습니다.

```java
@Test
public void verificationWithinTime() {
    List<String> mockList = Mockito.mock(List.class);

    mockList.add("테스트");

    Mockito.verify(mockList, Mockito.timeout(100)).add("테스트");
}
```

## 4. 특정 메소드가 호출되지 않았음을 확인

어떠한 메소드가 호출되지 않았음을 검증할 수 있습니다.

```java
@Test
public void verificationNoInteractions() {
    List<String> mockList = Mockito.mock(List.class);

    Mockito.verify(mockList, Mockito.never()).add("테스트");
}
```

## 5. 특정 메소드 이외의 메소드 호출을 확인

`verifyNoMoreInteractions()`를 사용하면, 지정된 메소드 이외에는 어떤 메소드도 호출되지 않았음을 검증할 수 있습니다.

```java
@Test
public void verificationNoMoreInteractions() {
    List<String> mockList = Mockito.mock(List.class);

    mockList.add("테스트");

    Mockito.verify(mockList).add("테스트");
    Mockito.verifyNoMoreInteractions(mockList);
}
```

## 6. Argument Matchers와 함께 사용

Argument Matchers를 사용하여 특정 인자값으로 메소드가 호출되었는지 검증할 수 있습니다.

```java
@Test
public void verificationWithArgumentMatchers() {
    Map<String, String> mockMap = Mockito.mock(Map.class);

    mockMap.put("키", "값");

    Mockito.verify(mockMap).put(Mockito.eq("키"), Mockito.anyString());
}
```

Mockito에서 `verify()` 메소드는 Mock 객체의 메소드 호출 패턴과 횟수를 검증하는데 매우 유용합니다. 이를 통해 우리는 기대한 바와 다르게 메소드가 호출되었거나, 예상한 횟수만큼 호출되지 않았을 때 그것을 캐치하고 오류를 반환할 수 있습니다. 이러한 검증 과정은 코드의 안정성을 높이고, 코드가 예상대로 동작하는지 확신할 수 있게 도와줍니다. 다음 섹션에서는 Mockito에서 예외를 처리하는 방법에 대해 다룰 예정입니다.
  
# 4.4. 예외 처리하기
Mock 객체에서 예외를 발생시키는 것은 Mockito의 강력한 기능 중 하나입니다. 이를 통해, 예외 상황에서 시스템의 동작을 검증할 수 있습니다. Spring Boot 환경에서도 Mockito를 활용하여 예외 처리 테스트를 손쉽게 구성할 수 있습니다.

## 1. 기본적인 예외 발생

Mock 객체의 특정 메소드 호출 시 예외를 발생시키려면 `thenThrow()` 함수를 사용합니다.

```java
@Test(expected = IllegalArgumentException.class)
public void shouldThrowException() {
    List<String> mockList = Mockito.mock(List.class);
    Mockito.when(mockList.get(Mockito.anyInt())).thenThrow(new IllegalArgumentException("잘못된 인덱스"));

    mockList.get(0);
}
```

위의 예에서는 mockList 객체의 get 메소드 호출 시 `IllegalArgumentException`이 발생합니다.

## 2. 예외 타입으로 발생

발생시킬 예외의 타입만 지정하면, 해당 타입의 기본 생성자를 사용하여 예외가 발생합니다.

```java
@Test(expected = NullPointerException.class)
public void shouldThrowExceptionWithType() {
    List<String> mockList = Mockito.mock(List.class);
    Mockito.when(mockList.get(Mockito.anyInt())).thenThrow(NullPointerException.class);

    mockList.get(0);
}
```

## 3. Void 메소드에서의 예외 발생

void 반환 타입의 메소드에서 예외를 발생시키려면 `doThrow()` 함수를 사용합니다.

```java
@Test(expected = UnsupportedOperationException.class)
public void shouldThrowExceptionForVoidMethod() {
    List<String> mockList = Mockito.mock(List.class);
    Mockito.doThrow(new UnsupportedOperationException("지원되지 않는 연산")).when(mockList).clear();

    mockList.clear();
}
```

## 4. 연속적인 예외 발생

`thenThrow()`를 체인 방식으로 호출하여 연속적으로 여러 예외를 발생시킬 수 있습니다.

```java
@Test(expected = RuntimeException.class)
public void shouldThrowMultipleExceptions() {
    List<String> mockList = Mockito.mock(List.class);
    Mockito.when(mockList.get(Mockito.anyInt())).thenThrow(IllegalArgumentException.class).thenThrow(RuntimeException.class);

    mockList.get(0); // 첫 호출에는 IllegalArgumentException 발생
    mockList.get(0); // 두 번째 호출에는 RuntimeException 발생
}
```

## 5. 예외 발생시 추가 동작 수행

`thenAnswer()`를 사용하여 예외 발생 시 추가적인 동작을 수행하게 만들 수 있습니다.

```java
@Test(expected = IllegalArgumentException.class)
public void shouldPerformAdditionalActionsOnException() {
    List<String> mockList = Mockito.mock(List.class);
    Mockito.when(mockList.get(Mockito.anyInt())).thenAnswer(invocation -> {
        if (invocation.getArgument(0, Integer.class) == 0) {
            System.out.println("0 인덱스에 접근하였습니다.");
            throw new IllegalArgumentException("잘못된 인덱스");
        }
        return null;
    });

    mockList.get(0);
}
```

Mockito는 다양한 예외 처리 테스트를 지원합니다. 이 기능을 활용하면, 다양한 예외 상황에서의 애플리케이션 동작을 손쉽게 검증할 수 있습니다. 예외 처리는 애플리케이션의 안정성과 견고성을 높이는 중요한 요소이므로, Mockito를 통해 이러한 테스트를 충실히 수행하는 것이 중요합니다. 다음 섹션에서는 Spring Boot 환경에서 Mockito를 어떻게 활용하는지에 대해 자세히 알아보겠습니다. 