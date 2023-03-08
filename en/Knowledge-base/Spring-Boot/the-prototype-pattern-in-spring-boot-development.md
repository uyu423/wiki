---
title: The Prototype Pattern in Spring Boot Development
description: 
published: true
date: 2023-01-31T15:43:35.036Z
tags: 
editor: markdown
dateCreated: 2023-01-31T15:43:31.380Z
---

- [Spring Boot 개발의 프로토타입 패턴***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/the-prototype-pattern-in-spring-boot-development)
{.links-list}
- [Spring Boot 開発におけるプロトタイプ パターン***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/the-prototype-pattern-in-spring-boot-development)
{.links-list}
- [Spring Boot开发中的原型模式***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/the-prototype-pattern-in-spring-boot-development)
{.links-list}


# The Prototype Pattern in Spring Boot Development

The Prototype pattern is a creational design pattern that allows you to clone an object while avoiding the overhead of creating a new one from scratch. In Spring, the Prototype scope is used to create beans that are meant to be used only once. This can be useful when you need to create a large number of beans with the same configuration.

When you create a prototype bean, Spring will create a new instance of the bean for each request. This can be useful for beans that are expensive to create, such as objects that need to be queried from a database.

To use the Prototype scope, you can annotate your bean class with the @Scope("prototype") annotation. This will tell Spring to create a new instance of the bean for each request.

For example, let's say you have a bean that needs to query a database. You can annotate this bean with the @Scope("prototype") annotation to ensure that a new instance is created for each request. This way, each request will get its own database connection.

```java
@Scope("prototype")
@Component
public class MyBean {
   ...
}
```

If you need to inject a prototype bean into a singleton bean, you can use the @Autowired annotation. This will tell Spring to create a new instance of the prototype bean for each request.

```java
@Autowired
MyBean myBean;
```

You can also use the @Resource annotation to inject a prototype bean into a singleton bean. This will tell Spring to create a new instance of the prototype bean for each request.

```java
@Resource(name="myBean")
MyBean myBean;
```

When you are using the Prototype scope, it is important to keep in mind that each request will get its own instance of the bean. This means that any state that you store in the bean will not be shared between requests.

If you need to share state between prototype beans, you can use the ThreadLocal class. This class allows you to store data in a thread-safe manner.

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

In the example above, we are using a ThreadLocal to store the count. This will ensure that each request gets its own count.

It is also important to note that the Prototype scope is not inherited. This means that if you have a bean that is annotated with the @Scope("prototype") annotation, and you inject it into a child bean, the child bean will not be a prototype.

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

In the example above, the ChildBean will not be a prototype. This is because the @Scope("prototype") annotation is not inherited.

If you need to make a child bean a prototype, you can annotate it with the @Scope("prototype") annotation.

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

In the example above, the ChildBean will be a prototype. This is because the @Scope("prototype") annotation is applied to the ChildBean class.

The Prototype pattern is a powerful tool that can be used to improve the performance of your application. When used correctly, it can help you avoid the overhead of creating new objects from scratch.