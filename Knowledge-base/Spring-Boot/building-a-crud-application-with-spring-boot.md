---
title: Spring Boot로 CRUD 애플리케이션 구축
description: 
published: true
date: 2023-02-06T08:33:25.979Z
tags: 
editor: markdown
dateCreated: 2023-02-06T08:33:24.329Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building a CRUD Application with Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/building-a-crud-application-with-spring-boot)
{.links-list}


# Spring Boot로 CRUD 애플리케이션 구축

CRUD(Create, Read, Update, Delete) 애플리케이션 개발은 웹 애플리케이션을 구축할 때 일반적인 요구 사항입니다. Spring Boot를 사용하면 "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다. 이 기사에서는 Spring Boot로 CRUD 애플리케이션을 만드는 방법에 중점을 둘 것입니다.

## 스프링부트란?

Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 만드는 데 사용되는 Java 기반 프레임워크입니다. Spring 플랫폼과 타사 라이브러리에 대한 독단적인 관점을 취하므로 최소한의 소란으로 시작할 수 있습니다. 대부분의 Spring Boot 애플리케이션에는 Spring 구성이 거의 필요하지 않습니다.

## 스프링 부트를 사용하는 이유는 무엇입니까?

SpringBoot는 웹 애플리케이션을 쉽게 개발할 수 있는 여러 기능을 제공합니다.

- Tomcat, Jetty 또는 Undertow를 직접 포함할 수 있습니다(WAR 파일을 배포할 필요 없음).
- 구성에 대한 독단적인 접근 방식을 사용합니다.
- 상용구 코드를 줄입니다.
- 메트릭, 상태 확인 및 외부화된 구성과 같은 프로덕션 준비 기능을 제공합니다.

## 시작하기

이 섹션에서는 Spring Boot로 간단한 CRUD 애플리케이션을 만드는 방법을 보여줍니다.

### 전제 조건

이 문서를 따라 하려면 다음이 필요합니다.

- 자바 8 이상
- 스프링 부트 2.0 이상
- 선택한 IDE
- 메이븐 3.0 이상

### 프로젝트 만들기

먼저 IDE에서 Maven 프로젝트를 만듭니다. "Spring Boot" 스타터 프로젝트와 "web" 모듈을 선택했는지 확인하십시오.

![스프링 부트 프로젝트 생성](https://i.imgur.com/5BkRJN4.png)

### 종속성 추가

다음으로 `pom.xml` 파일에 몇 가지 종속성을 추가해야 합니다.

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <scope>runtime</scope>
    </dependency>
</dependencies>
```

`spring-boot-starter-data-jpa` 종속성은 프로젝트에 Spring Data 및 Hibernate를 추가합니다. `spring-boot-starter-web` 종속성은 Spring MVC 및 Tomcat을 추가합니다. 마지막으로 `postgresql` 종속성은 PostgreSQL 드라이버를 추가합니다.

### 데이터베이스 구성

다음으로 데이터베이스를 구성해야 합니다. 이 예에서는 PostgreSQL을 사용하지만 원하는 데이터베이스를 사용할 수 있습니다.

먼저 `src/main/resources` 디렉토리에 `application.properties`라는 파일을 만들고 다음 줄을 추가합니다.

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=postgres
spring.datasource.password=postgres
spring.jpa.show-sql=true
```

이렇게 하면 포트 5432의 localhost에서 실행되는 PostgreSQL 데이터베이스에 연결하도록 애플리케이션이 구성됩니다. 사용자 이름과 비밀번호는 모두 'postgres'입니다.

### 엔터티 만들기

이제 엔터티 클래스를 만들어야 합니다. 엔터티는 데이터베이스 테이블을 나타내는 Java 클래스입니다. 이 예에서는 `User` 엔터티를 만듭니다.

```java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;
    // ... getters and setters
}
```

`@Entity` 주석은 Hibernate에게 이 클래스가 엔티티임을 알려줍니다. `@Id` 주석은 Hibernate에게 `id` 필드가 기본 키임을 알려줍니다. `@GeneratedValue` 주석은 기본 키에 대한 고유한 값을 생성하도록 Hibernate에 지시합니다.

### 저장소 생성

다음으로 저장소 인터페이스를 만들어야 합니다. 리포지토리는 데이터를 저장하고 검색하는 방법을 제공하는 Java 인터페이스입니다. 이 예에서는 `UserRepository` 인터페이스를 만듭니다.

```java
public interface UserRepository extends CrudRepository<User, Long> {
}
```

`CrudRepository` 인터페이스는 CRUD 작업을 위한 메서드를 제공합니다. 이 인터페이스를 사용하여 `UserRepository`를 구현할 것입니다.

### 서비스 만들기

이제 서비스 클래스를 만들어야 합니다. 서비스는 비즈니스 로직을 포함하는 Java 클래스입니다. 이 예에서는 `UserService` 클래스를 만듭니다.

```java
@Service
public class UserService {
    private final UserRepository userRepository;
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
    public User createUser(User user) {
        return userRepository.save(user);
    }
    public User getUserById(Long id) {
        return userRepository.findById(id).orElseThrow(() -> new RuntimeException("User not found"));
    }
    public List<User> getAllUsers() {
        return userRepository.findAll();
    }
    public User updateUser(User user) {
        return userRepository.save(user);
    }
    public void deleteUserById(Long id) {
        userRepository.deleteById(id);
    }
}
```

`@Service` 어노테이션은 Spring에게 이것이 서비스 bean임을 알려줍니다. `UserService` 클래스에는 사용자 생성, 검색, 업데이트 및 삭제를 위한 메서드가 포함되어 있습니다.

### 컨트롤러 만들기

다음으로 컨트롤러 클래스를 만들어야 합니다. 컨트롤러는 HTTP 요청을 처리하기 위한 메서드를 포함하는 Java 클래스입니다. 이 예에서는 `UserController` 클래스를 만듭니다.

```java
@RestController
@RequestMapping("/users")
public class UserController {
    private final UserService userService;
    public UserController(UserService userService) {
        this.userService = userService;
    }
    @PostMapping
    public User createUser(@RequestBody User user) {
        return userService.createUser(user);
    }
    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        return userService.getUserById(id);
    }
    @GetMapping
    public List<User> getAllUsers() {
        return userService.getAllUsers();
    }
    @PutMapping
    public User updateUser(@RequestBody User user) {
        return userService.updateUser(user);
    }
    @DeleteMapping("/{id}")
    public void deleteUserById(@PathVariable Long id) {
        userService.deleteUserById(id);
    }
}
```

`@RestController` 주석은 이것이 컨트롤러 빈임을 Spring에 알려줍니다. `@RequestMapping` 주석은 HTTP 요청을 컨트롤러 메서드에 매핑합니다. `UserController` 클래스에는 사용자 생성, 검색, 업데이트 및 삭제를 위한 메서드가 포함되어 있습니다.

### 애플리케이션 실행

이제 애플리케이션을 구성했으므로 실행할 수 있습니다. 애플리케이션을 실행하려면 `Application` 클래스에서 `main` 메서드를 실행하기만 하면 됩니다.

```java
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

응용 프로그램은 포트 8080에서 시작됩니다.

## 애플리케이션 테스트

이제 애플리케이션이 실행 중이므로 테스트해 보겠습니다. 애플리케이션에 HTTP 요청을 보내기 위해 `curl`을 사용할 수 있습니다.

### 사용자 만들기

사용자를 생성하기 위해 `POST` 메소드를 사용할 수 있습니다.

```
curl -X POST localhost:8080/users -d '{"name": "John Doe", "email": "john.doe@example.com"}' -H "Content-Type: application/json"
```

그러면 이름이 'John Doe'이고 이메일 주소가 'john.doe@example.com'인 사용자가 생성됩니다.

### ID로 사용자 가져오기

사용자를 검색하기 위해 `GET` 메서드를 사용할 수 있습니다.

```
curl localhost:8080/users/1
```

ID가 '1'인 사용자를 검색합니다.

### 모든 사용자 가져오기

모든 사용자를 검색하려면 `GET` 메서드를 사용할 수 있습니다.

```
curl localhost:8080/users
```

그러면 모든 사용자가 검색됩니다.

### 사용자 업데이트

사용자를 업데이트하려면 `PUT` 메서드를 사용할 수 있습니다.

```
curl -X PUT localhost:8080/users -d '{"id": "1", "name": "John Doe", "email": "john.doe@example.com"}' -H "Content-Type: application/json"
```

이렇게 하면 ID가 '1'인 사용자가 업데이트됩니다.

### 사용자 삭제

사용자를 삭제하려면 `DELETE` 메소드를 사용할 수 있습니다.

```
curl -X DELETE localhost:8080/users/1
```

ID가 '1'인 사용자가 삭제됩니다.

## 결론

이 기사에서는 Spring Boot로 간단한 CRUD 애플리케이션을 만드는 방법을 보여주었습니다. 또한 `curl`을 사용하여 애플리케이션을 테스트하는 방법도 보여 주었습니다.

이제 Spring Boot로 CRUD 애플리케이션을 만드는 방법을 알았으므로 자신만의 애플리케이션을 만들 수 있습니다. Spring Boot 웹 사이트(https://spring.io/projects/spring-boot)에서도 자세한 정보를 찾을 수 있습니다.