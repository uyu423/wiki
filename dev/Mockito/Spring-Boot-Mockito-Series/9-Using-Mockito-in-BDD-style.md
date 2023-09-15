---
title: [Spring Boot + Mockito] 09. BDD (Behavior Driven Development) 스타일로 Mockito 활용하기
description: 
published: true
date: 2023-09-15T10:14:39.830Z
tags: java, mockito, springboot, test
editor: markdown
dateCreated: 2023-09-15T10:03:47.333Z
---

# 9.1. BDD와 Mockito

## BDD (Behavior Driven Development)란?

BDD (Behavior Driven Development, 행위 주도 개발)는 테스트 주도 개발(TDD)에서 발전된 형태로, 비즈니스 요구 사항과 소프트웨어 개발 사이의 간극을 줄이기 위해 만들어진 방법론입니다. BDD는 시스템의 행동에 초점을 맞추며, 자연어 스타일의 표현을 사용해 테스트 케이스를 작성합니다. 이를 통해 비개발자들과의 협업과 소통이 쉬워집니다.

## Mockito와 BDD 스타일

Mockito는 BDD 스타일의 테스팅을 지원하기 위해 `BDDMockito` 클래스를 제공합니다. `BDDMockito`는 기존의 Mockito API를 BDD 스타일로 감싼 것입니다. 따라서, 기본적인 사용 방법은 기존의 Mockito와 크게 다르지 않습니다. 다만, 테스트 코드의 가독성과 이해도를 높이는 데 중점을 둡니다.

## 기본 사용법

BDD 스타일의 Mockito는 주로 `given`, `when`, `then` 패턴을 사용하여 테스트를 작성합니다.

- **given**: 시스템의 특정 상태를 설정합니다. (사전 조건)
- **when**: 시스템에 특정 작업을 수행합니다. (동작)
- **then**: 시스템의 행동이 예상대로 이루어졌는지 확인합니다. (검증)

```java
import static org.mockito.BDDMockito.*;

@RunWith(SpringRunner.class)
@SpringBootTest
public class BookServiceTest {

    @Mock
    private BookRepository bookRepository;

    @InjectMocks
    private BookService bookService;

    @Test
    public void findBookByIdTest() {
        // given
        Book mockBook = new Book(1L, "Sample Title", "Sample Author");
        given(bookRepository.findById(1L)).willReturn(Optional.of(mockBook));
        
        // when
        Book book = bookService.findBookById(1L);
        
        // then
        assertThat(book).isEqualTo(mockBook);
    }
}
```

이러한 방식은 테스트의 의도와 결과를 명확하게 표현하며, 팀원이나 다른 이해 관계자들이 테스트 코드를 쉽게 이해할 수 있도록 도와줍니다.

## 예외 처리와 BDD

Mockito의 BDD 스타일을 사용하여 예외 상황을 모킹하는 것도 가능합니다.

```java
@Test
public void findBookByNonExistentIdTest() {
    // given
    given(bookRepository.findById(999L)).willThrow(new NoSuchElementException());
    
    // when
    assertThrows(NoSuchElementException.class, () -> {
        bookService.findBookById(999L);
    });

    // then - assertThrows에서 예외가 처리됨
}
```

> BDD는 개발자와 비개발자 모두에게 테스트의 의도와 결과를 명확하게 통일된 언어로 전달하는 강력한 도구입니다. Mockito의 BDD 스타일은 Spring Boot 환경에서 소프트웨어의 행동을 효과적으로 테스트하는 데 필수적인 도구로서, 테스트 코드의 가독성과 효율성을 높이는 데 크게 기여합니다.

# 9.2. BDD Mockito를 활용한 테스트 케이스 작성

BDD의 핵심은 "사전 조건 - 동작 - 결과"의 순서로 시나리오를 작성하는 것입니다. Mockito의 BDD 스타일은 이러한 BDD의 패턴을 따르며, 테스트를 더 명확하게 작성할 수 있도록 도와줍니다. 이 섹션에서는 BDD Mockito를 활용하여 Spring Boot 환경에서 테스트 케이스를 작성하는 방법을 알아봅니다.

## BDD Mockito의 주요 API
Mockito는 BDD를 위한 별도의 API 세트를 제공합니다. 가장 자주 사용되는 메서드들은 다음과 같습니다.

- `given()`: 사전 조건을 설정합니다.
- `willReturn()`: 특정 메서드 호출 시 리턴 값이나 예외를 설정합니다.
- `willThrow()`: 특정 메서드 호출 시 예외를 발생시킵니다.
- `then()`: 검증할 메서드를 지정합니다.

## 테스트 케이스 작성 순서

### 1. 사전 조건 설정 (given)

첫 단계에서는 테스트의 초기 상태를 설정합니다. 예를 들어, Mock 객체가 어떤 메서드를 호출했을 때 어떤 값을 반환하거나 예외를 발생시킬 것인지 설정할 수 있습니다.

```java
given(mockRepository.findById(anyLong())).willReturn(Optional.of(sampleBook));
```

### 2. 액션 수행 (when)

테스트하려는 기능 또는 메서드를 실행합니다.

```java
Book book = bookService.findBookById(1L);
```

### 3. 검증 (then)

메서드의 결과나 Mock 객체의 상태를 검증합니다.

```java
then(mockRepository).should(times(1)).findById(anyLong());
assertThat(book).isEqualTo(sampleBook);
```

### 실제 테스트 케이스 예제

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class BookServiceTest {

    @Mock
    private BookRepository mockRepository;

    @InjectMocks
    private BookService bookService;

    private Book sampleBook;

    @Before
    public void setup() {
        sampleBook = new Book(1L, "Sample Title", "Sample Author");
    }

    @Test
    public void findBookById_shouldReturnBook() {
        // given
        given(mockRepository.findById(anyLong())).willReturn(Optional.of(sampleBook));

        // when
        Book book = bookService.findBookById(1L);

        // then
        then(mockRepository).should(times(1)).findById(anyLong());
        assertThat(book).isEqualTo(sampleBook);
    }
}
```

> BDD 스타일로 Mockito를 활용하여 테스트 케이스를 작성하면, 테스트의 의도와 결과를 명확하게 파악할 수 있습니다. 또한, BDD 스타일은 비개발자와의 협업을 강화하고, 테스트의 가독성을 높이는 데 큰 역할을 합니다. Spring Boot 환경에서 BDD Mockito를 올바르게 활용하면, 더욱 효과적이고 효율적인 테스트 케이스를 작성할 수 있습니다.