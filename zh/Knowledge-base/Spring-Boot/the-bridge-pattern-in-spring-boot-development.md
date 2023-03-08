---
title: Spring Boot开发中的桥接模式
description: 
published: true
date: 2023-02-06T09:17:15.805Z
tags: 
editor: markdown
dateCreated: 2023-02-06T09:17:14.245Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [The Bridge Pattern in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-bridge-pattern-in-spring-boot-development)
{.links-list}


# Spring Boot 开发中的桥接模式

最有用的设计模式之一是桥接模式。此模式可用于将抽象与其实现解耦，以便两者可以独立变化。桥接模式通常与适配器模式结合使用。

在 Spring Boot 中，桥接模式用于将应用程序与底层数据库解耦。这是通过使用 Repository 和 @Transactional 注释完成的。

Repository 注释用于将类标记为存储库。存储库是为实体提供 CRUD 操作的类。 @Transactional 注释用于将方法标记为事务的一部分。


这是存储库的示例：

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

在上面的示例中，PersonRepository 类被标记为存储库。 save、findById 和 delete 方法被标记为事务的一部分。

桥接模式是一种有用的模式，可用于将抽象与其实现解耦。在 Spring Boot 中，Repository 和 @Transactional 注解用于将应用程序与底层数据库解耦。