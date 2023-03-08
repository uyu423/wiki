---
title: Spring Boot 개발의 프로토타입 패턴
description: 
published: true
date: 2023-01-31T15:43:32.965Z
tags: 
editor: markdown
dateCreated: 2023-01-31T15:43:31.381Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [The Prototype Pattern in Spring Boot Development***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-prototype-pattern-in-spring-boot-development)
{.links-list}


# Spring Boot 개발의 프로토타입 패턴

프로토타입 패턴은 개체를 처음부터 새로 만드는 오버헤드를 피하면서 개체를 복제할 수 있는 생성 디자인 패턴입니다. Spring에서 Prototype 범위는 한 번만 사용되는 빈을 생성하는 데 사용됩니다. 이는 동일한 구성으로 많은 수의 bean을 생성해야 할 때 유용할 수 있습니다.

프로토타입 bean을 생성할 때 Spring은 각 요청에 대해 bean의 새 인스턴스를 생성합니다. 이는 데이터베이스에서 쿼리해야 하는 개체와 같이 생성 비용이 많이 드는 빈에 유용할 수 있습니다.

Prototype 범위를 사용하려면 빈 클래스에 @Scope("prototype") 주석을 추가할 수 있습니다. 이것은 각 요청에 대해 Bean의 새 인스턴스를 생성하도록 Spring에 지시합니다.

예를 들어 데이터베이스를 쿼리해야 하는 빈이 있다고 가정해 보겠습니다. @Scope("prototype") 주석으로 이 빈에 주석을 달아 각 요청에 대해 새 인스턴스가 생성되도록 할 수 있습니다. 이렇게 하면 각 요청이 자체 데이터베이스 연결을 갖게 됩니다.

```java
@Scope("prototype")
@Component
public class MyBean {
   ...
}
```

프로토타입 빈을 싱글톤 빈에 주입해야 하는 경우 @Autowired 주석을 사용할 수 있습니다. 이는 각 요청에 대해 프로토타입 빈의 새 인스턴스를 생성하도록 Spring에 지시합니다.

```java
@Autowired
MyBean myBean;
```

@Resource 주석을 사용하여 프로토타입 빈을 싱글톤 빈에 주입할 수도 있습니다. 이는 각 요청에 대해 프로토타입 빈의 새 인스턴스를 생성하도록 Spring에 지시합니다.

```java
@Resource(name="myBean")
MyBean myBean;
```

Prototype 범위를 사용할 때 각 요청이 고유한 bean 인스턴스를 얻는다는 점을 염두에 두는 것이 중요합니다. 이는 Bean에 저장하는 모든 상태가 요청 간에 공유되지 않음을 의미합니다.

프로토타입 빈 간에 상태를 공유해야 하는 경우 ThreadLocal 클래스를 사용할 수 있습니다. 이 클래스를 사용하면 스레드로부터 안전한 방식으로 데이터를 저장할 수 있습니다.

```java
@Scope("prototype")
@Component
public class MyBean {
   private ThreadLocal<Integer> count = new ThreadLocal<Integer>();

   public void increment() {
      count.set(count.get() + 1);
   }

   public int getCount() {
      return count.get();
   }
}
```

위의 예에서는 개수를 저장하기 위해 ThreadLocal을 사용하고 있습니다. 이렇게 하면 각 요청이 자체 개수를 얻습니다.

Prototype 범위가 상속되지 않는다는 점에 유의하는 것도 중요합니다. 즉, @Scope("prototype") 주석으로 주석이 달린 빈이 있고 이를 자식 빈에 주입하면 자식 빈은 프로토타입이 되지 않습니다.

```java
@Component
@Scope("prototype")
public class ParentBean {
   ...
}

@Component
public class ChildBean {
   @Autowired
   private ParentBean parentBean;

   ...
}
```

위의 예에서 ChildBean은 프로토타입이 아닙니다. 이는 @Scope("prototype") 주석이 상속되지 않기 때문입니다.

자식 빈을 프로토타입으로 만들어야 하는 경우 @Scope("prototype") 주석으로 주석을 달 수 있습니다.

```java
@Component
@Scope("prototype")
public class ParentBean {
   ...
}

@Component
@Scope("prototype")
public class ChildBean {
   @Autowired
   private ParentBean parentBean;

   ...
}
```

위의 예에서 ChildBean은 프로토타입이 됩니다. 이는 ChildBean 클래스에 @Scope("prototype") 주석이 적용되기 때문입니다.

프로토타입 패턴은 애플리케이션의 성능을 향상시키는 데 사용할 수 있는 강력한 도구입니다. 올바르게 사용하면 처음부터 새 개체를 만드는 오버헤드를 피할 수 있습니다.