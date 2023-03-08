---
title: Spring Boot에서 종속성 주입 시작하기
description: 
published: true
date: 2023-02-17T18:01:12.741Z
tags: 
editor: markdown
dateCreated: 2023-01-30T00:51:02.793Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Getting Started with Dependency Injection in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/getting-started-with-dependency-injection-in-spring-boot)
{.links-list}


# Spring Boot에서 의존성 주입 시작하기

이 기사에서는 종속성 주입이 무엇이며 Spring Boot 애플리케이션에서 어떻게 사용할 수 있는지 살펴보겠습니다. 또한 종속성 주입을 사용하여 얻을 수 있는 몇 가지 이점에 대해서도 살펴보겠습니다.

## 의존성 주입이란?

종속성 주입은 소프트웨어 시스템의 종속성을 관리하는 기술입니다. 종속성은 다른 개체가 의존하는 개체입니다. 종속성을 주입한다는 것은 해당 개체 외부에서 개체에 종속성을 제공하는 것을 의미합니다.

종속성 주입에는 생성자 주입과 세터 주입의 두 가지 주요 유형이 있습니다. 생성자 주입을 사용하면 개체가 생성될 때 개체에 종속성이 제공됩니다. 세터 주입은 종속성을 설정하기 위해 개체에서 세터 메서드를 호출하여 수행됩니다.

## 의존성 주입을 사용하는 이유

종속성 주입을 사용하면 몇 가지 이점이 있습니다.

### 느슨한 결합

종속성 주입은 개체 간의 느슨한 결합을 허용합니다. 종속성에 느슨하게 연결된 개체는 동일한 종속성을 제공하는 다른 개체로 쉽게 대체할 수 있습니다. 이렇게 하면 해당 개체를 사용하는 코드를 변경하지 않고도 개체의 동작을 쉽게 변경할 수 있습니다.

### 테스트 용이성

종속성 주입을 사용하면 개체에 대한 단위 테스트를 쉽게 작성할 수 있습니다. 개체에 종속성이 주입되면 해당 종속성을 실제 종속성의 동작을 시뮬레이션하는 모의 개체로 대체할 수 있습니다. 이를 통해 개체의 실제 종속성에 의존하지 않는 단위 테스트를 작성할 수 있습니다.

### 유연성

종속성 주입을 사용하면 개체를 사용하는 방식에 더 큰 유연성을 부여할 수 있습니다. 개체에 다른 종속성을 제공하여 개체를 다른 방식으로 사용할 수 있습니다. 이는 개체를 다른 컨텍스트에서 사용해야 할 때 유용할 수 있습니다.

## Spring Boot에서 의존성 주입을 사용하는 방법

Spring Boot는 생성자 주입과 setter 주입을 모두 지원합니다.

### 생성자 주입

생성자 주입은 Spring Boot에서 선호되는 종속성 주입 방법입니다. 생성자 주입을 사용하려면 생성자에 @Autowired 주석을 추가하면 됩니다. 그런 다음 Spring Boot는 해당 생성자에 종속성을 주입합니다.

```java
@Autowired
public MyService(Dependency1 dependency1, Dependency2 dependency2) {
    this.dependency1 = dependency1;
    this.dependency2 = dependency2;
}
```

### 세터 주입

setter 주입은 @Autowired 주석으로 setter 메서드에 주석을 달아 사용할 수 있습니다. Spring Boot는 해당 setter 메서드를 호출하고 개체에 종속성을 주입합니다.

```java
@Autowired
public void setDependency1(Dependency1 dependency1) {
    this.dependency1 = dependency1;
}
```

## 결론

종속성 주입은 소프트웨어 시스템의 종속성을 관리하는 데 유용한 기술입니다. 느슨한 결합을 달성하고 테스트 가능성을 개선하며 유연성을 높이는 데 사용할 수 있습니다. Spring Boot는 생성자 주입과 setter 주입을 모두 지원합니다.