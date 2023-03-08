---
title: Dependency Injection in Spring Boot
description: 
published: true
date: 2023-01-31T14:57:28.453Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:57:23.768Z
---

- [Spring Boot에서 의존성 주입***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/dependency-injection-in-spring-boot)
{.links-list}
- [Spring Boot での依存性注入***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/dependency-injection-in-spring-boot)
{.links-list}
- [Spring Boot 中的依赖注入***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/dependency-injection-in-spring-boot)
{.links-list}


# Dependency Injection in Spring Boot

## Introduction

Dependency Injection (DI) is a technique widely used in modern programming to increase the modularity of an application. By injecting dependencies into an object, we can avoid hard-coding these dependencies and make our code more flexible and easier to test and maintain.

In this article, we'll take a look at how DI works in the context of the Spring Framework, and how it can be used to make our Spring-based applications more modular and easier to test.

## What is Dependency Injection?

Dependency Injection is a technique for decoupling the dependencies of an object from the object itself.

In traditional programming, an object would hard-code its dependencies, meaning that if those dependencies changed, the object would need to be changed as well. This tight coupling makes code difficult to maintain and test.

With DI, the dependencies of an object are injected into the object at runtime, rather than being hard-coded. This allows the dependencies to be changed without changing the object that uses them.

## How Does DI Work in Spring?

In Spring, DI is accomplished through the use of the @Autowired annotation. This annotation can be used on fields, setter methods, and constructors. When used on a field, the field will be injected with the dependencies at runtime. When used on a setter method, the dependencies will be injected into the method when it is called. When used on a constructor, the dependencies will be injected into the object when it is created.

The @Autowired annotation can also be used on methods annotated with @Configuration, in which case the dependencies will be injected into the method when it is called.

## How to Use DI in Spring Boot

Spring Boot makes it easy to use DI in your applications. To use DI in Spring Boot, you just need to add the @Autowired annotation to the fields, setter methods, or constructors that you want to inject dependencies into.

For example, suppose we have a simple service that we want to inject a dependency into. We can do this by annotating the field with @Autowired:

```java
@Service
public class MyService {
    @Autowired
    private MyDependency myDependency;
}
```

Alternatively, we could annotate a setter method:

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

Or, we could annotate a constructor:

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

## Conclusion

Dependency Injection is a powerful technique that can be used to increase the modularity of an application. In Spring, DI is accomplished through the use of the @Autowired annotation.

Spring Boot makes it easy to use DI in your applications. To use DI in Spring Boot, you just need to add the @Autowired annotation to the fields, setter methods, or constructors that you want to inject dependencies into.