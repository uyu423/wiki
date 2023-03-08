---
title: 스프링 부트와 하이버네이트 통합
description: 
published: true
date: 2023-02-06T07:32:35.445Z
tags: 
editor: markdown
dateCreated: 2023-02-06T07:32:29.629Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Integrating Hibernate with Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/integrating-hibernate-with-spring-boot)
{.links-list}


# 스프링 부트와 하이버네이트 통합

이 기사에서는 Hibernate를 Spring Boot 프레임워크와 통합하는 방법을 살펴보겠습니다.

## 하이버네이트란?

Hibernate는 Java 애플리케이션 지속성의 개발을 단순화하는 Java 프레임워크입니다. 관계형 데이터베이스에 데이터를 저장하기 위한 강력한 개체 관계형 매핑 도구를 제공합니다.

## 스프링부트란?

Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 응용 프로그램을 만드는 간단한 방법을 제공하는 Java 기반 프레임워크입니다. 마이크로서비스 구축에 탁월한 선택입니다.

## Spring Boot와 함께 Hibernate를 사용하는 이유는 무엇입니까?

Hibernate는 관계형 데이터베이스를 Spring 기반 애플리케이션과 함께 사용하려는 Java 개발자에게 인기 있는 선택입니다. 설정이 쉽고 개체 캐싱 및 쿼리 최적화를 비롯한 다양한 기능이 있습니다.

## Hibernate를 Spring Boot와 통합하는 방법

Hibernate를 Spring Boot와 통합하는 두 가지 방법이 있습니다.

### 1. Spring Boot의 내장 Hibernate 지원 사용

Spring Boot는 Hibernate에 대한 내장 지원을 제공합니다. 프로젝트의 `pom.xml` 파일에 다음 종속성을 간단히 추가할 수 있습니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

이렇게 하면 Hibernate Core 및 JPA(Java Persistence API) 라이브러리를 포함하여 Hibernate에 필요한 모든 종속성이 추가됩니다.

### 2. Hibernate 전용 Spring Boot 스타터 사용

또는 Hibernate 구성에 대해 보다 세밀한 제어를 제공하는 Hibernate 관련 Spring Boot 스타터를 사용할 수 있습니다. 이 스타터를 사용하려면 프로젝트의 `pom.xml` 파일에 다음 종속성을 추가하십시오.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-hibernate</artifactId>
</dependency>
```

## Spring Boot로 Hibernate 구성

필요한 종속성을 추가했으면 `application.properties` 파일에 다음 속성을 추가하여 Hibernate를 구성할 수 있습니다.

```properties
# Hibernate settings
spring.jpa.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
spring.jpa.hibernate.ddl-auto=update
```

`spring.jpa.hibernate.dialect` 속성은 사용할 Hibernate 방언을 구성합니다. 이것은 Hibernate에게 Java 객체를 SQL 문으로 변환하는 방법을 알려줍니다.

`spring.jpa.hibernate.ddl-auto` 속성은 Hibernate의 자동 DDL 모드를 구성합니다. 이는 엔티티에 필요한 SQL 스키마를 자동으로 생성하도록 Hibernate에 지시합니다. '업데이트' 모드는 스키마가 변경된 경우 업데이트하지만 존재하지 않는 경우 생성하지 않습니다.

## Hibernate 엔티티 생성

Hibernate 엔터티를 생성하려면 데이터베이스의 테이블을 나타내는 Java 클래스를 생성하기만 하면 됩니다. 예를 들어 다음 코드는 `User` 항목을 정의합니다.

```java
@Entity
public class User {
 
    @Id
    @GeneratedValue
    private Long id;
 
    @Column(nullable = false)
    private String name;
 
    // ...
}
```

`@Entity` 주석은 클래스를 Hibernate 엔티티로 표시합니다. `@Id` 주석은 `id` 필드를 기본 키로 표시합니다. `@Column` 주석은 `name` 필드를 데이터베이스 테이블의 열로 표시합니다.

## Hibernate 저장소 생성

Hibernate 저장소를 생성하려면 `CrudRepository` 인터페이스를 확장하는 인터페이스를 생성하기만 하면 됩니다. 예를 들어 다음 코드는 `UserRepository`를 정의합니다.

```java
public interface UserRepository extends CrudRepository<User, Long> {
}
```

이 저장소는 `User` 엔터티에 대한 기본 CRUD 작업을 제공합니다.

## 리포지토리를 서비스에 주입

리포지토리를 서비스에 주입하려면 `@Autowired` 주석을 사용할 수 있습니다. 예를 들어 다음 코드는 `UserRepository`를 `UserService`에 삽입합니다.

```java
@Service
public class UserService {
 
    @Autowired
    private UserRepository userRepository;
 
    // ...
}
```

## 저장소 사용

리포지토리를 서비스에 주입하면 이를 사용하여 엔터티에서 CRUD 작업을 수행할 수 있습니다. 예를 들어 다음 코드는 새 `사용자`를 만듭니다.

```java
@Service
public class UserService {
 
    @Autowired
    private UserRepository userRepository;
 
    public User create(String name) {
        User user = new User();
        user.setName(name);
        return userRepository.save(user);
    }
 
    // ...
}
```

## 참조

- [하이버네이트](https://hibernate.org/)
- [스프링 부트](https://spring.io/projects/spring-boot)
- [스프링 데이터 JPA](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/# reference)
- [스프링 데이터 하이버네이트](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-sql.html# boot-features-hibernate)