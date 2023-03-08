---
title: Spring Boot 和 NoSQL 数据库
description: 
published: true
date: 2023-02-07T02:55:51.519Z
tags: 
editor: markdown
dateCreated: 2023-02-07T02:55:49.921Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot and NoSQL Databases***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-nosql-databases)
{.links-list}


# Spring Boot 和 NoSQL 数据库

开发人员越来越多地将 NoSQL 数据库转向他们的 Web 应用程序，因为与传统关系数据库相比，它们具有多项优势。 Spring Boot 是流行的 Java 微服务框架，可以轻松使用 NoSQL 数据库。在本文中，我们将探讨一些最流行的 NoSQL 数据库以及如何将它们与 Spring Boot 结合使用。

## MongoDB

MongoDB 是一个非常受 Java 开发人员欢迎的面向文档的 NoSQL 数据库。它很容易与 Spring Boot 一起使用，因为有一个专用的启动模块可用。要将 MongoDB 与 Spring Boot 一起使用，您需要将以下依赖项添加到您的 pom.xml 文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

添加依赖项后，您可以通过在 application.properties 文件中设置 spring.data.mongodb.uri 属性来配置 MongoDB。例如：

```
spring.data.mongodb.uri=mongodb://localhost/mydatabase
```

然后，您可以使用 MongoDB 存储库创建 Spring Boot 应用程序。例如：

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}

@Repository
public interface CustomerRepository extends MongoRepository<Customer, String> {

    public List<Customer> findByLastName(String lastName);

}

@Document
public class Customer {

    @Id
    private String id;
    private String firstName;
    private String lastName;

    // Getters and setters omitted
}
```

在上面的示例中，我们创建了一个扩展 MongoRepository 的 CustomerRepository。这使我们能够访问 Customer 类的所有标准 CRUD 操作。我们还创建了一个 @Document 注释来告诉 Spring 我们的 Customer 类应该映射到 MongoDB 集合。

## 阿帕奇卡桑德拉

Apache Cassandra 是一种分布式 NoSQL 数据库，因其可扩展性和性能而广受欢迎。它也很容易与 Spring Boot 一起使用，因为有一个专用的启动模块可用。要将 Cassandra 与 Spring Boot 一起使用，您需要将以下依赖项添加到您的 pom.xml 文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-cassandra</artifactId>
</dependency>
```

添加依赖项后，您可以通过在 application.properties 文件中设置 spring.data.cassandra.keyspace-name 和 spring.data.cassandra.contact-points 属性来配置 Cassandra。例如：

```
spring.data.cassandra.keyspace-name=mykeyspace
spring.data.cassandra.contact-points=localhost
```

然后，您可以使用 Cassandra 存储库创建 Spring Boot 应用程序。例如：

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}

@Repository
public interface CustomerRepository extends CassandraRepository<Customer, String> {

    public List<Customer> findByLastName(String lastName);

}

@Table
public class Customer {

    @PrimaryKey
    private String id;
    private String firstName;
    private String lastName;

    // Getters and setters omitted
}
```

在上面的示例中，我们创建了一个扩展 CassandraRepository 的 CustomerRepository。这使我们能够访问 Customer 类的所有标准 CRUD 操作。我们还创建了一个 @Table 注释来告诉 Spring 我们的 Customer 类应该映射到 Cassandra 表。

## 阿帕奇 HBase

Apache HBase 是一种面向列的 NoSQL 数据库，因其可扩展性和性能而广受欢迎。它也很容易与 Spring Boot 一起使用，因为有一个专用的启动模块可用。要将 HBase 与 Spring Boot 一起使用，您需要将以下依赖项添加到您的 pom.xml 文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-hbase</artifactId>
</dependency>
```

添加依赖项后，您可以通过在 application.properties 文件中设置 spring.data.hbase.zookeeper.quorum 和 spring.data.hbase.zookeeper.property.clientPort 属性来配置 HBase。例如：

```
spring.data.hbase.zookeeper.quorum=localhost
spring.data.hbase.zookeeper.property.clientPort=2181
```

然后，您可以使用 HBase 存储库创建 Spring Boot 应用程序。例如：

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}

@Repository
public interface CustomerRepository extends HbaseRepository<Customer, String> {

    public List<Customer> findByLastName(String lastName);

}

@Table(name = "customers")
public class Customer {

    @Id
    private String id;
    private String firstName;
    private String lastName;

    // Getters and setters omitted
}
```

在上面的示例中，我们创建了一个扩展 HbaseRepository 的 CustomerRepository。这使我们能够访问 Customer 类的所有标准 CRUD 操作。我们还创建了一个 @Table 注释来告诉 Spring 我们的 Customer 类应该映射到一个 HBase 表。

## 雷迪斯

Redis 是一种非常受 Java 开发人员欢迎的键值存储。它很容易与 Spring Boot 一起使用，因为有一个专用的启动模块可用。要将 Redis 与 Spring Boot 一起使用，您需要将以下依赖项添加到您的 pom.xml 文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

添加依赖项后，您可以通过在 application.properties 文件中设置 spring.redis.host 和 spring.redis.port 属性来配置 Redis。例如：

```
spring.redis.host=localhost
spring.redis.port=6379
```

然后，您可以使用 Redis 存储库创建 Spring Boot 应用程序。例如：

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}

@Repository
public interface CustomerRepository extends RedisRepository<Customer, String> {

    public List<Customer> findByLastName(String lastName);

}

@RedisHash("customers")
public class Customer {

    @Id
    private String id;
    private String firstName;
    private String lastName;

    // Getters and setters omitted
}
```

在上面的示例中，我们创建了一个扩展 RedisRepository 的 CustomerRepository。这使我们能够访问 Customer 类的所有标准 CRUD 操作。我们还创建了一个 @RedisHash 注释来告诉 Spring 我们的 Customer 类应该映射到 Redis 哈希。

## 结论

在本文中，我们了解了一些最流行的 NoSQL 数据库以及如何将它们与 Spring Boot 结合使用。与传统关系数据库相比，NoSQL 数据库具有多项优势，而 Spring Boot 使其易于使用。