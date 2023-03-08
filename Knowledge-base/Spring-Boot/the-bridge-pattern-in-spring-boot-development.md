---
title: Spring Boot 개발의 브리지 패턴
description: 
published: true
date: 2023-02-06T09:17:15.854Z
tags: 
editor: markdown
dateCreated: 2023-02-06T09:17:14.244Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [The Bridge Pattern in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-bridge-pattern-in-spring-boot-development)
{.links-list}


# Spring Boot 개발의 Bridge 패턴

가장 유용한 디자인 패턴 중 하나는 브리지 패턴입니다. 이 패턴은 구현에서 추상화를 분리하여 둘이 독립적으로 변경될 수 있도록 하는 데 유용합니다. 브리지 패턴은 종종 어댑터 패턴과 함께 사용됩니다.

Spring Boot에서 브리지 패턴은 기본 데이터베이스에서 애플리케이션을 분리하는 데 사용됩니다. 이는 Repository 및 @Transactional 주석을 사용하여 수행됩니다.

Repository 주석은 클래스를 저장소로 표시하는 데 사용됩니다. 리포지토리는 엔터티에 대한 CRUD 작업을 제공하는 클래스입니다. @Transactional 어노테이션은 메소드를 트랜잭션의 일부로 표시하는 데 사용됩니다.


다음은 저장소의 예입니다.

```java
@Repository
public class PersonRepository {
 
    @Transactional
    public void save(Person person) {
        // save person
    }
 
    @Transactional
    public Person findById(Long id) {
        // find person by id
    }
 
    @Transactional
    public void delete(Person person) {
        // delete person
    }
}
```

위의 예에서 PersonRepository 클래스는 리포지토리로 표시됩니다. save, findById 및 delete 메소드는 트랜잭션의 일부로 표시됩니다.

브리지 패턴은 구현에서 추상화를 분리하는 데 유용한 패턴입니다. Spring Boot에서 Repository 및 @Transactional 주석은 기본 데이터베이스에서 애플리케이션을 분리하는 데 사용됩니다.