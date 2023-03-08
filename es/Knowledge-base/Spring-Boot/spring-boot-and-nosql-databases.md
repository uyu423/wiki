---
title: Bases de datos Spring Boot y NoSQL
description: 
published: true
date: 2023-02-07T02:55:51.579Z
tags: 
editor: markdown
dateCreated: 2023-02-07T02:55:49.929Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot and NoSQL Databases***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-nosql-databases)
{.links-list}


# Bases de datos Spring Boot y NoSQL

Los desarrolladores recurren cada vez más a las bases de datos NoSQL para sus aplicaciones web, ya que ofrecen varias ventajas sobre las bases de datos relacionales tradicionales. Spring Boot, el popular marco de microservicios de Java, facilita el trabajo con bases de datos NoSQL. En este artículo, exploraremos algunas de las bases de datos NoSQL más populares y cómo usarlas con Spring Boot.

## MongoDB

MongoDB es una base de datos NoSQL orientada a documentos que es muy popular entre los desarrolladores de Java. Es fácil de usar con Spring Boot, ya que hay un módulo de inicio dedicado disponible. Para usar MongoDB con Spring Boot, debe agregar la siguiente dependencia a su archivo pom.xml:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

Una vez que haya agregado la dependencia, puede configurar MongoDB configurando la propiedad spring.data.mongodb.uri en su archivo application.properties. Por ejemplo:

```
spring.data.mongodb.uri=mongodb://localhost/mydatabase
```

Luego puede crear una aplicación Spring Boot con un repositorio MongoDB. Por ejemplo:

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

En el ejemplo anterior, hemos creado un CustomerRepository que amplía MongoRepository. Esto nos da acceso a todas las operaciones CRUD estándar para nuestra clase Cliente. También hemos creado una anotación @Document para decirle a Spring que nuestra clase de Cliente debe asignarse a una colección de MongoDB.

## Apache Casandra

Apache Cassandra es una base de datos NoSQL distribuida que es popular por su escalabilidad y rendimiento. También es fácil de usar con Spring Boot, ya que hay un módulo de inicio dedicado disponible. Para usar Cassandra con Spring Boot, debe agregar la siguiente dependencia a su archivo pom.xml:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-cassandra</artifactId>
</dependency>
```

Una vez que haya agregado la dependencia, puede configurar Cassandra configurando las propiedades spring.data.cassandra.keyspace-name y spring.data.cassandra.contact-points en su archivo application.properties. Por ejemplo:

```
spring.data.cassandra.keyspace-name=mykeyspace
spring.data.cassandra.contact-points=localhost
```

Luego puede crear una aplicación Spring Boot con un repositorio de Cassandra. Por ejemplo:

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

En el ejemplo anterior, hemos creado un CustomerRepository que amplía CassandraRepository. Esto nos da acceso a todas las operaciones CRUD estándar para nuestra clase Cliente. También hemos creado una anotación @Table para indicarle a Spring que nuestra clase Customer debe asignarse a una tabla Cassandra.

## Base de Apache

Apache HBase es una base de datos NoSQL orientada a columnas que es popular por su escalabilidad y rendimiento. También es fácil de usar con Spring Boot, ya que hay un módulo de inicio dedicado disponible. Para usar HBase con Spring Boot, debe agregar la siguiente dependencia a su archivo pom.xml:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-hbase</artifactId>
</dependency>
```

Una vez que haya agregado la dependencia, puede configurar HBase configurando las propiedades spring.data.hbase.zookeeper.quorum y spring.data.hbase.zookeeper.property.clientPort en su archivo application.properties. Por ejemplo:

```
spring.data.hbase.zookeeper.quorum=localhost
spring.data.hbase.zookeeper.property.clientPort=2181
```

Luego puede crear una aplicación Spring Boot con un repositorio HBase. Por ejemplo:

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

En el ejemplo anterior, hemos creado un CustomerRepository que amplía HbaseRepository. Esto nos da acceso a todas las operaciones CRUD estándar para nuestra clase Cliente. También hemos creado una anotación @Table para indicarle a Spring que nuestra clase Customer debe asignarse a una tabla HBase.

## redis

Redis es un almacén de clave-valor que es muy popular entre los desarrolladores de Java. Es fácil de usar con Spring Boot, ya que hay un módulo de inicio dedicado disponible. Para usar Redis con Spring Boot, debe agregar la siguiente dependencia a su archivo pom.xml:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

Una vez que haya agregado la dependencia, puede configurar Redis configurando las propiedades spring.redis.host y spring.redis.port en su archivo application.properties. Por ejemplo:

```
spring.redis.host=localhost
spring.redis.port=6379
```

Luego puede crear una aplicación Spring Boot con un repositorio de Redis. Por ejemplo:

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

En el ejemplo anterior, hemos creado un CustomerRepository que amplía RedisRepository. Esto nos da acceso a todas las operaciones CRUD estándar para nuestra clase Cliente. También creamos una anotación @RedisHash para decirle a Spring que nuestra clase de Cliente debe asignarse a un hash de Redis.

## Conclusión

En este artículo, hemos analizado algunas de las bases de datos NoSQL más populares y cómo usarlas con Spring Boot. Las bases de datos NoSQL ofrecen varias ventajas sobre las bases de datos relacionales tradicionales, y Spring Boot facilita el trabajo con ellas.