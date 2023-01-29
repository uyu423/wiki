---
title: Setting up a Backend System with Spring Boot
description: 
published: true
date: 2023-01-29T21:26:55.230Z
tags: 
editor: markdown
dateCreated: 2023-01-29T21:26:55.230Z
---

- [Spring Boot로 백엔드 시스템 설정***Korean** version of this document is available*](/ko/Knowledge-base/Backend/setting-up-a-backend-system-with-spring-boot)
{.links-list}


# Setting up a Backend System with Spring Boot

In this post, we'll see how to set up a backend system using Spring Boot. We'll use MySQL as the database and Spring Data JPA for data access. The code for this post is available on GitHub.

## Prerequisites

To follow along with this post, you will need the following:

* Spring Boot (I'm using version 2.0.3.RELEASE)
* MySQL (I'm using version 5.7.21)
* Maven (I'm using version 3.5.3)

## Creating the Project

We'll start by creating a new Spring Boot project. We'll use the spring-boot-starter-data-jpa and mysql-connector-java dependencies. The complete pom.xml file is shown below.

    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    	<modelVersion>4.0.0</modelVersion>
    
    	<groupId>com.example</groupId>
    	<artifactId>spring-boot-mysql</artifactId>
    	<version>0.0.1-SNAPSHOT</version>
    	<packaging>jar</packaging>
    
    	<name>spring-boot-mysql</name>
    	<description>Demo project for Spring Boot</description>
    
    	<parent>
    		<groupId>org.springframework.boot</groupId>
    		<artifactId>spring-boot-starter-parent</artifactId>
    		<version>2.0.3.RELEASE</version>
    		<relativePath/> <!-- lookup parent from repository -->
    	</parent>
    
    	<properties>
    		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
    		<java.version>1.8</java.version>
    	</properties>
    
    	<dependencies>
    		<dependency>
    			<groupId>org.springframework.boot</groupId>
    			<artifactId>spring-boot-starter-data-jpa</artifactId>
    		</dependency>
    		<dependency>
    			<groupId>org.springframework.boot</groupId>
    			<artifactId>spring-boot-starter-test</artifactId>
    			<scope>test</scope>
    		</dependency>
    		<dependency>
    			<groupId>mysql</groupId>
    			<artifactId>mysql-connector-java</artifactId>
    			<scope>runtime</scope>
    		</dependency>
    	</dependencies>
    
    	<build>
    		<plugins>
    			<plugin>
    				<groupId>org.springframework.boot</groupId>
    				<artifactId>spring-boot-maven-plugin</artifactId>
    			</plugin>
    		</plugins>
    	</build>
    
    
    </project>

## Configuring MySQL

Next, we need to configure MySQL. We'll create a database called `test` and a user called `test` with the password `test`.

    create database test;
    grant all on test.* to 'test'@'localhost' identified by 'test';

## Configuring Spring Boot

Spring Boot will automatically configure a DataSource if it finds the right libraries on the classpath. In our case, we need to put the mysql-connector-java library on the classpath. Spring Boot will then automatically create a DataSource and configure it with the database settings in application.properties.

The only settings we need to configure are the database URL, username, and password. The complete application.properties file is shown below.

    spring.datasource.url=jdbc:mysql://localhost:3306/test
    spring.datasource.username=test
    spring.datasource.password=test

## Creating the Entity

We'll start by creating a simple entity. We'll call it `User`.

    @Entity
    public class User {
    
    	@Id
    	@GeneratedValue(strategy = GenerationType.AUTO)
    	private Long id;
    
    	private String name;
    	private String email;
    
    	// Getters and setters omitted
    
    }

## Creating the Repository

Next, we'll create a repository for our entity. We'll call it `UserRepository`.

    public interface UserRepository extends CrudRepository<User, Long> {
    
    }

That's all we need to do. Spring Data JPA will automatically create a concrete implementation of the repository at runtime.

## Creating the Service

We'll create a simple service that we can use to create, read, update, and delete users. We'll call it `UserService`.

    @Service
    public class UserService {
    
    	@Autowired
    	private UserRepository userRepository;
    
    	public User createUser(User user) {
    		return userRepository.save(user);
    	}
    
    	public User findUserById(Long id) {
    		return userRepository.findById(id).get();
    	}
    
    	public List<User> findAllUsers() {
    		return userRepository.findAll();
    	}
    
    	public User updateUser(User user) {
    		return userRepository.save(user);
    	}
    
    	public void deleteUser(User user) {
    		userRepository.delete(user);
    	}
    
    }

## Creating the REST Controller

We'll create a controller that exposes our service as a REST API. We'll call it `UserController`.

    @RestController
    @RequestMapping("/users")
    public class UserController {
    
    	@Autowired
    	private UserService userService;
    
    	@PostMapping
    	public User createUser(@RequestBody User user) {
    		return userService.createUser(user);
    	}
    
    	@GetMapping("/{id}")
    	public User findUserById(@PathVariable Long id) {
    		return userService.findUserById(id);
    	}
    
    	@GetMapping
    	public List<User> findAllUsers() {
    		return userService.findAllUsers();
    	}
    
    	@PutMapping
    	public User updateUser(@RequestBody User user) {
    		return userService.updateUser(user);
    	}
    
    	@DeleteMapping("/{id}")
    	public void deleteUser(@PathVariable Long id) {
    		userService.deleteUser(id);
    	}
    
    }

## Testing the API

We can test the API using curl. To create a user, we can use the following command.

    curl -X POST -H "Content-Type: application/json" -d '{"name":"John","email":"john@example.com"}' http://localhost:8080/users

To find a user by id, we can use the following command.

    curl http://localhost:8080/users/1

To find all users, we can use the following command.

    curl http://localhost:8080/users

To update a user, we can use the following command.

    curl -X PUT -H "Content-Type: application/json" -d '{"name":"John Smith","email":"john@example.com"}' http://localhost:8080/users/1

To delete a user, we can use the following command.

    curl -X DELETE http://localhost:8080/users/1

## Summary

In this post, we've seen how to set up a backend system using Spring Boot. We've used MySQL as the database and Spring Data JPA for data access. We've also created a simple REST API for our backend system.