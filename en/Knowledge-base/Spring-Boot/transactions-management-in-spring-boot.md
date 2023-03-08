---
title: Transactions Management in Spring Boot
description: 
published: true
date: 2023-02-17T18:01:19.566Z
tags: 
editor: markdown
dateCreated: 2023-01-30T01:11:45.871Z
---

- [Spring Boot의 트랜잭션 관리***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/transactions-management-in-spring-boot)
{.links-list}


## Transactional Management in Spring Boot

Spring Boot provides several options for transactional management. This post explains each option and provides a code example for each option.

### 1. JTA with Atomikos

JTA with Atomikos is the most recommended option for transactional management in Spring Boot. Atomikos is a transaction manager that supports JTA. JTA is a standard Java API for managing transactions.

To use JTA with Atomikos, you need to add the following dependencies to your pom.xml:

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-jta-atomikos</artifactId>
</dependency>
```

And you need to configure Atomikos in your application.properties file:

```
spring.jta.atomikos.properties.logbase=java.io.tmpdir
spring.jta.atomikos.properties.service=com.atomikos.icatch.standalone.UserTransactionServiceFactory
```

You can find more information about configuring Atomikos in the [Atomikos documentation](https://docs.atomikos.com/Main/ConfiguringTheTransactionService).

### 2. LocalTransactionManager

The LocalTransactionManager is a simple transaction manager that can be used for transactional management in Spring Boot. To use the LocalTransactionManager, you need to add the following dependency to your pom.xml:

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
```

And you need to configure the LocalTransactionManager in your application.properties file:

```
spring.jta.transaction-manager-id=localTransactionManager
```

### 3. JTA with Bitronix

JTA with Bitronix is another option for transactional management in Spring Boot. Bitronix is a transaction manager that supports JTA. To use JTA with Bitronix, you need to add the following dependencies to your pom.xml:

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-jta-bitronix</artifactId>
</dependency>
```

And you need to configure Bitronix in your application.properties file:

```
spring.jta.bitronix.tm-unique-name=bitronixTransactionManager
```

You can find more information about configuring Bitronix in the [Bitronix documentation](https://docs.bitronix.net/latest/user-guide/).

### 4. DataSourceTransactionManager

The DataSourceTransactionManager is another option for transactional management in Spring Boot. The DataSourceTransactionManager is a simple transaction manager that can be used for transactional management with JDBC data sources. 

To use the DataSourceTransactionManager, you need to add the following dependency to your pom.xml:

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
```

And you need to configure the DataSourceTransactionManager in your application.properties file:

```
spring.jta.transaction-manager-id=dataSourceTransactionManager
```

### 5. JMS with ActiveMQ

JMS with ActiveMQ is another option for transactional management in Spring Boot. ActiveMQ is a message broker that supports JMS. JMS is a standard Java API for managing messages.

To use JMS with ActiveMQ, you need to add the following dependencies to your pom.xml:

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-activemq</artifactId>
</dependency>
```

And you need to configure ActiveMQ in your application.properties file:

```
spring.activemq.broker-url=tcp://localhost:61616
```

You can find more information about configuring ActiveMQ in the [ActiveMQ documentation](http://activemq.apache.org/).

### 6. NoTransactionManager

The NoTransactionManager is a special transaction manager that can be used when there is no need for transactional management. The NoTransactionManager is used by default in Spring Boot.

To use the NoTransactionManager, you do not need to add any dependencies to your pom.xml. And you do not need to configure the NoTransactionManager in your application.properties file.

### 7. WebSphereUowTransactionManager

The WebSphereUowTransactionManager is a transaction manager that can be used in WebSphere application servers. To use the WebSphereUowTransactionManager, you need to add the following dependency to your pom.xml:

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-websphere-uow</artifactId>
</dependency>
```

And you need to configure the WebSphereUowTransactionManager in your application.properties file:

```
spring.jta.transaction-manager-id=webSphereUowTransactionManager
```

You can find more information about configuring the WebSphereUowTransactionManager in the [WebSphere documentation](https://www.ibm.com/support/knowledgecenter/was_beta/com.ibm.websphere.base.doc/ae/tcon_uowm.html).

### 8. JOTM

JOTM is a transaction manager that can be used in Spring Boot. To use JOTM, you need to add the following dependency to your pom.xml:

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-jotm</artifactId>
</dependency>
```

And you need to configure JOTM in your application.properties file:

```
spring.jta.transaction-manager-id=jotm
```

You can find more information about configuring JOTM in the [JOTM documentation](http://jotm.objectweb.org/current/docs/userGuide.html).

### 9. Narayana

Narayana is a transaction manager that can be used in Spring Boot. To use Narayana, you need to add the following dependency to your pom.xml:

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-narayana-jta</artifactId>
</dependency>
```

And you need to configure Narayana in your application.properties file:

```
spring.jta.transaction-manager-id=narayana
```

You can find more information about configuring Narayana in the [Narayana documentation](https://narayana.io/).

### 10. Geronimo

Geronimo is a transaction manager that can be used in Spring Boot. To use Geronimo, you need to add the following dependency to your pom.xml:

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-geronimo-jta</artifactId>
</dependency>
```

And you need to configure Geronimo in your application.properties file:

```
spring.jta.transaction-manager-id=geronimo
```

You can find more information about configuring Geronimo in the [Geronimo documentation](https://geronimo.apache.org/).