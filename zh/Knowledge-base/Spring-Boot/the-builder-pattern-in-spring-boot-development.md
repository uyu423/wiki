---
title: Spring Boot开发中的建造者模式
description: 
published: true
date: 2023-02-17T18:13:59.260Z
tags: 
editor: markdown
dateCreated: 2023-01-30T21:04:35.301Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [The Builder Pattern in Spring Boot Development***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-builder-pattern-in-spring-boot-development)
{.links-list}


# Spring Boot开发中的建造者模式

使用 Spring 框架时，通常需要创建需要多个构造函数参数的复杂对象的实例。这会导致代码难以阅读和维护。构建器模式是一种软件设计模式，可用于通过创建可用于逐步构建复杂对象的构建器对象来解决此问题。

在本文中，我们将了解如何在 Spring Boot 开发中使用构建器模式。我们还将了解使用此模式的一些优点和缺点。

## 什么是建造者模式？

构建器模式是一种软件设计模式，它提供了一种创建需要多个构造函数参数的复杂对象的方法。当需要创建一个有很多可选参数的对象时，经常使用它。

构建器模式是一种创建型设计模式，用于解决创建需要多个构造函数参数的复杂对象的问题。构建器模式将对象的构造与其表示分开。这允许从相同的构造过程中创建不同的表示。

建造者模式类似于工厂模式，但有一些重要的区别。工厂模式关注对象的创建，而建造者模式关注对象的构造。当需要创建相同类型的对象时，使用工厂模式。当需要创建不同类型的对象时，使用构建器模式。

建造者模式有以下优点：

- 它将对象的构造与其表示分开。这允许从相同的构造过程中创建不同的表示。
- 它允许以逐步的方式创建复杂的对象。
- 它允许在不影响客户端代码的情况下更改构造过程。

建造者模式有以下缺点：

- 它会导致大量样板代码。
- 如果构建器模式使用不当，可能很难理解生成的代码。

## 什么时候使用建造者模式？

当需要创建需要多个构造函数参数的复杂对象时，应使用构建器模式。当需要创建一个有很多可选参数的对象时，经常使用它。

## 如何在 Spring Boot 中使用构建器模式？

在 Spring Boot 中，构建器模式可用于创建需要多个构造函数参数的复杂对象。 @ConfigurationProperties 注释可用于将属性绑定到构建器对象。

以下是如何在 Spring Boot 中使用构建器模式的示例：

```java
@ConfigurationProperties(prefix="acme")
public class AcmeProperties {

    private String name;

    private String email;

    private String phone;

    // Getters and setters

    public static class Builder {
        private String name;
        private String email;
        private String phone;

        public Builder withName(String name) {
            this.name = name;
            return this;
        }

        public Builder withEmail(String email) {
            this.email = email;
            return this;
        }

        public Builder withPhone(String phone) {
            this.phone = phone;
            return this;
        }

        public AcmeProperties build() {
            return new AcmeProperties(this);
        }
    }

    private AcmeProperties(Builder builder) {
        this.name = builder.name;
        this.email = builder.email;
        this.phone = builder.phone;
    }

    // Getters and setters

}
```

@ConfigurationProperties 注释用于将属性绑定到构建器对象。 withName()、withEmail() 和 withPhone() 方法用于设置姓名、电子邮件和电话属性的值。 build() 方法用于创建 AcmeProperties 类的实例。

以下是如何使用 AcmeProperties 类的示例：

```java
@Autowired
private AcmeProperties acmeProperties;

@Test
public void test() {
    AcmeProperties.Builder builder = new AcmeProperties.Builder();
    builder.withName("John Smith")
           .withEmail("john.smith@example.com")
           .withPhone("555-555-1212");
    AcmeProperties acmeProperties = builder.build();
    assertThat(acmeProperties.getName()).isEqualTo("John Smith");
    assertThat(acmeProperties.getEmail()).isEqualTo("john.smith@example.com");
    assertThat(acmeProperties.getPhone()).isEqualTo("555-555-1212");
}
```

在上面的示例中，AcmeProperties 类用于创建 AcmeProperties 类的实例。 withName()、withEmail() 和 withPhone() 方法用于设置姓名、电子邮件和电话属性的值。 build() 方法用于创建 AcmeProperties 类的实例。

构建器模式可用于创建需要多个构造函数参数的复杂对象。 @ConfigurationProperties 注释可用于将属性绑定到构建器对象。 withName()、withEmail() 和 withPhone() 方法用于设置姓名、电子邮件和电话属性的值。 build() 方法用于创建 AcmeProperties 类的实例。