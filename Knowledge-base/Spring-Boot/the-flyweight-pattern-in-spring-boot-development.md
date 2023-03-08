---
title: Spring Boot 개발의 Flyweight 패턴
description: 
published: true
date: 2023-02-03T21:17:36.789Z
tags: 
editor: markdown
dateCreated: 2023-02-03T21:17:34.495Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [The Flyweight Pattern in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-flyweight-pattern-in-spring-boot-development)
{.links-list}


# Spring Boot 개발의 Flyweight 패턴

Flyweight 패턴은 많은 개체로 작업할 때 코드를 최적화하는 데 유용한 도구입니다. 핵심 아이디어는 새 개체를 만드는 대신 기존 개체를 재사용하여 시간과 메모리를 모두 절약할 수 있다는 것입니다.

Spring Boot 개발에서 플라이웨이트 패턴을 사용하여 공통 객체를 캐싱하고 요청에서 재사용함으로써 성능을 향상시킬 수 있습니다. 예를 들어 사용자 목록을 반환하는 서비스가 있는 경우 목록을 캐시하고 매번 데이터베이스에서 가져오는 대신 재사용할 수 있습니다.

Spring Boot에서 Flyweight 패턴을 구현하려면 Spring Cache 추상화를 사용할 수 있습니다. 이렇게 하면 캐시해야 하는 개체와 무효화 방법을 선언적으로 지정할 수 있습니다.

이 기사에서는 Spring Boot 개발에서 Flyweight 패턴을 사용하는 방법을 살펴보겠습니다. 패턴이 해결할 수 있는 문제부터 살펴보겠습니다. 그런 다음 Spring Cache 추상화를 사용하여 패턴을 구현하는 방법을 살펴보겠습니다. 마지막으로 Flyweight 패턴과 관련된 몇 가지 고급 주제를 살펴보겠습니다.

## 문제

사용자 관리를 위해 REST API를 노출하는 간단한 Spring Boot 애플리케이션을 고려하십시오. API에는 사용자 목록을 반환하는 GET 엔드포인트가 있습니다. 끝점은 다음과 같습니다.

```
@GetMapping("/users")
public List<User> getUsers() {
    return userService.getUsers();
}
```
@Repository
public interface UserRepository extends CrudRepository<User, Long> {

}
```
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public List<User> getUsers() {
        return userRepository.findAll();
    }

}
```
@서비스
공개 클래스 UserService {

    @Autowired
    개인 UserRepository userRepository;

    공개 목록<사용자> getUsers() {
        return userRepository.findAll();
    }

}
```

```UserService```는 ```UserRepository```를 사용하여 데이터베이스에서 사용자를 가져옵니다. ```UserRepository```는 간단한 CRUD 저장소입니다.

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-cache</artifactId>
</dependency>
```

이제 데이터베이스에 많은 수의 사용자가 있다고 가정합니다. ```/users``` 엔드포인트에 요청을 하면 데이터베이스에서 모든 사용자를 가져오는 데 시간이 오래 걸립니다. 이로 인해 애플리케이션이 느려지고 응답하지 않을 수 있습니다.

이 문제를 해결하는 한 가지 방법은 사용자 목록을 캐시하는 것입니다. 그렇게 하면 ```/users``` 엔드포인트에 요청을 할 때 매번 데이터베이스에서 가져오는 대신 캐시된 사용자 목록을 반환할 수 있습니다.

## 플라이웨이트 패턴 구현

Spring Cache 추상화를 사용하여 예제 애플리케이션에서 Flyweight 패턴을 구현할 수 있습니다. 먼저 ```pom.xml```에 ```spring-boot-starter-cache``` 종속성을 추가해야 합니다.

```
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    @Cacheable(value = "users")
    public List<User> getUsers() {
        return userRepository.findAll();
    }

}
```

다음으로 캐싱을 사용하도록 ```UserService```를 구성해야 합니다. ```@Cacheable``` 주석으로 ```getUsers()``` 메서드에 주석을 달아 이를 수행할 수 있습니다.

```
@Cacheable(value = "users", key = "#id")
public User getUserById(Long id) {
    return userRepository.findById(id).orElse(null);
}
```

```
@CacheEvict(value = "users", key = "#id")
public void deleteUserById(Long id) {
    userRepository.deleteById(id);
}
```/users``` 끝점에 요청하면 ```getUsers()``` 메서드가 캐시된 사용자 목록을 반환합니다. 메서드가 처음 호출되면 데이터베이스에서 사용자를 가져와 캐시합니다. 후속 호출은 단순히 캐시된 사용자 목록을 반환합니다.

캐시된 결과가 무효화되는 방식을 제어하기 위해 ```@Cacheable``` 주석을 구성할 수도 있습니다. 예를 들어 ```key``` 속성을 사용하여 캐시된 객체의 키를 지정할 수 있습니다.

```
@Cacheable(value = "users", expire = 60)
public List<User> getUsers() {
    return userRepository.findAll();
}
```

이 예에서는 캐시된 결과가 ```id``` 매개변수로 키가 지정되어야 한다고 지정했습니다. 이것은 ```id```가 변경될 때마다 캐시된 결과가 무효화됨을 의미합니다.

캐시에서 개체를 명시적으로 제거하기 위해 ```@CacheEvict``` 주석을 사용할 수도 있습니다.

```
@CacheEvict(value = "users", allEntries = true)
public void deleteUserById(Long id) {
    userRepository.deleteById(id);
}
```

이 예제에서는 ```@CacheEvict``` 주석을 사용하여 ```deleteUserById()``` 메서드에 주석을 추가했습니다. 이는 ```deleteUserById()``` 메소드가 호출될 때 ```getUserById()``` 메소드의 캐시된 결과를 제거하도록 Spring에 지시합니다.

## 고급 주제

언급할 가치가 있는 Flyweight 패턴과 관련된 몇 가지 고급 주제가 있습니다.

### 만료

기본적으로 Spring Cache 추상화는 일정 시간이 경과한 후 캐시된 객체를 만료시킵니다. 기본 만료 시간은 2시간입니다.

```
public class User {

    private Long id;

    private String name;

    private Date birthDate;

    // Getters and setters...

}
```
@Cacheable(값 = "사용자", 만료 = 60)
공개 목록<사용자> getUsers() {
    return userRepository.findAll();
}
```
public class User implements Serializable {

    private static final long serialVersionUID = 1L;

    private Long id;

    private String name;

    private Date birthDate;

    // Getters and setters...

}
```@CacheEvict``` 주석을 사용할 수도 있습니다:

```
public class SerializableUser implements Serializable {

    private static final long serialVersionUID = 1L;

    private User user;

    // Getters and setters...

}
```

이 예제에서는 ```@CacheEvict``` 주석을 사용하여 ```deleteUserById()``` 메서드에 주석을 추가했습니다. ```allEntries``` 속성은 Spring에게 ```users``` 캐시의 모든 객체를 만료시키라고 지시합니다.

### 직렬화

Spring Cache 추상화는 모든 유형의 개체를 캐시하는 데 사용할 수 있습니다. 그러나 CacheManager가 캐시된 개체를 직렬화 및 역직렬화한다는 사실을 인식하는 것이 중요합니다.

캐시된 개체를 직렬화할 수 없는 경우 문제가 발생할 수 있습니다. 예를 들어, 다음 ```User``` 클래스를 고려하십시오.

```
공개 클래스 사용자 {

    개인 긴 ID;

    개인 문자열 이름;

    비공개 날짜 생년월일;

    // 게터와 세터...

}
```

```User``` 클래스는 ```Date``` 필드를 포함하고 있기 때문에 직렬화할 수 없습니다. 이는 ```User``` 개체를 캐시할 수 없음을 의미합니다.

이 문제를 해결하는 한 가지 방법은 ```User``` 클래스를 직렬화할 수 있도록 만드는 것입니다.

```
공용 클래스 사용자는 직렬화 가능을 구현합니다. {

    개인 정적 최종 긴 serialVersionUID = 1L;

    개인 긴 ID;

    개인 문자열 이름;

    비공개 날짜 생년월일;

    // 게터와 세터...

}
```

이 예제에서는 ```serialVersionUID``` 필드를 추가하여 ```User``` 클래스를 직렬화할 수 있도록 했습니다. 이 필드는 ```Serializable``` 인터페이스에 필요합니다.

이 문제를 해결하는 또 다른 방법은 ```Serializable``` 래퍼 클래스를 사용하는 것입니다.

```
공개 클래스 SerializableUser는 Serializable을 구현합니다.

    개인 정적 최종 긴 serialVersionUID = 1L;

    개인 사용자 사용자;

    // 게터와 세터...

}
```

이 예제에서는 ```User``` 개체를 래핑하는 ```SerializableUser``` 클래스를 만들었습니다. 이를 통해 ```User``` 클래스를 직렬화할 필요 없이 ```SerializableUser``` 객체를 캐시할 수 있습니다.

## 결론

이 기사에서는 Spring Boot 개발에서 Flyweight 패턴을 사용하는 방법을 살펴보았습니다. 패턴이 해결할 수 있는 문제를 살펴보는 것부터 시작했습니다. 그런 다음 Spring Cache 추상화를 사용하여 패턴을 구현하는 방법을 살펴보았습니다. 마지막으로 Flyweight 패턴과 관련된 몇 가지 고급 주제를 살펴보았습니다.