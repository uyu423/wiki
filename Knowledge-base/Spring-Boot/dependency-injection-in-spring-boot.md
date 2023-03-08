---
title: Spring Boot에서 의존성 주입
description: 
published: true
date: 2023-01-31T14:57:25.348Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:57:23.769Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Dependency Injection in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/dependency-injection-in-spring-boot)
{.links-list}


# 스프링 부트에서 의존성 주입

## 소개

종속성 주입(DI)은 응용 프로그램의 모듈성을 높이기 위해 최신 프로그래밍에서 널리 사용되는 기술입니다. 개체에 종속성을 주입하면 이러한 종속성을 하드 코딩하지 않고 코드를 더 유연하고 테스트 및 유지 관리하기 쉽게 만들 수 있습니다.

이 기사에서는 Spring Framework의 컨텍스트에서 DI가 작동하는 방식과 이를 사용하여 Spring 기반 애플리케이션을 보다 모듈화하고 테스트하기 쉽게 만드는 방법을 살펴보겠습니다.

## 의존성 주입이란?

종속성 주입은 개체 자체에서 개체의 종속성을 분리하는 기술입니다.

전통적인 프로그래밍에서 개체는 종속성을 하드 코딩합니다. 즉, 이러한 종속성이 변경되면 개체도 변경되어야 합니다. 이 긴밀한 결합으로 인해 코드를 유지 관리하고 테스트하기가 어렵습니다.

DI를 사용하면 개체의 종속성이 하드 코딩되지 않고 런타임에 개체에 주입됩니다. 이를 통해 종속성을 사용하는 개체를 변경하지 않고도 종속성을 변경할 수 있습니다.

## Spring에서 DI는 어떻게 작동합니까?

Spring에서 DI는 @Autowired 주석을 사용하여 수행됩니다. 이 주석은 필드, setter 메서드 및 생성자에서 사용할 수 있습니다. 필드에서 사용될 때 필드는 런타임에 종속성과 함께 주입됩니다. setter 메서드에서 사용하는 경우 메서드가 호출될 때 종속성이 메서드에 주입됩니다. 생성자에서 사용하는 경우 객체가 생성될 때 종속성이 객체에 주입됩니다.

@Autowired 어노테이션은 @Configuration 어노테이션이 있는 메소드에서도 사용할 수 있으며, 이 경우 메소드가 호출될 때 메소드에 종속성이 주입됩니다.

## Spring Boot에서 DI를 사용하는 방법

Spring Boot를 사용하면 애플리케이션에서 DI를 쉽게 사용할 수 있습니다. Spring Boot에서 DI를 사용하려면 종속성을 주입하려는 필드, setter 메서드 또는 생성자에 @Autowired 주석을 추가하기만 하면 됩니다.

예를 들어 종속성을 주입하려는 간단한 서비스가 있다고 가정합니다. @Autowired로 필드에 주석을 달아 이를 수행할 수 있습니다.

```java
@Service
public class MyService {
    @Autowired
    private MyDependency myDependency;
}
```

또는 setter 메서드에 주석을 달 수 있습니다.

```java
@Service
public class MyService {
    private MyDependency myDependency;
    
    @Autowired
    public void setMyDependency(MyDependency myDependency) {
        this.myDependency = myDependency;
    }
}
```

또는 생성자에 주석을 달 수 있습니다.

```java
@Service
public class MyService {
    private MyDependency myDependency;
    
    @Autowired
    public MyService(MyDependency myDependency) {
        this.myDependency = myDependency;
    }
}
```

## 결론

종속성 주입은 애플리케이션의 모듈성을 높이는 데 사용할 수 있는 강력한 기술입니다. Spring에서 DI는 @Autowired 주석을 사용하여 수행됩니다.

Spring Boot를 사용하면 애플리케이션에서 DI를 쉽게 사용할 수 있습니다. Spring Boot에서 DI를 사용하려면 종속성을 주입하려는 필드, setter 메서드 또는 생성자에 @Autowired 주석을 추가하기만 하면 됩니다.