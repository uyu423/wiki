---
title: Building a REST API with Spring MVC
description: 
published: true
date: 2023-02-17T18:01:18.176Z
tags: 
editor: markdown
dateCreated: 2023-01-30T01:02:49.009Z
---

- [Spring MVC로 REST API 구축***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/building-a-rest-api-with-spring-mvc)
{.links-list}


# Building a REST API with Spring MVC

## Introduction

In this post, we'll take a look at how to build a simple REST API with Spring MVC. We'll be using the latest versions of both the Spring Framework and Hibernate ORM.

We'll first need to set up our project. For this example, we'll be using the Maven build system. We'll also need to add the following dependencies to our pom.xml file:

```xml
<!-- Spring MVC -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.0.5.RELEASE</version>
</dependency>

<!-- Hibernate ORM -->
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-core</artifactId>
    <version>5.2.12.Final</version>
</dependency>
```

With our dependencies in place, we can now move on to configuring our application.

## Configuration

We'll start by configuring Hibernate. We'll create a hibernate.cfg.xml file in the src/main/resources directory with the following contents:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
        <!-- Database connection settings -->
        <property name="connection.driver_class">org.h2.Driver</property>
        <property name="connection.url">jdbc:h2:mem:testdb</property>
        <property name="connection.username">sa</property>
        <property name="connection.password"></property>
 
        <!-- JDBC connection pool (use the built-in) -->
        <property name="connection.pool_size">1</property>
 
        <!-- SQL dialect -->
        <property name="dialect">org.hibernate.dialect.H2Dialect</property>
 
        <!-- Disable the second-level cache  -->
        <property name="cache.provider_class">org.hibernate.cache.internal.NoCacheProvider</property>
 
        <!-- Echo all executed SQL to stdout -->
        <property name="show_sql">true</property>
 
        <!-- Drop and re-create the database schema on startup -->
        <property name="hbm2ddl.auto">create</property>
    </session-factory>
</hibernate-configuration>
```

In the hibernate.cfg.xml file, we've configured Hibernate to use an in-memory H2 database. We've also set the show_sql property to true so that Hibernate will print all SQL queries to the console.

Next, we'll configure Spring MVC. We'll create a file called web.xml in the src/main/webapp/WEB-INF directory with the following contents:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
         version="3.0">
 
    <!-- Configure Spring MVC DispatcherServlet -->
    <servlet>
        <servlet-name>dispatcher</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/spring-mvc-config.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
 
    <servlet-mapping>
        <servlet-name>dispatcher</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
 
</web-app>
```

In the web.xml file, we've configured the Spring MVC DispatcherServlet. This servlet is responsible for handling all requests to our application. We've also specified a contextConfigLocation init-param. This param tells the DispatcherServlet where to find our application's Spring configuration file. In this case, we've stored our configuration in a file called spring-mvc-config.xml, which we'll create next.

Lastly, we'll create the spring-mvc-config.xml file in the src/main/webapp/WEB-INF directory with the following contents:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
 
    <!-- Enable annotation-based Spring MVC configuration -->
    <context:annotation-config/>
 
    <!-- Scan for Spring components -->
    <context:component-scan base-package="com.example.restapi"/>
 
    <!-- Configure the Hibernate bean -->
    <bean id="hibernate5AnnotatedSessionFactory"
          class="org.springframework.orm.hibernate5.LocalSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <property name="packagesToScan">
            <list>
                <value>com.example.restapi.model</value>
            </list>
        </property>
        <property name="hibernateProperties">
            <props>
                <prop key="hibernate.dialect">org.hibernate.dialect.H2Dialect</prop>
                <prop key="hibernate.show_sql">${hibernate.show_sql}</prop>
                <prop key="hibernate.hbm2ddl.auto">${hibernate.hbm2ddl.auto}</prop>
            </props>
        </property>
    </bean>
 
    <!-- Configure the data source bean -->
    <bean id="dataSource"
          class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="${database.driverClassName}"/>
        <property name="url" value="${database.url}"/>
        <property name="username" value="${database.username}"/>
        <property name="password" value="${database.password}"/>
    </bean>
 
</beans>
```

In the spring-mvc-config.xml file, we've configured our application to use annotation-based configuration and component scanning. We've also configured our Hibernate and data source beans.

With our configuration complete, we can now move on to writing our code.

## Writing the Code

We'll start by creating our model classes. We'll need a class to represent our users and a class to represent our posts. We'll create these classes in the src/main/java/com/example/restapi/model directory:

```java
package com.example.restapi.model;
 
import javax.persistence.*;
 
@Entity
@Table(name = "users")
public class User {
 
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
 
    @Column(nullable = false)
    private String username;
 
    @Column(nullable = false)
    private String password;
 
    @Column(nullable = false)
    private String email;
 
    // Getters and setters
 
}
```

```java
package com.example.restapi.model;
 
import javax.persistence.*;
import java.util.Date;
 
@Entity
@Table(name = "posts")
public class Post {
 
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
 
    @Column(nullable = false)
    private String title;
 
    @Column(nullable = false, columnDefinition = "TEXT")
    private String body;
 
    @Column(nullable = false)
    @Temporal(TemporalType.TIMESTAMP)
    private Date createdAt;
 
    @Column(nullable = false)
    @Temporal(TemporalType.TIMESTAMP)
    private Date updatedAt;
 
    // Getters and setters
 
}
```

Our User and Post classes are simple JPA entities. We've annotated them with the @Entity annotation to indicate that they should be mapped to database tables. We've also annotated them with the @Table annotation to specify the name of the table that each class should be mapped to.

Next, we'll create our repository interfaces. We'll create these interfaces in the src/main/java/com/example/restapi/repository directory:

```java
package com.example.restapi.repository;
 
import com.example.restapi.model.User;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;
 
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
 
}
```

```java
package com.example.restapi.repository;
 
import com.example.restapi.model.Post;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;
 
@Repository
public interface PostRepository extends JpaRepository<Post, Long> {
 
}
```

Our UserRepository and PostRepository interfaces are simple Spring Data JPA repositories. We've annotated them with the @Repository annotation to indicate that they are Spring beans. We've extended the JpaRepository interface to provide all of the basic CRUD operations for our entities.

Now that we have our models and repositories in place, we can move on to writing our service layer. We'll create our service interfaces and implementations in the src/main/java/com/example/restapi/service directory:

```java
package com.example.restapi.service;
 
import com.example.restapi.model.User;
 
public interface UserService {
 
    User createUser(User user);
 
    User getUser(Long id);
 
    User updateUser(User user);
 
    void deleteUser(User user);
 
}
```

```java
package com.example.restapi.service;
 
import com.example.restapi.model.Post;
 
public interface PostService {
 
    Post createPost(Post post);
 
    Post getPost(Long id);
 
    Post updatePost(Post post);
 
    void deletePost(Post post);
 
}
```

Our UserService and PostService interfaces are simple CRUD interfaces for our User and Post entities. We'll implement these interfaces in our UserServiceImpl and PostServiceImpl classes:

```java
package com.example.restapi.service.impl;
 
import com.example.restapi.model.User;
import com.example.restapi.repository.UserRepository;
import com.example.restapi.service.UserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
 
@Service
public class UserServiceImpl implements UserService {
 
    @Autowired
    private UserRepository userRepository;
 
    @Override
    public User createUser(User user) {
        return userRepository.save(user);
    }
 
    @Override
    public User getUser(Long id) {
        return userRepository.getOne(id);
    }
 
    @Override
    public User updateUser(User user) {
        return userRepository.save(user);
    }
 
    @Override
    public void deleteUser(User user) {
        userRepository.delete(user);
    }
 
}
```

```java
package com.example.restapi.service.impl;
 
import com.example.restapi.model.Post;
import com.example.restapi.repository.PostRepository;
import com.example.restapi.service.PostService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
 
@Service
public class PostServiceImpl implements PostService {
 
    @Autowired
    private PostRepository postRepository;
 
    @Override
    public Post createPost(Post post) {
        return postRepository.save(post);
    }
 
    @Override
    public Post getPost(Long id) {
        return postRepository.getOne(id);
    }
 
    @Override
    public Post updatePost(Post post) {
        return postRepository.save(post);
    }
 
    @Override
    public void deletePost(Post post) {
        postRepository.delete(post);
    }
 
}
```

Our UserServiceImpl and PostServiceImpl classes are simple implementations of our service interfaces. We've annotated them with the @Service annotation to indicate that they are Spring beans. We've also injected our UserRepository and PostRepository beans into our service classes.

With our service layer in place, we can now move on to writing our controller. We'll create our controller in the src/main/java/com/example/restapi/controller directory:

```java
package com.example.restapi.controller;
 
import com.example.restapi.model.Post;
import com.example.restapi.model.User;
import