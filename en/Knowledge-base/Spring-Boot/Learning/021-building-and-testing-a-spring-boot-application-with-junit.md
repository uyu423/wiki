---
title: 021: Building and testing a Spring Boot application with Junit
description: 
published: true
date: 2023-02-03T13:34:22.048Z
tags: 
editor: markdown
dateCreated: 2023-02-03T13:34:17.072Z
---

- [021: Creación y prueba de una aplicación Spring Boot con Junit***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/021-building-and-testing-a-spring-boot-application-with-junit)
{.links-list}
- [021：使用 Junit 构建和测试 Spring Boot 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/021-building-and-testing-a-spring-boot-application-with-junit)
{.links-list}
- [021: Junit으로 Spring Boot 애플리케이션 빌드 및 테스트***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/021-building-and-testing-a-spring-boot-application-with-junit)
{.links-list}


#021: Building and testing a Spring Boot application with Junit

Junit is a popular testing framework for Java applications. Spring Boot is a Java-based framework used for creating microservices and web applications. In this post, we will show you how to build and test a Spring Boot application using Junit.

We will be using the following tools in this tutorial:

- Java 8
- Maven 3.3.9
- Eclipse Neon.3
- Junit 4.12

##Creating a Spring Boot application

We will start by creating a Spring Boot application. For this tutorial, we will be using the Spring Initializr website to generate our project.

Go to the Spring Initializr website (https://start.spring.io/) and enter the following information:

- Group: com.example
- Artifact: junit-tutorial
- Name: junit-tutorial
- Description: Demo project for Junit tutorial
- Package Name: com.example.junit.tutorial
- Packaging: Jar
- Java Version: 1.8
- Select the following dependencies: Web, JPA, H2, Lombok

Click on Generate Project to download the project.

Extract the zip file and import it into Eclipse as a Maven project.

##Writing a test case

Now that we have our project set up, we can start writing our test case. We will be testing the following scenario:

- Given a user with the username "johndoe" and the password "password"
- When the user tries to login
- Then the user should be able to login successfully

Create a new Java class in the com.example.junit.tutorial.service package and name it LoginServiceTest.java. Add the following code to the class:

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class LoginServiceTest {

    @Autowired
    private LoginService loginService;

    @Test
    public void testLogin() {
        // given
        String username = "johndoe";
        String password = "password";

        // when
        boolean result = loginService.login(username, password);

        // then
        assertTrue(result);
    }
}
```

In the code above, we are using the @RunWith and @SpringBootTest annotations to run our test case. We are also injecting the LoginService into our test case so that we can test the login() method.

The login() method takes a username and password and returns a boolean value indicating whether the login was successful or not. In our test case, we are passing in the username and password "johndoe" and "password". We then assert that the result is true, meaning that the login was successful.

##Running the test case

To run the test case, right-click on the LoginServiceTest.java class and select Run As > JUnit Test.

You should see the following output in the console:

```
.   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.0.3.RELEASE)

2018-07-26 12:21:06.469  INFO 6484 --- [           main] c.e.j.t.s.LoginServiceTest              : Starting LoginServiceTest on PC-LAPTOP with PID 6484 (started by John Doe in C:\junit-tutorial)
2018-07-26 12:21:06.470  INFO 6484 --- [           main] c.e.j.t.s.LoginServiceTest              : No active profile set, falling back to default profiles: default
2018-07-26 12:21:06.526  INFO 6484 --- [           main] s.c.a.AnnotationConfigApplicationContext : Refreshing org.springframework.context.annotation.AnnotationConfigApplicationContext@4a3a4df7: startup date [Thu Jul 26 12:21:06 EDT 2018]; root of context hierarchy
2018-07-26 12:21:07.067  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Registering beans for JMX exposure on startup
2018-07-26 12:21:07.068  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Bean with name 'dataSource' has been autodetected for JMX exposure
2018-07-26 12:21:07.069  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Located MBean 'dataSource': registering with JMX server as MBean [com.zaxxer.hikari:name=dataSource,type=HikariDataSource]
2018-07-26 12:21:07.076  INFO 6484 --- [           main] o.s.b.a.h2.H2ConsoleAutoConfiguration    : H2 console available at '/h2-console'. Database available at 'jdbc:h2:mem:testdb'
2018-07-26 12:21:07.094  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Located MBean 'h2:name=MemoryManagerService': registering with JMX server as MBean [org.h2.mvstore.db.H2Database:name=MemoryManagerService]
2018-07-26 12:21:07.095  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Located MBean 'h2:name=DatabaseStatusMBean': registering with JMX server as MBean [org.h2.engine.DatabaseStatusMBean]
2018-07-26 12:21:07.097  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Located MBean 'h2:name=DeadlockDetector': registering with JMX server as MBean [org.h2.engine.DeadlockDetector]
2018-07-26 12:21:07.098  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Located MBean 'h2:name=ThreadPool': registering with JMX server as MBean [org.h2.engine.ThreadPool]
2018-07-26 12:21:07.102  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Located MBean 'h2:name=SessionTracker': registering with JMX server as MBean [org.h2.engine.SessionTracker]
2018-07-26 12:21:07.104  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Located MBean 'h2:name=WebServer': registering with JMX server as MBean [org.h2.tools.Server]
2018-07-26 12:21:07.105  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Located MBean 'h2:name=ConnectionPool': registering with JMX server as MBean [org.h2.engine.ConnectionPool]
2018-07-26 12:21:07.106  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Located MBean 'h2:name=StatementTracker': registering with JMX server as MBean [org.h2.engine.StatementTracker]
2018-07-26 12:21:07.107  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Located MBean 'h2:name=SystemProperties': registering with JMX server as MBean [org.h2.engine.SystemProperties]
2018-07-26 12:21:07.108  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Located MBean 'h2:name=Versions': registering with JMX server as MBean [org.h2.engine.Versions]
2018-07-26 12:21:07.109  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Located MBean 'h2:name=ClusterSettings': registering with JMX server as MBean [org.h2.cluster.settings.ClusterSettings]
2018-07-26 12:21:07.110  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Located MBean 'h2:name=ServerInfo': registering with JMX server as MBean [org.h2.engine.ServerInfo]
2018-07-26 12:21:07.115  INFO 6484 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2018-07-26 12:21:07.118  INFO 6484 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2018-07-26 12:21:07.118  INFO 6484 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet Engine: Apache Tomcat/8.5.27
2018-07-26 12:21:07.119  INFO 6484 --- [ost-startStop-1] o.a.catalina.core.AprLifecycleListener   : The APR based Apache Tomcat Native library which allows optimal performance in production environments was not found on the java.library.path: [C:\Program Files\Java\jdk1.8.0_171\bin;C:\WINDOWS\Sun\Java\bin;C:\WINDOWS\system32;C:\WINDOWS;C:/Program Files/Java/jdk1.8.0_171/jre/bin/server;C:/Program Files/Java/jdk1.8.0_171/jre/bin;C:/Program Files/Java/jdk1.8.0_171/jre/lib/amd64;C:\ProgramData\Oracle\Java\javapath;C:\WINDOWS\system32;C:\WINDOWS;C:\WINDOWS\System32\Wbem;C:\WINDOWS\System32\WindowsPowerShell\v1.0\;C:\Program Files\Git\cmd;C:\Program Files\nodejs\;C:\Program Files (x86)\Brackets\command;C:\Users\John Doe\AppData\Local\Microsoft\WindowsApps;;.]
2018-07-26 12:21:07.154  INFO 6484 --- [ost-startStop-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2018-07-26 12:21:07.154  INFO 6484 --- [ost-startStop-1] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 350 ms
2018-07-26 12:21:07.295  INFO 6484 --- [ost-startStop-1] o.s.b.w.servlet.ServletRegistrationBean  : Servlet dispatcherServlet mapped to [/]
2018-07-26 12:21:07.296  INFO 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'characterEncodingFilter' to: [/*]
2018-07-26 12:21:07.296  INFO 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'hiddenHttpMethodFilter' to: [/*]
2018-07-26 12:21:07.296  INFO 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'httpPutFormContentFilter' to: [/*]
2018-07-26 12:21:07.296  INFO 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'requestContextFilter' to: [/*]
2018-07-26 12:21:07.363  INFO 6484 --- [           main] j.LocalContainerEntityManagerFactoryBean : Building JPA container EntityManagerFactory for persistence unit 'default'
2018-07-26 12:21:07.364  INFO 6484 --- [           main] o.hibernate.jpa.internal.util.LogHelper  : HHH000204: Processing PersistenceUnitInfo [
	name: default
	...]
2018-07-26 12:21:07.380  INFO 6484 --- [           main] org.hibernate.Version                    : HHH000412: Hibernate Core {5.2.17.Final}
2018-07-26 12:21:07.381  INFO 6484 --- [           main] org.hibernate.cfg.Environment            : HHH000206: hibernate.properties not found
2018-07-26 12:21:07.381  INFO 6484 --- [           main] org.hibernate.cfg.Environment            : HHH000021: Bytecode provider name : javassist
2018-07-26 12:21:07.402  INFO 6484 --- [           main] o.hibernate.annotations.common.Version   : HCANN000001: Hibernate Commons Annotations {5.0.1.Final}
2018-07-26 12:21:07.445  INFO 6484 --- [           main] org.hibernate.dialect.Dialect            : HHH000400: Using dialect: org.hibernate.dialect.H2Dialect
2018-07-26 12:21:07.502  INFO 6484 --- [           main] o.h.e.j.e.i.LobCreatorBuilderImpl        : HHH000424: Disabling contextual LOB creation as connection was null
2018-07-26 12:21:07.504  INFO 6484 --- [           main] org.hibernate.type.BasicTypeRegistry     : HHH000270: Type registration [java.util.UUID] overrides previous : org.hibernate.type.UUIDBinaryType@6e3c0c47
2018-07-26 12:21:07.620  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Registering beans for JMX exposure on startup
2018-07-26 12:21:07.621  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Bean with name 'dataSource' has been autodetected for JMX exposure
2018-07-26 12:21:07.621  INFO 6484 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Bean with name 'entityManagerFactory' has been autodetected for JMX exposure
2018-07-26 12:21:07.621  INFO 6484 --- [           main] o.s.j.e.a.An