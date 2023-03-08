---
title: The Decorator Pattern in Spring Boot Development
description: 
published: true
date: 2023-02-08T16:32:30.280Z
tags: 
editor: markdown
dateCreated: 2023-02-08T16:32:24.342Z
---

- [El patrón Decorator en el desarrollo de Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/the-decorator-pattern-in-spring-boot-development)
{.links-list}
- [Spring Boot开发中的装饰者模式***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/the-decorator-pattern-in-spring-boot-development)
{.links-list}
- [스프링 부트 개발의 데코레이터 패턴***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/the-decorator-pattern-in-spring-boot-development)
{.links-list}


# The Decorator Pattern in Spring Boot Development

The Decorator Pattern is a software design pattern that allows for the modification of existing objects without changing their core functionality. This is achieved by wrapping the original object with a decorator object that contains the desired functionality.

In Spring Boot, the Decorator Pattern can be used to dynamically add new functionality to existing beans without changing their code. This is done by wrapping the original bean with a decorator bean that contains the desired functionality.

For example, let's say we have a simple bean that contains a message:

```java
public class MessageBean {
  
  private String message;
  
  public MessageBean(String message) {
    this.message = message;
  }
  
  public String getMessage() {
    return message;
  }
}
```

We can use the Decorator Pattern to dynamically add a new functionality to this bean without changing its code. For example, we can create a decorator bean that adds a timestamp to the message:

```java
public class TimestampDecorator implements MessageBean {
  
  private MessageBean messageBean;
  
  public TimestampDecorator(MessageBean messageBean) {
    this.messageBean = messageBean;
  }
  
  @Override
  public String getMessage() {
    return messageBean.getMessage() + " - " + new Date();
  }
}
```

Now, when we inject the MessageBean into our code, we can specify that we want to use the TimestampDecorator:

```java
@Autowired
@Qualifier("timestampDecorator")
private MessageBean messageBean;
```

This will add the current timestamp to the message when we call the getMessage() method:

```java
messageBean.getMessage(); // "Hello World! - Thu Jan 01 00:00:00 EST 1970"
```

The Decorator Pattern is a useful way to dynamically add new functionality to existing beans without changing their code. This can be used to add timestamps, logging, security, or any other desired functionality.