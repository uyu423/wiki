---
title: Spring Data JPA: 고급 기술
description: 
published: true
date: 2023-02-06T23:17:42.593Z
tags: 
editor: markdown
dateCreated: 2023-02-06T23:17:40.923Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Data JPA: Advanced Techniques***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-data-jpa-advanced-techniques)
{.links-list}


# 스프링 데이터 JPA: 고급 기술

JPA(Java Persistence API)는 관계형 데이터베이스에서 데이터를 저장, 액세스 및 관리하기 위한 Java 사양입니다. Spring Data JPA는 JPA의 Spring 프레임워크 구현으로 Spring 애플리케이션에서 JPA로 작업하기가 더 쉬워집니다.

이 기사에서는 다음을 포함하여 Spring Data JPA의 일부 고급 주제를 다룰 것입니다.

- 예측
- Querydsl
- 기준 API

## 예측

프로젝션은 데이터베이스에서 검색하려는 엔터티의 필드를 지정하는 방법입니다. Spring Data JPA는 두 가지 유형의 프로젝션을 지원합니다.

- 인터페이스 기반 프로젝션
- 동적 프로젝션

### 인터페이스 기반 프로젝션

인터페이스 기반 프로젝션을 사용하여 검색하려는 필드를 정의하는 인터페이스를 생성하고 Spring Data JPA는 런타임에 해당 인터페이스의 구현을 생성합니다. 이는 IDE의 형식 안전성 및 코드 완성 기능을 활용할 수 있으므로 프로젝션을 사용하는 데 권장되는 방법입니다.

인터페이스 기반 프로젝션을 사용하려면 먼저 검색하려는 필드를 정의하는 인터페이스를 만들어야 합니다.

```java
public interface UserNameOnly {
    String getUsername();
}
```

그런 다음 쿼리에서 해당 인터페이스를 사용할 수 있습니다.

```java
List<UserNameOnly> users = userRepository.findAll(projection(UserNameOnly.class));
```

### 동적 프로젝션

동적 프로젝션을 사용하면 검색하려는 필드를 문자열로 지정할 수 있습니다. 이는 인터페이스 기반 프로젝션보다 형식 안전성이 떨어지지만 엔터티 모델의 일부가 아닌 필드를 검색하려는 경우에 유용할 수 있습니다.

동적 프로젝션을 사용하려면 먼저 검색하려는 필드를 정의하는 클래스를 만들어야 합니다.

```java
public class UserNameOnly {
    private String username;

    public String getUsername() {
        return username;
    }
}
```

그런 다음 쿼리에서 해당 클래스를 사용할 수 있습니다.

```java
List<UserNameOnly> users = userRepository.findAll(projection(UserNameOnly.class, "username"));
```

## 쿼리dsl

Querydsl은 Java 기반 도메인별 언어로 형식이 안전한 쿼리를 만들 수 있는 라이브러리입니다. JPA, JDO 및 기타 데이터 액세스 프레임워크와 함께 사용할 수 있습니다.

Querydsl을 Spring Data JPA와 함께 사용하려면 Querydsl JPA 종속성을 프로젝트에 추가해야 합니다.

```xml
<dependency>
    <groupId>com.querydsl</groupId>
    <artifactId>querydsl-jpa</artifactId>
    <version>${querydsl.version}</version>
</dependency>
```

또한 엔터티에 대한 코드를 생성하도록 Querydsl을 구성해야 합니다.

```xml
<build>
    <plugins>
        ...
        <plugin>
            <groupId>com.mysema.maven</groupId>
            <artifactId>apt-maven-plugin</artifactId>
            <version>1.1.3</version>
            <configuration>
                <outputDirectory>target/generated-sources/java</outputDirectory>
                <processor>com.querydsl.apt.jpa.JPAAnnotationProcessor</processor>
            </configuration>
            <executions>
                <execution>
                    <goals>
                        <goal>process</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
        ...
    </plugins>
</build>
```

Querydsl이 구성되면 이를 사용하여 유형이 안전한 쿼리를 생성할 수 있습니다.

```java
QUser user = QUser.user;
List<User> users = queryFactory
    .selectFrom(user)
    .where(user.username.eq("johndoe"))
    .fetch();
```

## 기준 API

Criteria API는 유형이 안전한 쿼리를 작성하기 위한 Java API입니다. JPA 사양의 일부이며 모든 JPA 호환 데이터 액세스 프레임워크와 함께 사용할 수 있습니다.

Spring Data JPA에서 Criteria API를 사용하려면 CriteriaQuery를 생성해야 합니다.

```java
CriteriaBuilder builder = entityManager.getCriteriaBuilder();
CriteriaQuery<User> criteria = builder.createQuery(User.class);
```

그런 다음 CriteriaQuery를 사용하여 쿼리를 작성할 수 있습니다.

```java
Root<User> user = criteria.from(User.class);
criteria.select(user);
criteria.where(builder.equal(user.get("username"), "johndoe"));
```

마지막으로 쿼리를 실행할 수 있습니다.

```java
List<User> users = entityManager.createQuery(criteria).getResultList();
```

## 결론

이 기사에서는 프로젝션, Querydsl 및 Criteria API를 포함하여 Spring Data JPA의 일부 고급 주제를 다루었습니다. 또한 Spring 애플리케이션에서 이러한 각 기능을 사용하는 방법도 살펴보았습니다.