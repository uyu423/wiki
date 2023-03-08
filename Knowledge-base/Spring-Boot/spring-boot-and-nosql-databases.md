---
title: Spring Boot 및 NoSQL 데이터베이스
description: 
published: true
date: 2023-02-07T02:55:51.526Z
tags: 
editor: markdown
dateCreated: 2023-02-07T02:55:49.925Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot and NoSQL Databases***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-nosql-databases)
{.links-list}


# 스프링 부트와 NoSQL 데이터베이스

기존의 관계형 데이터베이스에 비해 몇 가지 이점을 제공하는 NoSQL 데이터베이스를 웹 애플리케이션으로 사용하는 개발자가 늘고 있습니다. 널리 사용되는 Java 마이크로서비스 프레임워크인 Spring Boot를 사용하면 NoSQL 데이터베이스로 쉽게 작업할 수 있습니다. 이 기사에서는 가장 인기 있는 NoSQL 데이터베이스와 이를 Spring Boot와 함께 사용하는 방법을 살펴보겠습니다.

## 몽고디비

MongoDB는 Java 개발자에게 매우 인기 있는 문서 지향 NoSQL 데이터베이스입니다. 사용 가능한 전용 스타터 모듈이 있으므로 Spring Boot와 함께 사용하기 쉽습니다. Spring Boot에서 MongoDB를 사용하려면 pom.xml 파일에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

종속성을 추가했으면 application.properties 파일에서 spring.data.mongodb.uri 속성을 설정하여 MongoDB를 구성할 수 있습니다. 예를 들어:

```
spring.data.mongodb.uri=mongodb://localhost/mydatabase
```

그런 다음 MongoDB 리포지토리를 사용하여 Spring Boot 애플리케이션을 만들 수 있습니다. 예를 들어:

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

위의 예에서는 MongoRepository를 확장하는 CustomerRepository를 만들었습니다. 이렇게 하면 Customer 클래스에 대한 모든 표준 CRUD 작업에 액세스할 수 있습니다. 또한 Customer 클래스가 MongoDB 컬렉션에 매핑되어야 함을 Spring에 알리기 위해 @Document 주석을 만들었습니다.

## 아파치 카산드라

Apache Cassandra는 확장성과 성능으로 널리 알려진 분산 NoSQL 데이터베이스입니다. 또한 전용 스타터 모듈을 사용할 수 있으므로 Spring Boot와 함께 사용하기 쉽습니다. Spring Boot에서 Cassandra를 사용하려면 pom.xml 파일에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-cassandra</artifactId>
</dependency>
```

종속성을 추가했으면 application.properties 파일에서 spring.data.cassandra.keyspace-name 및 spring.data.cassandra.contact-points 속성을 설정하여 Cassandra를 구성할 수 있습니다. 예를 들어:

```
spring.data.cassandra.keyspace-name=mykeyspace
spring.data.cassandra.contact-points=localhost
```

그런 다음 Cassandra 리포지토리를 사용하여 Spring Boot 애플리케이션을 만들 수 있습니다. 예를 들어:

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

위의 예에서 CassandraRepository를 확장하는 CustomerRepository를 만들었습니다. 이렇게 하면 Customer 클래스에 대한 모든 표준 CRUD 작업에 액세스할 수 있습니다. 또한 Customer 클래스가 Cassandra 테이블에 매핑되어야 함을 Spring에 알리기 위해 @Table 주석을 만들었습니다.

## 아파치 HBase

Apache HBase는 확장성과 성능으로 널리 알려진 열 지향 NoSQL 데이터베이스입니다. 또한 전용 스타터 모듈을 사용할 수 있으므로 Spring Boot와 함께 사용하기 쉽습니다. Spring Boot와 함께 HBase를 사용하려면 pom.xml 파일에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-hbase</artifactId>
</dependency>
```

종속성을 추가한 후에는 application.properties 파일에서 spring.data.hbase.zookeeper.quorum 및 spring.data.hbase.zookeeper.property.clientPort 속성을 설정하여 HBase를 구성할 수 있습니다. 예를 들어:

```
spring.data.hbase.zookeeper.quorum=localhost
spring.data.hbase.zookeeper.property.clientPort=2181
```

그런 다음 HBase 리포지토리를 사용하여 Spring Boot 애플리케이션을 만들 수 있습니다. 예를 들어:

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

위의 예에서는 HbaseRepository를 확장하는 CustomerRepository를 만들었습니다. 이렇게 하면 Customer 클래스에 대한 모든 표준 CRUD 작업에 액세스할 수 있습니다. 또한 Customer 클래스가 HBase 테이블에 매핑되어야 함을 Spring에 알리기 위해 @Table 주석을 만들었습니다.

## 레디스

Redis는 Java 개발자에게 매우 인기 있는 키-값 저장소입니다. 사용 가능한 전용 스타터 모듈이 있으므로 Spring Boot와 함께 사용하기 쉽습니다. Redis를 Spring Boot와 함께 사용하려면 pom.xml 파일에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

종속성을 추가한 후에는 application.properties 파일에서 spring.redis.host 및 spring.redis.port 속성을 설정하여 Redis를 구성할 수 있습니다. 예를 들어:

```
spring.redis.host=localhost
spring.redis.port=6379
```

그런 다음 Redis 리포지토리를 사용하여 Spring Boot 애플리케이션을 생성할 수 있습니다. 예를 들어:

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

위의 예에서는 RedisRepository를 확장하는 CustomerRepository를 생성했습니다. 이렇게 하면 Customer 클래스에 대한 모든 표준 CRUD 작업에 액세스할 수 있습니다. 또한 Customer 클래스가 Redis 해시에 매핑되어야 함을 Spring에 알리기 위해 @RedisHash 주석을 만들었습니다.

## 결론

이 기사에서는 가장 인기 있는 NoSQL 데이터베이스와 이를 Spring Boot와 함께 사용하는 방법을 살펴보았습니다. NoSQL 데이터베이스는 기존 관계형 데이터베이스에 비해 몇 가지 이점을 제공하며 Spring Boot를 사용하면 쉽게 작업할 수 있습니다.