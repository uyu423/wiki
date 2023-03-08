---
title: 005: Working with Spring Boot and Spring Data JPA
description: 
published: true
date: 2023-02-03T07:43:47.994Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:43:43.292Z
---

- [005: Trabajar con Spring Boot y Spring Data JPA***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/005-working-with-spring-boot-and-spring-data-jpa)
{.links-list}
- [005：使用 Spring Boot 和 Spring Data JPA***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/005-working-with-spring-boot-and-spring-data-jpa)
{.links-list}
- [005: Spring Boot 및 Spring Data JPA 작업***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/005-working-with-spring-boot-and-spring-data-jpa)
{.links-list}


# Working with Spring Boot and Spring Data JPA

In this post, we'll take a look at how to work with Spring Boot and Spring Data JPA.

We'll start by looking at what JPA is and why we would want to use it. Then, we'll take a look at how to configure Spring Boot to work with JPA. Finally, we'll write a few simple example programs to show how to use JPA in a Spring Boot application.

## What is JPA?

JPA is the Java Persistence API. It's a specification for how to map Java objects to a relational database.

There are many implementations of JPA, the most popular being Hibernate. When you use JPA, you can write your code against the JPA API and let the JPA implementation (like Hibernate) handle the details of mapping your objects to the database.

## Why use JPA?

There are a few reasons you might want to use JPA in your applications:

- **JPA is a standard**. This means that there are many JPA implementations to choose from, and you can switch implementations if you need to.

- **JPA is flexible**. You can use JPA with different types of databases, and you can map your Java objects to the database in different ways.

- **JPA is easy to use**. The JPA API is designed to be easy to use, so you can get started with JPA quickly.

## Configuring Spring Boot for JPA

Spring Boot makes it easy to configure Spring for use with JPA. All you need to do is add the spring-boot-starter-data-jpa dependency to your project.

This dependency will pull in all of the necessary JPA dependencies, and it will also configure Spring Boot to use a JPA implementation (Hibernate, by default).

## Using JPA in Spring Boot

Now that we have Spring Boot configured to use JPA, let's write a few example programs to show how to use JPA in a Spring Boot application.

### Example 1: Creating a JPA Entity

To use JPA in your application, you need to create a JPA entity. A JPA entity is a Java class that is mapped to a database table.

Let's create a simple JPA entity:

```java
@Entity
public class Person {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    // ... getters and setters
}
```

This class is mapped to the `person` table in the database. The `@Entity` annotation indicates that this is a JPA entity. The `@Id` annotation indicates that the `id` field is the primary key for the entity. The `@GeneratedValue` annotation tells JPA to generate a unique id for each entity.

### Example 2: Creating a JPA Repository

Now that we have our JPA entity, we need a way to access it. We can do this by creating a JPA repository.

A JPA repository is a Spring Data repository that is used to access JPA entities. To create a JPA repository, we need to create an interface that extends the `JpaRepository` interface:

```java
public interface PersonRepository extends JpaRepository<Person, Long> {

}
```

This interface is used to access the `Person` entity. The `JpaRepository` interface provides many methods for working with JPA entities, so we don't need to write any code to implement this interface.

### Example 3: Using a JPA Repository

Now that we have our JPA entity and repository, let's write a program that uses the repository to create, read, update, and delete entities.

First, we'll inject the `PersonRepository` into our program:

```java
@Autowired
private PersonRepository personRepository;
```

Next, we'll use the repository to create a `Person` entity:

```java
Person person = new Person();
person.setName("John Doe");

personRepository.save(person);
```

This will insert a new row into the `person` table. The `save` method will generate a unique id for the entity and set it on the entity.

We can use the `findById` method to retrieve an entity by its id:

```java
Person person = personRepository.findById(1L);
```

We can use the `findAll` method to retrieve all entities:

```java
List<Person> people = personRepository.findAll();
```

We can use the `deleteById` method to delete an entity:

```java
personRepository.deleteById(1L);
```

And we can use the `delete` method to delete an entity:

```java
personRepository.delete(person);
```

These are just a few of the methods that are available on the `JpaRepository` interface. For a complete list of methods, see the [JpaRepository documentation](https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/JpaRepository.html).

## Conclusion

In this post, we've looked at how to work with Spring Boot and Spring Data JPA. We've seen how to configure Spring Boot to use JPA, and we've written a few simple example programs to show how to use JPA in a Spring Boot application.