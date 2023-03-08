---
title: Spring Boot and NoSQL Databases
description: 
published: true
date: 2023-02-07T02:55:55.623Z
tags: 
editor: markdown
dateCreated: 2023-02-07T02:55:49.933Z
---

- [Bases de datos Spring Boot y NoSQL***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-and-nosql-databases)
{.links-list}
- [Spring Boot 和 NoSQL 数据库***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-and-nosql-databases)
{.links-list}
- [Spring Boot 및 NoSQL 데이터베이스***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-and-nosql-databases)
{.links-list}


# Spring Boot and NoSQL Databases

Developers are increasingly turning to NoSQL databases for their web applications, as they offer several advantages over traditional relational databases. Spring Boot, the popular Java microservices framework, makes it easy to work with NoSQL databases. In this article, we'll explore some of the most popular NoSQL databases and how to use them with Spring Boot.

## MongoDB

MongoDB is a document-oriented NoSQL database that is very popular with Java developers. It is easy to use with Spring Boot, as there is a dedicated starter module available. To use MongoDB with Spring Boot, you need to add the following dependency to your pom.xml file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

Once you have added the dependency, you can configure MongoDB by setting the spring.data.mongodb.uri property in your application.properties file. For example:

```
spring.data.mongodb.uri=mongodb://localhost/mydatabase
```

You can then create a Spring Boot application with a MongoDB repository. For example:

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

In the example above, we have created a CustomerRepository that extends MongoRepository. This gives us access to all the standard CRUD operations for our Customer class. We have also created a @Document annotation to tell Spring that our Customer class should be mapped to a MongoDB collection.

## Apache Cassandra

Apache Cassandra is a distributed NoSQL database that is popular for its scalability and performance. It is also easy to use with Spring Boot, as there is a dedicated starter module available. To use Cassandra with Spring Boot, you need to add the following dependency to your pom.xml file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-cassandra</artifactId>
</dependency>
```

Once you have added the dependency, you can configure Cassandra by setting the spring.data.cassandra.keyspace-name and spring.data.cassandra.contact-points properties in your application.properties file. For example:

```
spring.data.cassandra.keyspace-name=mykeyspace
spring.data.cassandra.contact-points=localhost
```

You can then create a Spring Boot application with a Cassandra repository. For example:

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

In the example above, we have created a CustomerRepository that extends CassandraRepository. This gives us access to all the standard CRUD operations for our Customer class. We have also created a @Table annotation to tell Spring that our Customer class should be mapped to a Cassandra table.

## Apache HBase

Apache HBase is a column-oriented NoSQL database that is popular for its scalability and performance. It is also easy to use with Spring Boot, as there is a dedicated starter module available. To use HBase with Spring Boot, you need to add the following dependency to your pom.xml file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-hbase</artifactId>
</dependency>
```

Once you have added the dependency, you can configure HBase by setting the spring.data.hbase.zookeeper.quorum and spring.data.hbase.zookeeper.property.clientPort properties in your application.properties file. For example:

```
spring.data.hbase.zookeeper.quorum=localhost
spring.data.hbase.zookeeper.property.clientPort=2181
```

You can then create a Spring Boot application with an HBase repository. For example:

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

In the example above, we have created a CustomerRepository that extends HbaseRepository. This gives us access to all the standard CRUD operations for our Customer class. We have also created a @Table annotation to tell Spring that our Customer class should be mapped to an HBase table.

## Redis

Redis is a key-value store that is very popular with Java developers. It is easy to use with Spring Boot, as there is a dedicated starter module available. To use Redis with Spring Boot, you need to add the following dependency to your pom.xml file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

Once you have added the dependency, you can configure Redis by setting the spring.redis.host and spring.redis.port properties in your application.properties file. For example:

```
spring.redis.host=localhost
spring.redis.port=6379
```

You can then create a Spring Boot application with a Redis repository. For example:

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

In the example above, we have created a CustomerRepository that extends RedisRepository. This gives us access to all the standard CRUD operations for our Customer class. We have also created a @RedisHash annotation to tell Spring that our Customer class should be mapped to a Redis hash.

## Conclusion

In this article, we have looked at some of the most popular NoSQL databases and how to use them with Spring Boot. NoSQL databases offer several advantages over traditional relational databases, and Spring Boot makes it easy to work with them.