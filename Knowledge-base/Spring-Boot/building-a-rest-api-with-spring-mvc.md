---
title: Spring MVC로 REST API 구축
description: 
published: true
date: 2023-02-17T18:01:16.826Z
tags: 
editor: markdown
dateCreated: 2023-01-30T01:02:49.008Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Building a REST API with Spring MVC***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/building-a-rest-api-with-spring-mvc)
{.links-list}


# Spring MVC로 REST API 구축하기

## 소개

이번 포스팅에서는 Spring MVC로 간단한 REST API를 빌드하는 방법에 대해 알아보겠습니다. Spring Framework와 Hibernate ORM의 최신 버전을 사용할 것입니다.

먼저 프로젝트를 설정해야 합니다. 이 예제에서는 Maven 빌드 시스템을 사용합니다. 또한 pom.xml 파일에 다음 종속성을 추가해야 합니다.

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

종속 항목이 준비되었으므로 이제 애플리케이션 구성으로 이동할 수 있습니다.

## 구성

Hibernate를 구성하는 것으로 시작하겠습니다. 다음 내용으로 src/main/resources 디렉토리에 hibernate.cfg.xml 파일을 생성합니다.

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

hibernate.cfg.xml 파일에서 메모리 내 H2 데이터베이스를 사용하도록 Hibernate를 구성했습니다. 우리는 또한 Hibernate가 모든 SQL 쿼리를 콘솔에 출력하도록 show_sql 속성을 true로 설정했습니다.

다음으로 Spring MVC를 구성합니다. 다음 내용으로 src/main/webapp/WEB-INF 디렉토리에 web.xml이라는 파일을 생성합니다.

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

web.xml 파일에서 Spring MVC DispatcherServlet을 구성했습니다. 이 서블릿은 애플리케이션에 대한 모든 요청을 처리합니다. 또한 contextConfigLocation 초기화 매개변수도 지정했습니다. 이 매개변수는 애플리케이션의 Spring 구성 파일을 찾을 위치를 DispatcherServlet에 알려줍니다. 이 경우, 우리는 다음에 생성할 spring-mvc-config.xml이라는 파일에 구성을 저장했습니다.

마지막으로 다음 내용으로 src/main/webapp/WEB-INF 디렉토리에 spring-mvc-config.xml 파일을 생성합니다.

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

spring-mvc-config.xml 파일에서 주석 기반 구성 및 구성 요소 검색을 사용하도록 애플리케이션을 구성했습니다. 또한 Hibernate 및 데이터 소스 빈을 구성했습니다.

구성이 완료되면 이제 코드 작성으로 넘어갈 수 있습니다.

## 코드 작성

모델 클래스를 만드는 것으로 시작하겠습니다. 사용자를 나타내는 클래스와 게시물을 나타내는 클래스가 필요합니다. src/main/java/com/example/restapi/model 디렉토리에 다음 클래스를 생성합니다.

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

User 및 Post 클래스는 간단한 JPA 엔터티입니다. 데이터베이스 테이블에 매핑되어야 함을 나타내기 위해 @Entity 주석으로 주석을 달았습니다. 또한 각 클래스가 매핑되어야 하는 테이블의 이름을 지정하기 위해 @Table 주석으로 주석을 달았습니다.

다음으로 리포지토리 인터페이스를 만듭니다. src/main/java/com/example/restapi/repository 디렉토리에 다음 인터페이스를 생성합니다.

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

UserRepository 및 PostRepository 인터페이스는 간단한 Spring Data JPA 저장소입니다. Spring bean임을 나타내기 위해 @Repository 주석으로 주석을 달았습니다. 엔티티에 대한 모든 기본 CRUD 작업을 제공하도록 JpaRepository 인터페이스를 확장했습니다.

이제 모델과 리포지토리가 준비되었으므로 서비스 계층 작성으로 넘어갈 수 있습니다. src/main/java/com/example/restapi/service 디렉터리에 서비스 인터페이스와 구현을 생성합니다.

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

UserService 및 PostService 인터페이스는 User 및 Post 엔터티를 위한 간단한 CRUD 인터페이스입니다. UserServiceImpl 및 PostServiceImpl 클래스에서 이러한 인터페이스를 구현합니다.

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

UserServiceImpl 및 PostServiceImpl 클래스는 서비스 인터페이스의 간단한 구현입니다. Spring bean임을 나타내기 위해 @Service 주석으로 주석을 달았습니다. 또한 UserRepository 및 PostRepository 빈을 서비스 클래스에 삽입했습니다.

서비스 계층이 준비되었으므로 이제 컨트롤러 작성으로 넘어갈 수 있습니다. src/main/java/com/example/restapi/controller 디렉토리에 컨트롤러를 생성합니다.

```자바
패키지 com.example.restapi.controller;
 
import com.example.restapi.model.Post;
import com.example.restapi.model.User;
수입