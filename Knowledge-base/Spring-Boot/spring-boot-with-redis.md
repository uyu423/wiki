---
title: Redis를 사용한 스프링 부트
description: 
published: true
date: 2023-02-07T11:32:59.252Z
tags: 
editor: markdown
dateCreated: 2023-02-07T11:32:53.558Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot with Redis***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-with-redis)
{.links-list}


# Redis를 사용한 스프링 부트

Redis는 데이터베이스, 캐시 및 메시지 브로커로 사용되는 오픈 소스 인 메모리 데이터 구조 저장소입니다. 문자열, 해시, 목록, 집합, 범위 쿼리가 있는 정렬된 집합, 비트맵, 하이퍼로그 및 반경 쿼리가 있는 지리 공간 인덱스와 같은 데이터 구조를 지원합니다.

이 기사에서는 Redis에서 Spring Boot를 사용하는 방법을 보여줍니다.

## 레디스란?

Redis는 데이터베이스, 캐시 및 메시지 브로커로 사용되는 오픈 소스(BSD 라이센스), 메모리 내 데이터 구조 저장소입니다. 문자열, 해시, 목록, 집합, 범위 쿼리가 포함된 정렬된 집합, 비트맵, 하이퍼로그 및 반경 쿼리가 포함된 지리 공간 인덱스와 같은 데이터 구조를 지원합니다.

Redis는 기본 제공 복제, Lua 스크립팅, LRU 제거, 트랜잭션 및 다양한 수준의 온디스크 지속성을 갖추고 있으며 Redis Sentinel을 통한 고가용성 및 Redis 클러스터를 통한 자동 파티셔닝을 제공합니다.

## Redis를 사용한 스프링 부트

Spring Boot는 Redis에 대한 최고 수준의 지원을 제공합니다. 이 섹션에서는 Redis에서 Spring Boot를 사용하는 방법을 보여줍니다.

Redis와 통신하기 위해 [lettuce](https://github.com/lettuce-io/lettuce-core) 라이브러리를 사용할 것입니다. Lettuce는 Redis 연결을 처리하기 위한 Netty 기반의 완전한 비차단 Redis 클라이언트이고 객체 매핑을 위한 Spring Data입니다.

### 메이븐 종속성

먼저 `pom.xml`에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-redis</artifactId>
</dependency>
```

### 레디스 구성

기본적으로 Spring Boot는 `localhost:6379`에서 Redis 서버를 찾습니다. application.properties 파일에서 `spring.redis.host` 및 `spring.redis.port` 속성을 설정하여 이를 변경할 수 있습니다.

```properties
spring.redis.host=localhost
spring.redis.port=6379
```

비밀번호로 보호된 경우 Redis에 비밀번호를 지정할 수도 있습니다.

```properties
spring.redis.password=secret
```

### 스프링 데이터 레디스

Spring Data Redis는 Spring Data의 Redis 특정 구현입니다. [Jedis](https://github.com/xetorthio/jedis) 및 [Lettuce](https://github.com/lettuce-io/lettuce-core) Redis 클라이언트의 추상화를 제공하고 통합 객체를 제공합니다. - Redis용 매퍼 인터페이스.

#### Redis 템플릿

RedisTemplate은 Spring Data Redis의 중심 클래스입니다. Spring 애플리케이션에서 사용되는 데이터 유형에 대한 상위 수준 Redis 작업을 정의합니다.

Spring 애플리케이션 컨텍스트에서 RedisTemplate을 구성할 수 있습니다.

```java
@Bean
public RedisTemplate<String, Object> redisTemplate(
        RedisConnectionFactory factory) {
    RedisTemplate<String, Object> template = new RedisTemplate<>();
    template.setConnectionFactory(factory);
    return template;
}
```

#### StringRedis템플릿

StringRedisTemplate은 Redis에서 문자열 기반 데이터를 처리하기 위한 특수 RedisTemplate입니다.

Spring 애플리케이션 컨텍스트에서 StringRedisTemplate을 구성할 수 있습니다.

```java
@Bean
public StringRedisTemplate stringRedisTemplate(
        RedisConnectionFactory factory) {
    StringRedisTemplate template = new StringRedisTemplate();
    template.setConnectionFactory(factory);
    return template;
}
```

### Redis 리포지토리

Spring Data Redis는 Redis 특정 저장소 추상화를 제공합니다. 이 추상화를 사용하여 Redis 리포지토리를 만들 수 있습니다.

먼저 Repository 인터페이스를 확장하는 Redis 특정 인터페이스를 생성해야 합니다.

```java
public interface PersonRepository extends Repository<Person, String> {

    Person findById(String id);

    List<Person> findAll();

    Person save(Person person);

    void delete(Person person);
}
```

다음으로 PersonRepository 인터페이스 구현을 만들어야 합니다.

```java
@Service
public class PersonRepositoryImpl implements PersonRepository {

    private final RedisTemplate<String, Person> redisTemplate;

    @Autowired
    public PersonRepositoryImpl(RedisTemplate<String, Person> redisTemplate) {
        this.redisTemplate = redisTemplate;
    }

    @Override
    public Person findById(String id) {
        return redisTemplate.opsForValue().get(id);
    }

    @Override
    public List<Person> findAll() {
        return redisTemplate.opsForValue().multiGet(redisTemplate.keys("*"));
    }

    @Override
    public Person save(Person person) {
        redisTemplate.opsForValue().set(person.getId(), person);
        return person;
    }

    @Override
    public void delete(Person person) {
        redisTemplate.delete(person.getId());
    }
}
```

위의 예에서는 RedisTemplate을 사용하여 Redis와 상호 작용합니다.

### 스프링 데이터 레디스와 잭슨

Spring Data Redis는 JSON으로 객체를 직렬화 및 역직렬화하기 위해 Jackson을 사용합니다. 기본적으로 Jackson은 JAXB 주석 인트로스펙터를 사용하도록 구성됩니다.

application.properties 파일에서 `spring.jackson.deserialization.USE_JACKSON_ANNOTATIONS` 속성을 `true`로 설정하여 JAXB 주석 검사기 대신 Jackson 주석 검사기를 사용하도록 Jackson을 구성할 수 있습니다.

```properties
spring.jackson.deserialization.USE_JACKSON_ANNOTATIONS=true
```

사용자 정의 ObjectMapper를 사용하여 Jackson 주석 인트로스펙터를 사용하도록 Jackson을 구성할 수도 있습니다.

```java
@Bean
public ObjectMapper objectMapper() {
    ObjectMapper mapper = new ObjectMapper();
    mapper.configure(DeserializationFeature.USE_JACKSON_ANNOTATIONS, true);
    return mapper;
}
```

## 결론

이 기사에서는 Redis에서 Spring Boot를 사용하는 방법을 설명했습니다.