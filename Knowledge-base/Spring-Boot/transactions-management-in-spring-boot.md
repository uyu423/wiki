---
title: Spring Boot의 트랜잭션 관리
description: 
published: true
date: 2023-02-17T18:01:20.950Z
tags: 
editor: markdown
dateCreated: 2023-01-30T01:11:45.872Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Transactions Management in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/transactions-management-in-spring-boot)
{.links-list}


## Spring Boot의 트랜잭션 관리

Spring Boot는 트랜잭션 관리를 위한 몇 가지 옵션을 제공합니다. 이 게시물은 각 옵션을 설명하고 각 옵션에 대한 코드 예제를 제공합니다.

### 1. 아토미코스와 함께하는 JTA

Atomikos를 사용한 JTA는 Spring Boot에서 트랜잭션 관리를 위해 가장 권장되는 옵션입니다. Atomikos는 JTA를 지원하는 트랜잭션 관리자입니다. JTA는 트랜잭션 관리를 위한 표준 Java API입니다.

Atomikos에서 JTA를 사용하려면 pom.xml에 다음 종속성을 추가해야 합니다.

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-jta-atomikos</artifactId>
</dependency>
```

그리고 application.properties 파일에서 Atomikos를 구성해야 합니다.

```
spring.jta.atomikos.properties.logbase=java.io.tmpdir
spring.jta.atomikos.properties.service=com.atomikos.icatch.standalone.UserTransactionServiceFactory
```

[Atomikos 설명서](https://docs.atomikos.com/Main/ConfiguringTheTransactionService)에서 Atomikos 구성에 대한 자세한 정보를 찾을 수 있습니다.

### 2. LocalTransactionManager

LocalTransactionManager는 Spring Boot에서 트랜잭션 관리에 사용할 수 있는 간단한 트랜잭션 관리자입니다. LocalTransactionManager를 사용하려면 pom.xml에 다음 종속성을 추가해야 합니다.

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
```

그리고 application.properties 파일에서 LocalTransactionManager를 구성해야 합니다.

```
spring.jta.transaction-manager-id=localTransactionManager
```

### 3. Bitronix와 JTA

Bitronix를 사용한 JTA는 Spring Boot의 트랜잭션 관리를 위한 또 다른 옵션입니다. Bitronix는 JTA를 지원하는 트랜잭션 관리자입니다. Bitronix에서 JTA를 사용하려면 pom.xml에 다음 종속성을 추가해야 합니다.

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-jta-bitronix</artifactId>
</dependency>
```

그리고 application.properties 파일에서 Bitronix를 구성해야 합니다.

```
spring.jta.bitronix.tm-unique-name=bitronixTransactionManager
```

Bitronix 구성에 대한 자세한 내용은 [Bitronix 설명서](https://docs.bitronix.net/latest/user-guide/)에서 확인할 수 있습니다.

### 4. DataSourceTransactionManager

DataSourceTransactionManager는 Spring Boot의 트랜잭션 관리를 위한 또 다른 옵션입니다. DataSourceTransactionManager는 JDBC 데이터 소스를 사용한 트랜잭션 관리에 사용할 수 있는 간단한 트랜잭션 관리자입니다.

DataSourceTransactionManager를 사용하려면 pom.xml에 다음 종속성을 추가해야 합니다.

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
```

그리고 application.properties 파일에서 DataSourceTransactionManager를 구성해야 합니다.

```
spring.jta.transaction-manager-id=dataSourceTransactionManager
```

### 5. ActiveMQ를 사용하는 JMS

ActiveMQ를 사용하는 JMS는 Spring Boot의 트랜잭션 관리를 위한 또 다른 옵션입니다. ActiveMQ는 JMS를 지원하는 메시지 브로커입니다. JMS는 메시지 관리를 위한 표준 Java API입니다.

JMS를 ActiveMQ와 함께 사용하려면 pom.xml에 다음 종속성을 추가해야 합니다.

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-activemq</artifactId>
</dependency>
```

그리고 application.properties 파일에서 ActiveMQ를 구성해야 합니다.

```
spring.activemq.broker-url=tcp://localhost:61616
```

[ActiveMQ 설명서](http://activemq.apache.org/)에서 ActiveMQ 구성에 대한 자세한 정보를 찾을 수 있습니다.

### 6. NoTransactionManager

NoTransactionManager는 트랜잭션 관리가 필요하지 않을 때 사용할 수 있는 특수 트랜잭션 관리자입니다. NoTransactionManager는 Spring Boot에서 기본적으로 사용됩니다.

NoTransactionManager를 사용하기 위해 pom.xml에 종속성을 추가할 필요가 없습니다. 또한 application.properties 파일에서 NoTransactionManager를 구성할 필요가 없습니다.

### 7. WebSphereUowTransactionManager

WebSphereUowTransactionManager는 WebSphere 애플리케이션 서버에서 사용할 수 있는 트랜잭션 관리자입니다. WebSphereUowTransactionManager를 사용하려면 pom.xml에 다음 종속성을 추가해야 합니다.

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-websphere-uow</artifactId>
</dependency>
```

그리고 application.properties 파일에서 WebSphereUowTransactionManager를 구성해야 합니다.

```
spring.jta.transaction-manager-id=webSphereUowTransactionManager
```

[WebSphere 문서](https://www.ibm.com/support/knowledgecenter/was_beta/com.ibm.websphere.base.doc/ae/tcon_uowm.html)에서 WebSphereUowTransactionManager 구성에 대한 자세한 정보를 찾을 수 있습니다.

### 8. JOTM

JOTM은 Spring Boot에서 사용할 수 있는 트랜잭션 관리자입니다. JOTM을 사용하려면 pom.xml에 다음 종속성을 추가해야 합니다.

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-jotm</artifactId>
</dependency>
```

그리고 application.properties 파일에서 JOTM을 구성해야 합니다.

```
spring.jta.transaction-manager-id=jotm
```

[JOTM 문서](http://jotm.objectweb.org/current/docs/userGuide.html)에서 JOTM 구성에 대한 자세한 정보를 찾을 수 있습니다.

### 9. 나라야나

Narayana는 Spring Boot에서 사용할 수 있는 트랜잭션 관리자입니다. Narayana를 사용하려면 pom.xml에 다음 종속성을 추가해야 합니다.

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-narayana-jta</artifactId>
</dependency>
```

그리고 application.properties 파일에서 Narayana를 구성해야 합니다.

```
spring.jta.transaction-manager-id=narayana
```

[Narayana 설명서](https://narayana.io/)에서 Narayana 구성에 대한 자세한 정보를 찾을 수 있습니다.

### 10. 제로니모

Geronimo는 Spring Boot에서 사용할 수 있는 트랜잭션 관리자입니다. Geronimo를 사용하려면 pom.xml에 다음 종속성을 추가해야 합니다.

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-geronimo-jta</artifactId>
</dependency>
```

그리고 application.properties 파일에서 Geronimo를 구성해야 합니다.

```
spring.jta.transaction-manager-id=geronimo
```

Geronimo 구성에 대한 자세한 내용은 [Geronimo 문서](https://geronimo.apache.org/)에서 확인할 수 있습니다.