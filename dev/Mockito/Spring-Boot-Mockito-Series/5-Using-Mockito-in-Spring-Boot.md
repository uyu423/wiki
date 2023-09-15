---
title: [Spring Boot + Mockito] 4. Mockito 기본 사용 방법
description: 
published: true
date: 2023-09-15T09:24:48.136Z
tags: java, mockito, springboot, test
editor: markdown
dateCreated: 2023-09-15T09:24:48.136Z
---

# 5.1. @MockBean과 @Autowired 조합

Spring Boot에서는 통합 테스트를 위해 `@SpringBootTest` 어노테이션을 제공합니다. `@SpringBootTest`는 전체 Spring 컨텍스트를 로드하여 실제 환경과 유사한 테스트 환경을 구성할 수 있게 도와줍니다. 이때, 실제 서비스나 리포지토리 대신 Mock 객체를 사용하여 테스트를 수행하려면 `@MockBean` 어노테이션을 사용할 수 있습니다.

## @MockBean의 기능

`@MockBean`은 Spring 컨텍스트에 등록된 빈을 Mockito의 Mock 객체로 대체해줍니다. 이를 통해, 실제 빈의 로직을 실행하는 대신 Mock 객체의 로직을 실행하게 되어 원하는 방식으로 테스트를 진행할 수 있습니다.

## 기본적인 사용법

먼저, `@SpringBootTest` 어노테이션과 함께 `@MockBean`을 사용하여 Mock 객체를 정의합니다.

```java
@SpringBootTest
public class SomeServiceTest {

    @Autowired
    private SomeService someService;

    @MockBean
    private SomeRepository someRepository;
}
```

위 예제에서, `SomeRepository`는 Mock 객체로 생성되며, `SomeService`는 실제 객체로 생성됩니다. 따라서 `SomeService`의 메소드를 호출할 때, 내부에서 `SomeRepository`의 메소드가 호출되면 Mock 객체의 메소드가 실행됩니다.

## Stubbing과 @MockBean
Mock 객체의 메소드 호출을 가로채어 원하는 값을 반환하게 만들기 위해 Mockito의 `when`과 `thenReturn` 메소드를 사용할 수 있습니다.

```java
@Test
public void testFindById() {
    Long id = 1L;
    String expectedValue = "SomeValue";

    Mockito.when(someRepository.findById(id)).thenReturn(Optional.of(expectedValue));

    String result = someService.findById(id);
    assertEquals(expectedValue, result);
}
```

이 예제에서는 `someRepository`의 `findById` 메소드가 호출될 때, `expectedValue`를 반환하도록 설정하였습니다.

## @Autowired와의 조합

Spring Boot 테스트에서는 `@MockBean`으로 생성된 Mock 객체와 `@Autowired`로 주입받은 실제 객체를 함께 사용할 수 있습니다. 이렇게 하면, Mock 객체와 실제 객체 간의 상호작용을 쉽게 테스트할 수 있습니다.

> `@MockBean`은 Spring Boot 테스트에서 Mock 객체를 손쉽게 사용할 수 있도록 도와주는 강력한 도구입니다. @Autowired와의 조합을 통해, 실제 객체와 Mock 객체 간의 상호작용을 쉽게 테스트할 수 있습니다. 이를 활용하면, 서비스 레이어나 컨트롤러 레이어에서의 복잡한 상호작용을 효과적으로 테스트할 수 있습니다. 다음 섹션에서는 Service Layer의 테스트 방법에 대해 자세히 알아보겠습니다.

# 5.2. Service Layer 테스트

Service Layer는 어플리케이션의 핵심 비즈니스 로직을 담당하는 계층입니다. 따라서 이 계층의 테스트는 매우 중요하며, Mockito는 이 과정을 간편하게 도와줍니다.

##  Service Layer의 테스트 목표
Service Layer 테스트의 주요 목표는 다음과 같습니다:

- 비즈니스 로직이 정확히 수행되는지 확인
- Repository나 외부 서비스와의 상호작용이 올바르게 이루어지는지 검증
- 예외 상황에 대한 적절한 처리를 하는지 검증

## Mockito와 Service Layer

Service Layer에서는 주로 Repository나 다른 Service를 호출하게 됩니다. Mockito를 사용하면 이러한 외부 의존성을 Mock 객체로 대체하여, 외부 서비스의 동작에 구애받지 않고 Service Layer만을 대상으로 테스트를 진행할 수 있습니다.

## 기본적인 Service Layer 테스트 예제

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class SomeServiceTest {

    @Autowired
    private SomeService someService;

    @MockBean
    private SomeRepository someRepository;

    @Test
    public void testFindById() {
        Long id = 1L;
        SomeEntity expectedEntity = new SomeEntity(id, "SomeValue");

        Mockito.when(someRepository.findById(id)).thenReturn(Optional.of(expectedEntity));

        SomeDto result = someService.findById(id);

        assertEquals(expectedEntity.getValue(), result.getValue());
    }
}
```

위 예제에서 `SomeService`의 `findById` 메소드는 내부적으로 `SomeRepository`의 `findById` 메소드를 호출합니다. 따라서 테스트에서는 `SomeRepository`의 해당 메소드가 호출될 때 반환될 값을 미리 지정해줍니다.

## 예외 처리 테스트

Service Layer에서는 다양한 예외 상황을 처리해야 합니다. Mockito를 사용하면 예외 발생 시나리오도 쉽게 테스트할 수 있습니다.

```java
@Test(expected = SomeNotFoundException.class)
public void testFindById_NotFound() {
    Long id = 1L;

    Mockito.when(someRepository.findById(id)).thenReturn(Optional.empty());

    someService.findById(id);
}
```

위 예제에서는 `SomeRepository`의 `findById` 메소드가 `Optional.empty()`를 반환할 때 `SomeNotFoundException`이 발생하는지 테스트하였습니다.

## Service 간의 상호작용 테스트

때로는 하나의 Service 메소드 내에서 다른 Service를 호출해야 할 경우도 있습니다. 이러한 상호작용도 Mockito를 활용해 테스트할 수 있습니다.

```java
@MockBean
private AnotherService anotherService;

@Test
public void testSomeBusinessLogic() {
    // ... 생략 ...

    Mockito.when(anotherService.someMethod()).thenReturn(someValue);

    // ... 테스트 로직 ...

    Mockito.verify(anotherService, Mockito.times(1)).someMethod();
}
```

여기에서는 anotherService의 someMethod가 한 번 호출되었는지 검증하였습니다.

> Service Layer 테스트는 어플리케이션의 핵심 로직을 검증하는 중요한 과정입니다. Mockito를 활용하면 외부 의존성을 간편하게 Mock 객체로 대체하고, 다양한 시나리오와 예외 상황을 효과적으로 테스트할 수 있습니다. 다음 섹션에서는 Repository Layer의 테스트 방법에 대해 알아보겠습니다.

# 5.3. Repository Layer 테스트

Repository Layer는 데이터베이스와의 상호작용을 관리하는 계층으로, 이 계층의 테스트는 데이터의 CRUD(Create, Read, Update, Delete) 작업이 올바르게 수행되는지 확인하는 것을 목적으로 합니다. Mockito는 이 과정에서 실제 데이터베이스와의 상호작용 없이도 이를 효과적으로 테스트할 수 있게 도와줍니다.

## Repository Layer의 테스트 목표

- CRUD 연산이 정확히 수행되는지 확인
- 쿼리 최적화나 특수한 DB 연산을 포함하는 메소드가 올바르게 동작하는지 검증
- 예외 상황에 대한 적절한 처리를 하는지 검증

## Mockito로 Repository Layer 테스트하기
Spring Data JPA와 같은 기술을 사용할 경우, 대부분의 CRUD 연산이 이미 구현되어 있습니다. 그렇기에 테스트의 중점은 사용자 정의 쿼리나 특수한 DB 연산에 대한 것이 될 수 있습니다.

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class SomeRepositoryTest {

    @Autowired
    private SomeService someService;

    @MockBean
    private SomeRepository someRepository;

    @Test
    public void testFindByValue() {
        String value = "testValue";
        SomeEntity expectedEntity = new SomeEntity(1L, value);

        Mockito.when(someRepository.findByValue(value)).thenReturn(Collections.singletonList(expectedEntity));

        List<SomeDto> results = someService.findByValue(value);

        assertFalse(results.isEmpty());
        assertEquals(expectedEntity.getId(), results.get(0).getId());
    }
}
```

위 예제에서 findByValue는 사용자 정의 쿼리가 될 수 있으며, Mockito를 사용해 해당 메소드의 반환 값을 지정하였습니다.

## 예외 처리 테스트
데이터베이스와의 상호작용에서는 다양한 예외가 발생할 수 있습니다. Mockito를 사용하여 예외 발생 시나리오를 쉽게 테스트할 수 있습니다.

```java
@Test(expected = DataIntegrityViolationException.class)
public void testSaveDuplicateValue() {
    SomeEntity entity = new SomeEntity(1L, "duplicateValue");

    Mockito.when(someRepository.save(entity)).thenThrow(DataIntegrityViolationException.class);

    someService.save(entity);
}
```

위 예제에서는 중복된 값의 저장 시 `DataIntegrityViolationException` 예외가 발생하는지 테스트하였습니다.

## Custom Query 테스트

사용자 정의 쿼리나 특수한 DB 연산을 포함하는 메소드의 경우 Mockito를 사용하여 예상되는 결과를 제공하고, Service Layer에서 해당 결과가 올바르게 처리되는지 검증할 수 있습니다.

```java
@Test
public void testCustomQuery() {
    String customParam = "custom";
    SomeEntity expectedEntity = new SomeEntity(2L, "customValue");

    Mockito.when(someRepository.customQueryMethod(customParam)).thenReturn(Collections.singletonList(expectedEntity));

    List<SomeDto> results = someService.customBusinessLogic(customParam);

    assertFalse(results.isEmpty());
    assertEquals(expectedEntity.getValue(), results.get(0).getValue());
}
```

> Repository Layer는 데이터베이스와의 상호작용을 관리하는 중요한 계층입니다. Mockito를 활용하면 실제 데이터베이스와의 상호작용을 모킹하여, 다양한 시나리오와 예외 상황에 대해 효과적으로 테스트할 수 있습니다. 다음 섹션에서는 Controller Layer의 테스트 방법에 대해 알아보겠습니다.

# 5.4. Controller Layer 테스트
Controller Layer는 사용자의 요청을 받아 처리하고, 적절한 응답을 반환하는 계층입니다. 이 계층의 테스트는 사용자의 요청 처리와 관련된 로직, 예외 처리, 반환되는 응답의 형태 및 내용을 중점적으로 검증합니다. Mockito는 이 과정에서 Service Layer나 Repository Layer의 로직을 Mocking하여, Controller만의 독립된 테스트를 가능하게 해줍니다.

## Controller Layer의 테스트 목표
- 사용자 요청 처리 로직의 올바른 동작
- 예외 발생 시 적절한 응답 반환
- HTTP 응답 코드 및 반환 내용의 검증

## Spring Boot Test 환경에서 Controller 테스트하기
Spring Boot는 `MockMvc`라는 유용한 도구를 제공하여, 웹 애플리케이션의 Controller 계층을 쉽게 테스트할 수 있게 도와줍니다. 이를 사용하면 HTTP 요청을 생성하고, 반환되는 응답을 검증할 수 있습니다.

```java
@RunWith(SpringRunner.class)
@WebMvcTest(SomeController.class)
public class SomeControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private SomeService someService;

    @Test
    public void testGetEntityById() throws Exception {
        Long id = 1L;
        SomeDto expectedDto = new SomeDto(id, "testName");
        
        Mockito.when(someService.getEntityById(id)).thenReturn(expectedDto);

        mockMvc.perform(MockMvcRequestBuilders.get("/entities/{id}", id))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$.id", is(id)))
            .andExpect(jsonPath("$.name", is("testName")));
    }
}
```

이 예제에서는 `MockMvc`를 사용하여 `/entities/{id}` 경로로 요청을 보내고, 반환되는 응답 내용을 검증하는 과정을 보여줍니다. Mockito를 사용하여 Service 계층의 메소드를 모킹하였습니다.

## 예외 처리 테스트
Spring Boot에서 Controller 계층에서 발생한 예외를 적절하게 처리하는 것은 매우 중요합니다. Mockito를 사용하여 이러한 예외 상황을 효과적으로 테스트할 수 있습니다.

```java
@Test
public void testGetEntityById_NotFound() throws Exception {
    Long id = 999L;
    
    Mockito.when(someService.getEntityById(id)).thenThrow(new EntityNotFoundException("Entity not found"));

    mockMvc.perform(MockMvcRequestBuilders.get("/entities/{id}", id))
        .andExpect(status().isNotFound())
        .andExpect(content().string("Entity not found"));
}
```

이 예제에서는 존재하지 않는 Entity의 ID를 요청하였을 때, 적절한 응답 코드(404 Not Found)와 메시지를 반환하는지 테스트합니다.

## POST, PUT, DELETE 메소드 테스트
HTTP `POST`, `PUT`, `DELETE`와 같은 다양한 요청 메소드에 대한 테스트도 진행할 수 있습니다. 예를 들어, Entity를 생성하는 POST 요청을 테스트하려면 다음과 같이 할 수 있습니다.

```java
@Test
public void testCreateEntity() throws Exception {
    SomeDto requestDto = new SomeDto(null, "newEntity");
    SomeDto responseDto = new SomeDto(2L, "newEntity");

    Mockito.when(someService.createEntity(any(SomeDto.class))).thenReturn(responseDto);

    mockMvc.perform(MockMvcRequestBuilders.post("/entities")
            .contentType(MediaType.APPLICATION_JSON)
            .content(new ObjectMapper().writeValueAsString(requestDto)))
        .andExpect(status().isCreated())
        .andExpect(jsonPath("$.id", is(2L)))
        .andExpect(jsonPath("$.name", is("newEntity")));
}
```

> Controller Layer는 웹 애플리케이션의 진입점이므로, 해당 계층의 테스트는 애플리케이션의 안정성을 확보하는 데 중요한 역할을 합니다. Mockito와 Spring Boot의 MockMvc를 활용하면 다양한 요청 시나리오와 예외 상황에 대해 효과적으로 테스트할 수 있습니다. 다음 섹션에서는 Mocking의 Best Practices에 대해 알아보겠습니다.