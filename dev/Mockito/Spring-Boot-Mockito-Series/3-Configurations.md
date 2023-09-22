---
title: [Spring Boot + Mockito] 03. 환경 설정
description: 
published: true
date: 2023-09-22T05:47:34.619Z
tags: java, mockito, springboot
editor: markdown
dateCreated: 2023-09-15T09:04:12.357Z
---

# 3.1. Maven과 Gradle 의존성 추가

Spring Boot 프로젝트에서 Mockito를 사용하기 위해서는 해당 라이브러리의 의존성을 프로젝트에 추가해야 합니다. 이 섹션에서는 Maven과 Gradle을 사용하는 프로젝트에 Mockito 의존성을 추가하는 방법을 소개하겠습니다.

## 1. Maven 의존성 추가

Maven을 사용하는 경우, `pom.xml` 파일에 아래의 의존성을 추가합니다.

```xml
<!-- Mockito core dependency -->
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>3.X.X</version>
    <scope>test</scope>
</dependency>

<!-- Spring Boot Test Starter for Mockito Integration -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

> 주의: 3.X.X 부분은 Mockito의 최신 버전 번호로 교체해야 합니다. Maven Central Repository에서 최신 버전을 확인하실 수 있습니다.
{.is-warning}

## 2. Gradle 의존성 추가

Gradle을 사용하는 경우, `build.gradle` 파일에 아래의 의존성을 추가합니다.

```groovy
// Mockito core dependency
testImplementation 'org.mockito:mockito-core:3.X.X'

// Spring Boot Test Starter for Mockito Integration
testImplementation 'org.springframework.boot:spring-boot-starter-test'
```

> 주의: 여기서도 3.X.X 부분은 Mockito의 최신 버전 번호로 교체해야 합니다.
{.is-warning}

Mockito는 Spring Boot 테스트 환경과 통합이 잘 되어 있습니다. 위의 의존성 추가만으로 Spring Boot에서 Mockito를 활용하여 유닛 테스트를 작성할 준비가 완료됩니다. 추가적인 설정 없이 바로 테스트 코드 작성을 시작할 수 있습니다.

# 3.2. Spring Boot 테스트 환경 설정

Spring Boot 프로젝트에서 Mockito를 성공적으로 사용하기 위해서는 테스트 환경을 제대로 설정하는 것이 중요합니다. 이 섹션에서는 Spring Boot의 테스트 환경을 설정하고, Mockito를 통합하는 방법에 대해 설명하겠습니다.

## 1. 기본 테스트 환경 설정

Spring Boot는 기본적으로 `@SpringBootTest` 애너테이션을 제공합니다. 이 애너테이션은 Spring Boot 환경 아래에서 전체 테스트를 실행하는 데 사용됩니다. 또한, 자동 구성(Auto-Configuration)이 적용되어 별도의 추가 설정 없이도 테스트 환경이 구성됩니다.

```java
@SpringBootTest
public class MyServiceTest {

    @Autowired
    private MyService myService;

    @Test
    public void testMyServiceMethod() {
        // 테스트 코드 작성
    }
}
```

## 2. Mockito 통합

Spring Boot와 Mockito를 통합하기 위해서는 `@MockBean` 애너테이션을 사용하면 됩니다. 이 애너테이션은 Spring의 `ApplicationContext`에 mock 객체를 등록해줍니다. 따라서, 원래의 빈 대신 mock 객체가 사용됩니다.

```java
@SpringBootTest
public class MyServiceTest {

    @MockBean
    private MyRepository myRepository;

    @Autowired
    private MyService myService;

    @Test
    public void testMyServiceMethod() {
        // Mockito를 사용하여 myRepository의 동작을 stubbing
        when(myRepository.findByName(anyString())).thenReturn(Optional.of(new MyEntity()));

        // 테스트 코드 작성
    }
}
```

## 3. 테스트 슬라이스 (Test Slices) 사용

때때로 전체 `ApplicationContext`를 로드하는 대신 특정 레이어만 테스트하고 싶을 수 있습니다. Spring Boot는 이러한 경우를 위해 Test Slices라는 기능을 제공합니다. 예를 들어, 서비스 레이어만 테스트하려면 `@ServiceTest`, 데이터 접근 레이어만 테스트하려면 `@DataJpaTest` 애너테이션을 사용할 수 있습니다.

```java
@ServiceTest
public class MyServiceTest {

    @MockBean
    private MyRepository myRepository;

    @Autowired
    private MyService myService;

    // 테스트 코드 작성
}
```


> 아래는 Spring Boot에서 자주 사용되는 테스트 슬라이스의 종류입니다:
> 
> - **@WebMvcTest**: 웹 레이어와 관련된 부분만을 테스트합니다. Controller 및 RestController가 대상입니다. Service, Repository는 포함되지 않습니다.
> - **@DataJpaTest**: JPA와 관련된 테스트를 위한 설정만 로드합니다. 주로 Repository 레이어의 테스트에 사용됩니다.
> - **@JdbcTest**: JDBC에 대한 테스트를 위한 설정만 로드합니다.
> - **@DataMongoTest**: MongoDB와 관련된 테스트를 위한 설정만 로드합니다.
> - **@WebFluxTest**: Reactive 웹 애플리케이션의 컨트롤러를 테스트합니다.
> - **@RestClientTest**: REST 클라이언트(RestTemplate 및 WebClient)를 테스트합니다.
> - **@JsonTest**: JSON 직렬화 및 역직렬화를 테스트합니다. 주로 Jackson 또는 Gson과 같은 라이브러리에 대한 테스트에 사용됩니다.
> - **@DataLdapTest**: LDAP와 관련된 테스트를 위한 설정만 로드합니다.
> - **@DataRedisTest**: Redis와 관련된 테스트를 위한 설정만 로드합니다.
> - **@JooqTest**: JOOQ와 관련된 테스트를 위한 설정만 로드합니다.
> 
> 이를 통해 불필요한 빈들의 로딩을 줄이고, 테스트 속도를 향상시킬 수 있습니다.
{.is-info}


> Spring Boot의 테스트 환경 설정은 매우 유연하며, Mockito와의 통합도 쉽습니다. 본 섹션에서는 기본적인 설정 방법만을 소개하였으나, Spring Boot의 다양한 테스트 기능들을 활용하면 더욱 효율적이고 다양한 테스트 케이스를 작성할 수 있습니다.

# 3.3. Mockito 초기 설정

Mockito를 Spring Boot 프로젝트에 성공적으로 통합하려면 초기 설정 과정이 필요합니다. 이 설정은 Mockito의 기능을 최대한 활용하고 Spring Boot와의 호환성을 보장하기 위해 필요한 절차입니다. 이 섹션에서는 Mockito의 초기 설정 방법에 대해 자세히 설명합니다.

## Mockito 의존성 추가

먼저, Maven 또는 Gradle을 사용하여 프로젝트에 Mockito 의존성을 추가해야 합니다. 이는 3.1 절에서 이미 언급되었으므로 생략하겠습니다.

## Mockito 확장자 사용

Mockito의 핵심 기능 중 일부는 Mockito 확장자를 사용하여 제공됩니다. 가장 일반적으로 사용되는 확장자는 `MockitoJUnitRunner` 입니다. 이를 사용하면 `@Mock` 애너테이션을 사용하여 쉽게 mock 객체를 생성할 수 있습니다.

```java
@RunWith(MockitoJUnitRunner.class)
public class MyServiceTest {

    @Mock
    private MyRepository myRepository;

    @InjectMocks
    private MyService myService;

    // 테스트 코드 작성
}
```

`@InjectMocks` 애너테이션은 mock 객체와 함께 사용되는 실제 객체에 mock 객체를 주입하는 데 사용됩니다.

> **Q. @InjectMocks 과 @Mock 은 무슨 차이가 있습니까?**
> 
> `@InjectMocks`와 `@Mock`은 Mockito에서 제공하는 애너테이션으로, 객체 모킹과 관련된 두 가지 주요 기능을 수행합니다. 그렇지만 각각의 목적과 사용 방법은 다릅니다.
> 
> **@Mock**
> 
> `@Mock` 애너테이션은 특정 클래스나 인터페이스의 Mock 객체를 생성합니다.
> Mock 객체는 실제 객체의 동작을 수행하지 않지만, 해당 객체가 어떻게 사용되는지를 확인하고 그에 따른 결과나 동작을 시뮬레이션할 수 있습니다.
> 
> ```java
> @Mock
> private SampleRepository sampleRepository;
> ```
> 위 예제에서 `SampleRepository`의 Mock 객체가 생성되며, 이를 통해 해당 Repository의 메서드 호출을 모킹하거나 검증할 수 있습니다.
> 
> **@InjectMocks**
> 
> `@InjectMocks` 애너테이션은 주입해야 할 실제 객체의 인스턴스를 생성하며, 이 객체에 `@Mock` (또는 `@Spy`)로 생성된 객체를 자동으로 주입(inject)합니다.
> 주로 테스트하려는 서비스 또는 컨트롤러와 같은 클래스에 사용되며, 해당 클래스가 의존하는 다른 객체들을 Mock으로 주입받을 필요가 있을 때 사용합니다.
> 
> ```java
> @InjectMocks
> private SampleService sampleService;
> ```
> 위 예제에서 `SampleService`의 실제 인스턴스가 생성되고, 해당 서비스가 의존하는 모든 Mock 객체 (`@Mock`로 표시된 객체들)가 자동으로 주입됩니다.

## Mockito 설정 (MockitoSettings)

Mockito의 동작 방식을 더 세밀하게 제어하려면 `@MockitoSettings` 애너테이션을 사용할 수 있습니다. 예를 들어, strict stubbing 모드를 활성화하려면 다음과 같이 설정할 수 있습니다.

```java
@MockitoSettings(strictness = Strictness.STRICT_STUBS)
public class MyServiceTest {

    //...
}
```

strict stubbing 모드는 불필요한 stubbing을 감지하고 이에 대해 경고 메시지를 출력하도록 도와줍니다.


## BDD 스타일 초기 설정

BDD(Behavior Driven Development) 스타일로 Mockito를 사용하려는 경우 `BDDMockito` 클래스를 사용하여 mock과 stubbing을 설정할 수 있습니다. 이 스타일은 가독성이 뛰어나며, 비즈니스 요구 사항에 중점을 둡니다.

```java
@RunWith(MockitoJUnitRunner.class)
public class MyServiceTest {

    @Mock
    private MyRepository myRepository;

    @InjectMocks
    private MyService myService;

    @Test
    public void testBDDStyle() {
        // given
        given(myRepository.findByName(anyString())).willReturn(Optional.of(new MyEntity()));

        // when
        MyEntity result = myService.findByName("testName");

        // then
        assertThat(result).isNotNull();
    }
}
```

Mockito의 초기 설정은 비교적 간단하지만, 프로젝트의 요구 사항과 개발 스타일에 따라 다양한 설정 옵션을 제공합니다. 위에서 소개한 설정은 Mockito를 Spring Boot와 효과적으로 통합하는 데 필요한 기본적인 절차를 담고 있습니다. 앞으로의 핸드북에서는 이러한 설정을 바탕으로 Mockito의 다양한 기능과 활용 방법을 소개하겠습니다.

- [[Spring Boot + Mockito] 04. Mockito 기본 사용 방법
](/ko/dev/Mockito/Spring-Boot-Mockito-Series/4-Mockito-basic-usage)
{.links-list}