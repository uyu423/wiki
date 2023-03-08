---
title: Spring Boot 개발의 인터페이스 분리 원칙
description: 
published: true
date: 2023-02-04T02:17:22.280Z
tags: 
editor: markdown
dateCreated: 2023-02-04T02:17:20.756Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [The Interface Segregation Principle in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-interface-segregation-principle-in-spring-boot-development)
{.links-list}


# Spring Boot 개발의 인터페이스 분리 원칙

ISP(Interface Segregation Principle)는 클라이언트가 사용하지 않는 방법에 의존하도록 강요해서는 안 된다는 소프트웨어 설계 원칙입니다.

즉, 사용하지 않는 메서드에 의존하지 않고 필요한 클래스에서 인터페이스를 구현할 수 있도록 인터페이스를 작고 집중적으로 유지하는 것이 가장 좋습니다.

이 원칙은 Robert C. Martin이 그의 저서 "Agile Software Development, Principles, Patterns, and Practices"에서 처음 정의했습니다.

## 인터페이스 분리 원칙 적용

소프트웨어를 설계할 때 인터페이스가 너무 크거나 너무 일반적이지 않도록 ISP를 염두에 두는 것이 중요합니다.

예를 들어 사용자 생성, 업데이트 및 삭제를 위한 메서드를 포함하는 사용자 서비스용 인터페이스를 고려하십시오.

```java
public interface UserService {
    
    public void createUser(User user);
    
    public void updateUser(User user);
    
    public void deleteUser(User user);
    
}
```

이 인터페이스를 구현하는 클래스는 사용자 생성만 지원하면 되더라도 세 가지 메서드 모두에 대한 구현을 제공해야 합니다.

더 나은 설계는 각 작업 유형에 대해 별도의 인터페이스를 갖는 것입니다.

```java
public interface UserService {
    
    public void createUser(User user);
    
}

public interface UserUpdateService {
    
    public void updateUser(User user);
    
}

public interface UserDeleteService {
    
    public void deleteUser(User user);
    
}
```

이 디자인은 각 인터페이스가 특정 작업에 초점을 맞추기 때문에 ISP와 더 일치합니다.

사용자 생성만 지원하면 되는 클래스는 다른 인터페이스에 의존하지 않고 ```UserService``` 인터페이스를 구현할 수 있습니다.

## 스프링 부트와 인터페이스 분리 원칙

Spring Boot는 Java 애플리케이션 개발에 널리 사용되는 프레임워크입니다.

이는 명시적 구성보다 관례를 선호한다는 의미인 구성보다 관례의 원칙을 기반으로 합니다.

이 원칙은 인터페이스 설계에 적용될 수 있습니다.

예를 들어 ```UserService``` 인터페이스가 있는 Spring Boot 애플리케이션을 고려하십시오.

```java
@Service
public interface UserService {
    
    public void createUser(User user);
    
}
```

```@Service``` 주석은 이 인터페이스가 Spring 서비스임을 나타내는 데 사용됩니다.

Spring은 이 인터페이스에 대한 빈을 자동으로 생성하고 이를 필요로 하는 구성 요소에 주입합니다.

이 디자인은 인터페이스가 특정 작업(사용자 생성)에 초점을 맞추고 구성 요소가 사용하지 않는 방법에 의존할 필요가 없기 때문에 ISP와 일치합니다.