---
title: EhCache를 사용한 스프링 부트 캐싱
description: 
published: true
date: 2023-02-07T16:32:42.008Z
tags: 
editor: markdown
dateCreated: 2023-02-07T16:32:36.249Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Caching with EhCache***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-caching-with-ehcache)
{.links-list}


# EhCache를 사용한 스프링 부트 캐싱

캐싱은 애플리케이션의 성능과 확장성을 개선하기 위한 일반적인 기술입니다. 데이터베이스를 쿼리하지 않고도 빠르게 검색할 수 있도록 자주 액세스하는 데이터를 메모리에 캐시하는 데 사용할 수 있습니다.

Spring Boot를 사용할 때 @EnableCaching 주석을 사용하여 애플리케이션에서 EhCache를 활성화할 수 있습니다. 이 기사에서는 Spring Boot에서 EhCache를 구성하고 사용하는 방법을 살펴보겠습니다.

## EhCache 구성

EhCache를 구성하려면 src/main/resources 디렉토리에 ehcache.xml 파일을 생성해야 합니다. 파일 내용은 다음과 같아야 합니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="ehcache.xsd"
         updateCheck="true"
         monitoring="autodetect"
         dynamicConfig="true">
    <diskStore path="java.io.tmpdir"/>
    <cache name="defaultCache"
           maxElementsInMemory="10000"
           overflowToDisk="true"
           eternal="false"
           timeToIdleSeconds="120"
           timeToLiveSeconds="120"
           diskPersistent="false"
           diskExpiryThreadIntervalSeconds="120"
           memoryStoreEvictionPolicy="LRU">
        <persistence strategy="localTempSwap"/>
    </cache>
</ehcache>
```

ehcache.xml 파일에서 "defaultCache"라는 캐시를 구성했습니다. 이 캐시는 애플리케이션에서 데이터를 캐시하는 데 사용됩니다. 캐시는 오버플로에 대해 로컬 디스크 저장소를 사용하고 120초 동안 액세스되지 않은 항목을 만료하도록 구성됩니다.

## 스프링 부트로 캐싱

이제 EhCache를 구성했으므로 Spring Boot 애플리케이션에서 사용할 수 있습니다. 먼저 Application 클래스에 @EnableCaching 주석을 추가해야 합니다.

```java
@SpringBootApplication
@EnableCaching
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

다음으로 @Cacheable 주석으로 캐시하려는 서비스 클래스의 메서드에 주석을 달아야 합니다.

```java
@Service
public class UserService {

    @Cacheable(value = "users")
    public List<User> getUsers() {
        // query database for users
        return users;
    }
}
```

위의 코드에서 getUsers() 메서드에 @Cacheable을 주석으로 추가했습니다. 이는 "사용자" 캐시에서 이 메소드의 결과를 캐시하도록 Spring에 지시합니다.

이제 getUsers() 메서드를 호출하면 처음으로 데이터베이스를 쿼리하고 결과를 반환합니다. 두 번째로 호출하면 캐시에서 결과를 반환합니다.

## 캐시된 데이터 업데이트

데이터베이스의 데이터가 업데이트될 때 캐시된 데이터는 자동으로 업데이트되지 않는다는 점에 유의해야 합니다. 캐시를 업데이트하려면 @CacheEvict 주석을 사용해야 합니다.

```java
@Service
public class UserService {

    @CacheEvict(value = "users", allEntries = true)
    public void updateUser(User user) {
        // update user in database
    }
}
```

위의 코드에서 @CacheEvict로 updateUser() 메서드에 주석을 달았습니다. 이것은 이 메소드가 호출될 때 "사용자" 캐시에서 모든 항목을 제거하도록 Spring에 지시합니다.

이제 updateUser() 메서드를 호출하면 캐시가 지워지고 다음에 getUsers() 메서드를 호출하면 데이터베이스를 쿼리하고 업데이트된 결과를 반환합니다.

## 결론

이 기사에서는 Spring Boot에서 EhCache를 구성하고 사용하는 방법을 살펴보았습니다. 캐싱은 애플리케이션의 성능을 향상시키는 좋은 방법이 될 수 있습니다. 자주 액세스하는 데이터를 메모리에 캐싱하면 매번 데이터베이스를 쿼리하지 않아도 됩니다.