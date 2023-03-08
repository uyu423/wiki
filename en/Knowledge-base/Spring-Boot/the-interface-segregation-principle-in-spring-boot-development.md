---
title: The Interface Segregation Principle in Spring Boot Development
description: 
published: true
date: 2023-02-04T02:17:25.853Z
tags: 
editor: markdown
dateCreated: 2023-02-04T02:17:20.765Z
---

- [El principio de segregación de la interfaz en el desarrollo de Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/the-interface-segregation-principle-in-spring-boot-development)
{.links-list}
- [Spring Boot开发中的接口隔离原则***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/the-interface-segregation-principle-in-spring-boot-development)
{.links-list}
- [Spring Boot 개발의 인터페이스 분리 원칙***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/the-interface-segregation-principle-in-spring-boot-development)
{.links-list}


# The Interface Segregation Principle in Spring Boot Development

The Interface Segregation Principle (ISP) is a software design principle that states that no client should be forced to depend on methods it does not use.

In other words, it is best to keep interfaces small and focused so that they can be implemented by classes that need them, without depending on unused methods.

The principle was first defined by Robert C. Martin in his book "Agile Software Development, Principles, Patterns, and Practices".

## Applying the Interface Segregation Principle

When designing software, it is important to keep the ISP in mind so that interfaces are not too large or too general.

For example, consider an interface for a user service that includes methods for creating, updating, and deleting users.

```java
public interface UserService {
    
    public void createUser(User user);
    
    public void updateUser(User user);
    
    public void deleteUser(User user);
    
}
```

A class that implements this interface would need to provide implementations for all three methods, even if it only needs to support user creation.

A better design would be to have separate interfaces for each type of operation.

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

This design is more in line with the ISP because each interface is focused on a specific task.

A class that only needs to support user creation can implement the ```UserService``` interface without depending on the other interfaces.

## Spring Boot and the Interface Segregation Principle

Spring Boot is a popular framework for developing Java applications.

It is based on the principle of convention over configuration, which means that it favors convention over explicit configuration.

This principle can be applied to the design of interfaces.

For example, consider a Spring Boot application that has a ```UserService``` interface.

```java
@Service
public interface UserService {
    
    public void createUser(User user);
    
}
```

The ```@Service``` annotation is used to indicate that this interface is a Spring service.

Spring will automatically create a bean for this interface and inject it into any component that needs it.

This design is in line with the ISP because the interface is focused on a specific task (user creation) and it is not necessary for components to depend on unused methods.