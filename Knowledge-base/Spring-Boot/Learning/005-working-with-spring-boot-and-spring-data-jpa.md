---
title: 005: Spring Boot 및 Spring Data JPA 작업
description: 
published: true
date: 2023-02-03T07:43:44.916Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:43:43.284Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [005: Working with Spring Boot and Spring Data JPA***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/005-working-with-spring-boot-and-spring-data-jpa)
{.links-list}


# Spring Boot와 Spring Data JPA로 작업하기

이번 포스팅에서는 Spring Boot와 Spring Data JPA로 작업하는 방법에 대해 알아보겠습니다.

먼저 JPA가 무엇이고 JPA를 사용해야 하는 이유를 살펴보겠습니다. 그런 다음 JPA와 작동하도록 Spring Boot를 구성하는 방법을 살펴보겠습니다. 마지막으로 Spring Boot 애플리케이션에서 JPA를 사용하는 방법을 보여주는 몇 가지 간단한 예제 프로그램을 작성합니다.

## JPA란?

JPA는 Java Persistence API입니다. Java 개체를 관계형 데이터베이스에 매핑하는 방법에 대한 사양입니다.

JPA에는 많은 구현이 있으며 가장 인기 있는 것은 Hibernate입니다. JPA를 사용하면 JPA API에 대한 코드를 작성할 수 있고 JPA 구현(예: Hibernate)이 개체를 데이터베이스에 매핑하는 세부 사항을 처리하도록 할 수 있습니다.

## JPA를 사용하는 이유

애플리케이션에서 JPA를 사용하려는 몇 가지 이유가 있습니다.

- **JPA는 표준입니다**. 이는 선택할 수 있는 많은 JPA 구현이 있으며 필요한 경우 구현을 전환할 수 있음을 의미합니다.

- **JPA는 유연합니다**. 다양한 유형의 데이터베이스와 함께 JPA를 사용할 수 있으며 다양한 방식으로 Java 개체를 데이터베이스에 매핑할 수 있습니다.

- **JPA는 사용하기 쉽습니다**. JPA API는 사용하기 쉽도록 설계되었으므로 JPA를 빠르게 시작할 수 있습니다.

## JPA용 스프링 부트 구성

Spring Boot를 사용하면 JPA와 함께 사용하도록 Spring을 쉽게 구성할 수 있습니다. 프로젝트에 spring-boot-starter-data-jpa 의존성을 추가하기만 하면 됩니다.

이 종속성은 필요한 모든 JPA 종속성을 가져오고 JPA 구현(기본적으로 Hibernate)을 사용하도록 Spring Boot를 구성합니다.

## 스프링 부트에서 JPA 사용

이제 JPA를 사용하도록 Spring Boot를 구성했으므로 Spring Boot 애플리케이션에서 JPA를 사용하는 방법을 보여주는 몇 가지 예제 프로그램을 작성해 보겠습니다.

### 예 1: JPA 엔티티 생성

애플리케이션에서 JPA를 사용하려면 JPA 엔티티를 생성해야 합니다. JPA 엔터티는 데이터베이스 테이블에 매핑되는 Java 클래스입니다.

간단한 JPA 엔터티를 만들어 보겠습니다.

```java
@Entity
public class Person {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    // ... getters and setters
}
```

이 클래스는 데이터베이스의 `person` 테이블에 매핑됩니다. `@Entity` 주석은 이것이 JPA 엔티티임을 나타냅니다. `@Id` 주석은 `id` 필드가 엔티티의 기본 키임을 나타냅니다. `@GeneratedValue` 주석은 JPA에게 각 엔티티에 대한 고유 ID를 생성하도록 지시합니다.

### 예제 2: JPA 저장소 생성

이제 JPA 엔터티가 있으므로 액세스할 방법이 필요합니다. JPA 저장소를 생성하여 이를 수행할 수 있습니다.

JPA 리포지토리는 JPA 엔터티에 액세스하는 데 사용되는 Spring 데이터 리포지토리입니다. JPA 리포지토리를 생성하려면 `JpaRepository` 인터페이스를 확장하는 인터페이스를 생성해야 합니다.

```java
public interface PersonRepository extends JpaRepository<Person, Long> {

}
```

이 인터페이스는 `Person` 엔터티에 액세스하는 데 사용됩니다. `JpaRepository` 인터페이스는 JPA 엔터티 작업을 위한 많은 메서드를 제공하므로 이 인터페이스를 구현하기 위해 코드를 작성할 필요가 없습니다.

### 예 3: JPA 저장소 사용

이제 JPA 엔터티와 리포지토리가 있으므로 리포지토리를 사용하여 엔터티를 생성, 읽기, 업데이트 및 삭제하는 프로그램을 작성해 보겠습니다.

먼저 프로그램에 `PersonRepository`를 삽입합니다.

```java
@Autowired
private PersonRepository personRepository;
```

다음으로 리포지토리를 사용하여 `Person` 엔터티를 만듭니다.

```java
Person person = new Person();
person.setName("John Doe");

personRepository.save(person);
```

이렇게 하면 `person` 테이블에 새 행이 삽입됩니다. 'save' 메서드는 엔터티에 대한 고유 ID를 생성하고 엔터티에 설정합니다.

`findById` 메서드를 사용하여 ID로 엔터티를 검색할 수 있습니다.

```java
Person person = personRepository.findById(1L);
```

`findAll` 메서드를 사용하여 모든 항목을 검색할 수 있습니다.

```java
List<Person> people = personRepository.findAll();
```

엔티티를 삭제하기 위해 `deleteById` 메소드를 사용할 수 있습니다:

```java
personRepository.deleteById(1L);
```

그리고 `delete` 메서드를 사용하여 엔터티를 삭제할 수 있습니다.

```java
personRepository.delete(person);
```

이들은 `JpaRepository` 인터페이스에서 사용할 수 있는 메소드 중 일부에 불과합니다. 메서드의 전체 목록은 [JpaRepository 설명서](https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/JpaRepository.html)를 참조하세요. .

## 결론

이번 포스팅에서는 Spring Boot와 Spring Data JPA로 작업하는 방법에 대해 알아보았습니다. JPA를 사용하도록 Spring Boot를 구성하는 방법을 보았고 Spring Boot 애플리케이션에서 JPA를 사용하는 방법을 보여주는 몇 가지 간단한 예제 프로그램을 작성했습니다.