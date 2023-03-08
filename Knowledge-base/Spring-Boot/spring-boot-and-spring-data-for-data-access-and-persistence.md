---
title: 데이터 액세스 및 지속성을 위한 Spring Boot 및 Spring 데이터
description: 
published: true
date: 2023-02-08T06:32:33.276Z
tags: 
editor: markdown
dateCreated: 2023-02-08T06:32:31.674Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot and Spring Data for Data Access and Persistence***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-spring-data-for-data-access-and-persistence)
{.links-list}


# 데이터 액세스 및 지속성을 위한 스프링 부트 및 스프링 데이터

## 소개

Spring Boot는 CLI, 임베디드 Tomcat 및 자동 구성을 비롯한 다양한 기능을 제공하는 널리 사용되는 Java 웹 애플리케이션 프레임워크입니다. Spring Data는 Java 애플리케이션을 위한 데이터 액세스 및 지속성 솔루션을 제공하는 데 중점을 둔 Spring의 하위 프로젝트입니다.

이 기사에서는 Spring Boot 및 Spring Data를 사용하여 관계형 데이터베이스의 데이터에 액세스하고 유지하는 방법을 살펴보겠습니다. 또한 Spring Data가 Java 애플리케이션의 데이터 액세스 및 지속성을 위해 좋은 선택이 되도록 하는 몇 가지 기능을 살펴보겠습니다.

## 관계형 데이터베이스를 위한 Spring Boot 구성

Spring Boot는 MySQL, PostgreSQL 및 Oracle을 비롯한 다양한 관계형 데이터베이스와 함께 작동하도록 구성할 수 있습니다. 이 섹션에서는 MySQL 데이터베이스와 작동하도록 Spring Boot를 구성하는 방법을 살펴보겠습니다.

먼저 `pom.xml` 파일에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

다음으로 `application.properties` 파일에서 몇 가지 속성을 구성해야 합니다.

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydatabase
spring.datasource.username=myusername
spring.datasource.password=mypassword

spring.jpa.database=MYSQL
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update
```

`spring.datasource` 속성에서 MySQL 데이터베이스의 URL, 사용자 이름 및 암호를 구성하고 있습니다. `spring.jpa` 속성에서 데이터베이스 유형(MySQL)을 구성하고 Spring Boot에 SQL 쿼리를 표시하도록 지시하고 Hibernate에게 데이터베이스 스키마를 자동으로 업데이트하도록 지시합니다.

## 스프링 데이터로 데이터 접근하기

Spring Data를 사용하면 Java로 관계형 데이터베이스의 데이터에 쉽게 액세스할 수 있습니다. 이 섹션에서는 스프링 데이터를 사용하여 MySQL 데이터베이스의 데이터에 액세스하는 방법을 살펴보겠습니다.

먼저 데이터에 대한 `@Repository` 인터페이스를 생성해야 합니다.

```java
@Repository
public interface MyRepository extends JpaRepository<MyEntity, Long> {

}
```

`@Repository` 주석은 스프링에게 이것이 데이터 저장소임을 알려줍니다. `JpaRepository` 인터페이스는 관계형 데이터베이스의 데이터에 액세스하기 위한 메소드를 제공합니다. `MyEntity` 클래스는 데이터베이스의 행을 나타내는 엔티티 클래스입니다. `Long` 유형은 엔티티의 기본 키 유형입니다.

다음으로 엔터티 클래스를 만들어야 합니다.

```java
@Entity
public class MyEntity {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    // Getters and setters
}
```

`@Entity` 주석은 이것이 엔티티 클래스임을 Spring에 알려줍니다. `@Id` 주석은 Spring에 `id` 필드가 엔티티의 기본 키임을 알려줍니다. `@GeneratedValue` 주석은 `id` 필드가 데이터베이스에 의해 자동으로 생성되어야 함을 Spring에 알립니다.

이제 리포지토리와 엔터티 클래스가 설정되었으므로 이를 사용하여 데이터베이스의 데이터에 액세스할 수 있습니다. 예를 들어 `findAll()` 메서드를 사용하여 데이터베이스의 모든 엔터티를 찾을 수 있습니다.

```java
List<MyEntity> myEntities = myRepository.findAll();
```

또한 `save()` 메서드를 사용하여 엔터티를 데이터베이스에 저장할 수 있습니다.

```java
MyEntity myEntity = new MyEntity();
myEntity.setName("John Smith");

myRepository.save(myEntity);
```

## 결론

이 기사에서는 Spring Boot 및 Spring Data를 사용하여 관계형 데이터베이스의 데이터에 액세스하고 데이터를 유지하는 방법을 살펴보았습니다. 또한 Spring Data가 Java 애플리케이션의 데이터에 쉽게 액세스하는 방법을 살펴보았습니다.