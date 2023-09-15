---
title: [Spring Boot + Mockito] 08. Mocking 외부 서비스와 인터페이스
description: 
published: true
date: 2023-09-15T10:14:30.106Z
tags: java, mockito, springboot, test
editor: markdown
dateCreated: 2023-09-15T09:57:55.323Z
---

# 8.1. RestTemplate, WebClient Mocking

외부 API 또는 서비스와의 통신은 대부분의 Spring Boot 어플리케이션에서 흔히 볼 수 있습니다. `RestTemplate`과 `WebClient`는 Spring Boot에서 외부 서비스와의 통신을 위해 주로 사용되는 도구입니다. 이러한 도구를 테스트하려면 해당 서비스를 호출하지 않고도 원하는 응답을 모의(mock)하여야 합니다.

## RestTemplate Mocking

RestTemplate은 전통적인 동기 방식의 HTTP 통신을 위한 클래스입니다. Mockito를 사용하여 `RestTemplate`의 메서드를 모의하려면 먼저 해당 객체를 Mock으로 생성해야 합니다.

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class ExternalServiceTest {

    @MockBean
    private RestTemplate restTemplate;

    @Autowired
    private ExternalService externalService;

    @Test
    public void testGetExternalData() {
        ResponseEntity<String> responseEntity = new ResponseEntity<>("Mocked Data", HttpStatus.OK);
        when(restTemplate.exchange(anyString(), any(), any(), eq(String.class)))
            .thenReturn(responseEntity);

        String result = externalService.getExternalData();
        assertEquals("Mocked Data", result);
    }
}
```

여기에서 `@MockBean` 어노테이션을 사용하여 Spring Context에 있는 `RestTemplate` 빈을 모의 객체로 대체합니다.

## WebClient Mocking

Spring WebFlux가 도입되면서, `WebClient`가 비동기, 반응형 웹 애플리케이션에서 `RestTemplate`의 대안으로 등장했습니다. `WebClient`를 mocking하는 것은 조금 더 복잡합니다.

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class ReactiveExternalServiceTest {

    @MockBean
    private WebClient.Builder webClientBuilder;

    @Mock
    private WebClient webClient;

    @Mock
    private WebClient.RequestHeadersSpec requestHeadersSpec;

    @Mock
    private WebClient.ResponseSpec responseSpec;

    @Autowired
    private ReactiveExternalService reactiveExternalService;

    @Test
    public void testGetReactiveData() {
        when(webClientBuilder.build()).thenReturn(webClient);
        when(webClient.get()).thenReturn(requestHeadersSpec);
        when(requestHeadersSpec.uri(anyString())).thenReturn(requestHeadersSpec);
        when(requestHeadersSpec.retrieve()).thenReturn(responseSpec);
        when(responseSpec.bodyToMono(String.class)).thenReturn(Mono.just("Mocked Reactive Data"));

        String result = reactiveExternalService.getReactiveData().block();
        assertEquals("Mocked Reactive Data", result);
    }
}
```

이 예제에서는 여러 `WebClient` 관련 객체들을 모의하여 외부 서비스 호출을 모방합니다.

> 외부 서비스와의 통신은 종종 예측할 수 없는 오류와 지연 시간을 가져올 수 있기 때문에, 테스트 환경에서 이를 제대로 모의하는 것은 중요합니다. Mockito를 사용하면 RestTemplate 및 WebClient의 동작을 쉽게 모의하고 원하는 결과를 반환하도록 설정할 수 있습니다. 이를 통해 외부 서비스와의 실제 통신 없이도 서비스의 로직을 안정적으로 테스트할 수 있습니다.

# 8.2. MongoTemplate Mocking

MongoDB는 다양한 어플리케이션에서 널리 사용되는 NoSQL 데이터베이스입니다. Spring Boot에서는 `MongoTemplate`을 활용해 MongoDB와의 연동을 쉽게 관리할 수 있습니다. 그러나 M`ongoTemplate`의 메서드들을 직접 테스트하는 것은 복잡하고, 때로는 비효율적일 수 있습니다. Mockito를 활용하면 이러한 메서드들을 효과적으로 모의할 수 있습니다.

## MongoTemplate의 기본 Mocking
먼저, Spring Boot 테스트 환경에서 MongoTemplate을 모의하기 위해 `@MockBean` 어노테이션을 활용합니다.

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class MongoServiceTest {

    @MockBean
    private MongoTemplate mongoTemplate;

    @Autowired
    private MongoService mongoService;

    @Test
    public void testFindAll() {
        List<Document> documents = Arrays.asList(new Document("key", "value"));
        when(mongoTemplate.findAll(Document.class)).thenReturn(documents);

        List<Document> result = mongoService.findAll();
        assertEquals(1, result.size());
        assertEquals("value", result.get(0).getString("key"));
    }
}
```

## 쿼리 메서드 Mocking

`MongoTemplate`의 `find`, `findOne`, `insert`와 같은 쿼리 메서드들도 쉽게 모의할 수 있습니다. 이러한 메서드들은 Query 객체와 함께 사용되기 때문에, 이를 고려하여 Mockito의 `when()` 메서드를 활용하여 적절한 반환 값을 설정합니다.

```java
@Test
public void testFindByKey() {
    Document mockDocument = new Document("key", "value");
    when(mongoTemplate.findOne(any(Query.class), eq(Document.class)))
        .thenReturn(mockDocument);

    Document result = mongoService.findByKey("key");
    assertEquals("value", result.getString("key"));
}
```

## 오류 시나리오 Mocking
때로는 `MongoTemplate`의 메서드 호출 중 오류가 발생하는 시나리오를 테스트해야 할 수도 있습니다. Mockito는 예외 발생 시나리오도 쉽게 모의할 수 있습니다.

```java
@Test(expected = RuntimeException.class)
public void testInsertErrorScenario() {
    doThrow(new RuntimeException("DB error")).when(mongoTemplate).insert(any(Document.class));
    mongoService.insert(new Document());
}
```

> MongoTemplate을 사용하여 MongoDB와의 연동을 관리하는 Spring Boot 어플리케이션에서는 데이터베이스와의 실제 연동 없이 서비스 로직을 테스트하기 위해 Mockito를 활용하는 것이 중요합니다. MongoTemplate의 다양한 메서드들을 Mockito를 사용하여 모의함으로써, 다양한 시나리오에 대한 테스트를 빠르고 효과적으로 수행할 수 있습니다.

# 8.3. KafkaTemplate Mocking

Kafka는 대규모 스트림 처리를 위한 분산 메시징 시스템으로 널리 알려져 있습니다. Spring Boot에서는 `KafkaTemplate`을 통해 Kafka 프로듀서(Producer)와의 연동을 관리합니다. 실제 Kafka 클러스터 없이 `KafkaTemplate`의 메서드를 테스트하기 위해 Mockito를 활용하면, 테스트 실행 속도의 향상 및 특정 시나리오를 재현하기 용이합니다.

## KafkaTemplate의 기본 Mocking
먼저, `KafkaTemplate`의 기본 사용법을 모의하기 위해 `@MockBean` 어노테이션을 사용하여 `KafkaTemplate` 객체를 모킹합니다.

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class KafkaServiceTest {

    @MockBean
    private KafkaTemplate<String, String> kafkaTemplate;

    @Autowired
    private KafkaService kafkaService;

    @Test
    public void testSend() {
        String topic = "test-topic";
        String message = "Hello Kafka!";
        kafkaService.sendMessage(topic, message);

        verify(kafkaTemplate, times(1)).send(topic, message);
    }
}
```

## KafkaTemplate의 결과 및 콜백 Mocking
Kafka 메시지를 보낼 때, 결과나 실패에 대한 콜백(callback)을 처리할 수 있습니다. Mockito를 사용하면 이러한 콜백을 테스트할 수 있습니다.

```java
@Test
public void testSendMessageWithCallbackSuccess() {
    String topic = "test-topic";
    String message = "Hello Kafka!";
    ListenableFuture<SendResult<String, String>> future = mock(ListenableFuture.class);

    when(kafkaTemplate.send(anyString(), anyString())).thenReturn(future);
    kafkaService.sendMessageWithCallback(topic, message);

    verify(future, times(1)).addCallback(any(SuccessCallback.class), any(FailureCallback.class));
}
```

## 예외 시나리오 Mocking

`KafkaTemplate`의 메서드 호출 중 예외가 발생하는 시나리오를 모의하기 위해 Mockito의 `doThrow()` 메서드를 사용할 수 있습니다.

```java
@Test(expected = KafkaException.class)
public void testSendErrorScenario() {
    doThrow(new KafkaException("Kafka error")).when(kafkaTemplate).send(anyString(), anyString());
    kafkaService.sendMessage("test-topic", "Hello Kafka!");
}
```

> 실제 Kafka 클러스터와의 통신 없이 `KafkaTemplate`의 다양한 메서드들과 그 반응을 테스트하기 위해 Mockito를 활용하는 것은 매우 효과적입니다. Kafka와의 통신 오류나 성공적인 전송 시나리오, 콜백 처리 등 다양한 상황을 손쉽게 재현하여 테스트할 수 있습니다. 이로써 서비스 로직의 안정성을 높이는 데 큰 도움이 됩니다.

# 8.4. RedisTemplate Mocking

Redis는 인-메모리 데이터 구조 저장소로, 다양한 경우에 사용됩니다. Spring Boot에서는 `RedisTemplate`을 통해 Redis와의 연동을 관리합니다. 실제 Redis 서버 없이 `RedisTemplate`의 메서드를 테스트하기 위해 Mockito를 활용하면, 테스트 실행 속도의 향상 및 특정 시나리오를 재현하기 용이합니다.

## RedisTemplate의 기본 Mocking

먼저, RedisTemplate의 기본 사용법을 모의하기 위해 @MockBean 어노테이션을 사용하여 RedisTemplate 객체를 모킹합니다.

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class RedisServiceTest {

    @MockBean
    private RedisTemplate<String, String> redisTemplate;

    @Autowired
    private RedisService redisService;

    @Test
    public void testSetAndGet() {
        String key = "test-key";
        String value = "Hello Redis!";
        when(redisTemplate.opsForValue().get(key)).thenReturn(value);
        
        String result = redisService.getValue(key);
        
        assertEquals(value, result);
    }
}
```

## RedisTemplate의 다양한 연산 Mocking

RedisTemplate은 여러 Redis 데이터 구조와 연산을 지원합니다. 예를 들어, `Set`, `List`, `Hash` 등의 연산을 모의할 수 있습니다.

```java
@Test
public void testListOperations() {
    String key = "test-list";
    String value = "Redis List Item";
    
    ListOperations<String, String> listOperations = mock(ListOperations.class);
    when(redisTemplate.opsForList()).thenReturn(listOperations);
    when(listOperations.rightPop(key)).thenReturn(value);
    
    String result = redisService.popFromList(key);
    
    assertEquals(value, result);
}
```

## 예외 시나리오 Mocking

`RedisTemplate`의 메서드 호출 중 예외가 발생하는 시나리오를 모의하기 위해 Mockito의 `doThrow()` 메서드를 사용할 수 있습니다.

```java
@Test(expected = RedisConnectionFailureException.class)
public void testRedisErrorScenario() {
    doThrow(new RedisConnectionFailureException("Redis connection error")).when(redisTemplate).opsForValue().get(anyString());
    redisService.getValue("test-key");
}
```

> 실제 Redis 서버와의 통신 없이 RedisTemplate의 다양한 메서드들과 그 반응을 테스트하기 위해 Mockito를 활용하는 것은 매우 효과적입니다. Redis 연산 오류나 특정 데이터 구조의 동작, Redis와의 통신 문제 등 다양한 상황을 손쉽게 재현하여 테스트할 수 있습니다. 이로써 서비스 로직의 안정성을 높이는 데 큰 도움이 됩니다.

# 8.5. MyBatis Mappers Mocking

MyBatis는 개발자가 SQL 매핑 문장과 Java 코드를 분리하여 관리할 수 있게 해주는 퍼시스턴스 프레임워크입니다. Spring Boot와 함께 사용될 때, Mapper 인터페이스를 통해 데이터베이스 연산을 추상화할 수 있습니다. 테스트 시, 실제 데이터베이스 연결 없이 Mapper의 동작을 모의(mock)하여 빠르고 안정적인 테스트를 구성할 수 있습니다.

## 기본 MyBatis Mapper Mocking

먼저, MyBatis의 Mapper 인터페이스를 Mockito로 모킹하는 기본 방법을 살펴봅니다.

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class UserServiceTest {

    @Mock
    private UserMapper userMapper;

    @InjectMocks
    private UserService userService;

    @Test
    public void getUserByIdTest() {
        User mockUser = new User(1, "John", "Doe");
        when(userMapper.findUserById(1)).thenReturn(mockUser);
        
        User user = userService.getUserById(1);
        
        assertEquals(mockUser, user);
    }
}
```

## 복잡한 쿼리 결과 Mocking
복잡한 쿼리나 여러 조건을 가진 메서드를 테스트할 때도 Mockito를 활용하여 원하는 결과를 반환하도록 설정할 수 있습니다.

```java
@Test
public void getUsersByRoleTest() {
    List<User> mockUsers = Arrays.asList(
        new User(1, "John", "Admin"),
        new User(2, "Jane", "Admin")
    );
    
    when(userMapper.findUsersByRole("Admin")).thenReturn(mockUsers);
    
    List<User> users = userService.getUsersByRole("Admin");
    
    assertEquals(2, users.size());
    assertEquals("Admin", users.get(0).getRole());
}
```

## 예외 시나리오 Mocking

데이터베이스 연산 중 예외가 발생하는 시나리오를 재현하기 위해 Mockito의 `doThrow()` 메서드를 활용할 수 있습니다.

```java
@Test(expected = DataAccessException.class)
public void testDatabaseErrorScenario() {
    doThrow(new DataAccessException("DB Error")).when(userMapper).findUserById(anyInt());
    
    userService.getUserById(1);
}
```

> 실제 데이터베이스와의 통신 없이 MyBatis의 Mapper 메서드들의 동작을 모킹하면, 테스트 실행 시간을 줄이고, 다양한 시나리오를 쉽게 재현하여 서비스 로직의 안정성을 높일 수 있습니다. MyBatis와 Mockito를 적절히 조합하면, 복잡한 데이터베이스 로직도 견고하게 테스트할 수 있습니다.
  
# 8.6. JPA Repositories Mocking

Spring Data JPA는 자바 개발자들이 데이터 접근 계층을 효과적으로 구현할 수 있게 해주는 프레임워크입니다. Repository 인터페이스만을 정의하면 Spring Data JPA가 해당 인터페이스를 구현해 줍니다. 이러한 메커니즘은 테스트에서도 도움을 줄 수 있는데, 실제 데이터베이스 연동 없이 Repository의 동작을 Mockito를 통해 모의(Mock)할 수 있습니다.

## 기본 JPA Repository Mocking
JPA의 Repository 인터페이스를 Mockito로 모킹하는 방법부터 살펴봅니다.

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class BookServiceTest {

    @Mock
    private BookRepository bookRepository;

    @InjectMocks
    private BookService bookService;

    @Test
    public void findBookByIdTest() {
        Book mockBook = new Book(1L, "Sample Title", "Sample Author");
        when(bookRepository.findById(1L)).thenReturn(Optional.of(mockBook));
        
        Book book = bookService.findBookById(1L);
        
        assertEquals(mockBook, book);
    }
}
```
## 다양한 Repository 메서드 Mocking

Spring Data JPA에서 제공하는 다양한 메서드(`save`, `findAll`, `delete` 등)도 Mockito를 활용하여 모킹할 수 있습니다.

```java
@Test
public void saveBookTest() {
    Book mockBook = new Book(null, "New Title", "New Author");
    Book savedBook = new Book(2L, "New Title", "New Author");
    
    when(bookRepository.save(mockBook)).thenReturn(savedBook);
    
    Book result = bookService.saveBook(mockBook);
    
    assertEquals(savedBook.getId(), result.getId());
}
```

## Custom Query Mocking

사용자 정의 쿼리를 가진 메서드의 경우도 Mockito를 통해 원하는 동작을 반환하도록 설정할 수 있습니다.

```java
@Test
public void findBooksByAuthorTest() {
    List<Book> mockBooks = Arrays.asList(
        new Book(1L, "Title1", "AuthorA"),
        new Book(2L, "Title2", "AuthorA")
    );
    
    when(bookRepository.findByAuthor("AuthorA")).thenReturn(mockBooks);
    
    List<Book> books = bookService.findBooksByAuthor("AuthorA");
    
    assertEquals(2, books.size());
}
```

## 예외 시나리오 Mocking

데이터베이스 연산 중 예외가 발생할 수 있는 시나리오를 재현하기 위해 Mockito의 `doThrow()` 메서드를 활용할 수 있습니다.

```java
@Test(expected = DataIntegrityViolationException.class)
public void testDuplicateBookSaveScenario() {
    Book mockBook = new Book(null, "Duplicate Title", "AuthorB");
    
    doThrow(new DataIntegrityViolationException("Duplicate entry"))
        .when(bookRepository).save(mockBook);
    
    bookService.saveBook(mockBook);
}
```

> Spring Data JPA의 Repository 인터페이스를 Mockito를 통해 모킹하면, 실제 데이터베이스 연동 없이 서비스 로직을 테스트할 수 있습니다. 이를 통해 테스트의 실행 속도를 높이고, 다양한 시나리오와 예외 상황에 대한 테스트를 쉽게 작성할 수 있습니다. JPA와 Mockito의 조합은 데이터베이스 관련 로직을 안정적으로 테스트하는 데 매우 효과적입니다.