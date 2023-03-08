---
title: 021：使用 Junit 构建和测试 Spring Boot 应用程序
description: 
published: true
date: 2023-02-03T13:34:18.648Z
tags: 
editor: markdown
dateCreated: 2023-02-03T13:34:17.065Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [021: Building and testing a Spring Boot application with Junit***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/021-building-and-testing-a-spring-boot-application-with-junit)
{.links-list}


# 021：使用 Junit 构建和测试 Spring Boot 应用程序

Junit 是一种流行的 Java 应用程序测试框架。 Spring Boot 是一个基于 Java 的框架，用于创建微服务和 Web 应用程序。在本文中，我们将向您展示如何使用 Junit 构建和测试 Spring Boot 应用程序。

我们将在本教程中使用以下工具：

- Java 8
- 行家 3.3.9
- Eclipse Neon.3
- 联合 4.12

## 创建 Spring Boot 应用程序

我们将从创建一个 Spring Boot 应用程序开始。对于本教程，我们将使用 Spring Initializr 网站来生成我们的项目。

转到 Spring Initializr 网站（https://start.spring.io/）并输入以下信息：

- 组：com.example
- 神器：junit-tutorial
- 名称：junit-tutorial
- 描述：Junit 教程的演示项目
- 包名：com.example.junit.tutorial
- 包装：罐
- Java 版本：1.8
- 选择以下依赖项：Web、JPA、H2、Lombok

单击生成项目以下载项目。

解压缩 zip 文件并将其作为 Maven 项目导入 Eclipse。

## 编写测试用例

现在我们已经设置好项目，可以开始编写测试用例了。我们将测试以下场景：

- 给定用户名“johndoe”和密码“password”的用户
- 当用户尝试登录时
- 然后用户应该能够成功登录

在 com.example.junit.tutorial.service 包中创建一个新的 Java 类并将其命名为 LoginServiceTest.java。将以下代码添加到类中：

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

在上面的代码中，我们使用@RunWith 和@SpringBootTest 注释来运行我们的测试用例。我们还将 LoginService 注入到我们的测试用例中，以便我们可以测试 login() 方法。

login() 方法接受用户名和密码，并返回一个布尔值，指示登录是否成功。在我们的测试用例中，我们传递了用户名和密码“johndoe”和“password”。然后我们断言结果为真，这意味着登录成功。

## 运行测试用例

要运行测试用例，请右键单击 LoginServiceTest.java 类并选择 Run As > JUnit Test。

您应该在控制台中看到以下输出：

```
. ____ _ _ _ _
 /\\ / ___'_ __ _ _(_)_ __ __ _ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \
 \\/ ___)| |_)| | | | | || (_| | ) ) ) )
  ' |____| .__|_| |_|_| |_\__, | // / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot :: (v2.0.3.RELEASE)

2018-07-26 12:21:06.469 INFO 6484 --- [main] c.e.j.t.s.LoginServiceTest：在 PID 6484 的 PC-LAPTOP 上启动 LoginServiceTest（由 John Doe 在 C:\junit-tutorial 中启动）
2018-07-26 12:21:06.470 INFO 6484 --- [main] c.e.j.t.s.LoginServiceTest：未设置活动配置文件，回退到默认配置文件：默认
2018-07-26 12:21:06.526 INFO 6484 --- [main] s.c.a.AnnotationConfigApplicationContext：刷新 org.springframework.context.annotation.AnnotationConfigApplicationContext@4a3a4df7：启动日期 [2018 年 7 月 26 日星期四 12:21:06 EDT]；上下文层次的根
2018-07-26 12:21:07.067 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：在启动时为 JMX 暴露注册 bean
2018-07-26 12:21:07.068 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：已自动检测到名为“dataSource”的 Bean 以进行 JMX 暴露
2018-07-26 12:21:07.069 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：定位 MBean“dataSource”：向 JMX 服务器注册为 MBean [com.zaxxer.hikari:name=dataSource,type=HikariDataSource]
2018-07-26 12:21:07.076 INFO 6484 --- [main] o.s.b.a.h2.H2ConsoleAutoConfiguration：H2 控制台在“/h2-console”可用。数据库位于 'jdbc:h2:mem:testdb'
2018-07-26 12:21:07.094 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：位于 MBean 'h2:name=MemoryManagerService': 向 JMX 服务器注册为 MBean [org.h2.mvstore.db.H2Database:name=内存管理器服务]
2018-07-26 12:21:07.095 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：定位 MBean 'h2:name=DatabaseStatusMBean'：向 JMX 服务器注册为 MBean [org.h2.engine.DatabaseStatusMBean]
2018-07-26 12:21:07.097 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：定位 MBean 'h2:name=DeadlockDetector'：作为 MBean [org.h2.engine.DeadlockDetector] 向 JMX 服务器注册
2018-07-26 12:21:07.098 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：定位 MBean 'h2:name=ThreadPool'：向 JMX 服务器注册为 MBean [org.h2.engine.ThreadPool]
2018-07-26 12:21:07.102 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：定位 MBean 'h2:name=SessionTracker'：向 JMX 服务器注册为 MBean [org.h2.engine.SessionTracker]
2018-07-26 12:21:07.104 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：定位 MBean 'h2:name=WebServer'：向 JMX 服务器注册为 MBean [org.h2.tools.Server]
2018-07-26 12:21:07.105 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：定位 MBean 'h2:name=ConnectionPool'：作为 MBean [org.h2.engine.ConnectionPool] 向 JMX 服务器注册
2018-07-26 12:21:07.106 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：定位 MBean 'h2:name=StatementTracker'：向 JMX 服务器注册为 MBean [org.h2.engine.StatementTracker]
2018-07-26 12:21:07.107 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：定位 MBean 'h2:name=SystemProperties'：向 JMX 服务器注册为 MBean [org.h2.engine.SystemProperties]
2018-07-26 12:21:07.108 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：定位的 MBean 'h2:name=Versions'：向 JMX 服务器注册为 MBean [org.h2.engine.Versions]
2018-07-26 12:21:07.109 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：位于 MBean 'h2:name=ClusterSettings'：作为 MBean [org.h2.cluster.settings.ClusterSettings] 向 JMX 服务器注册
2018-07-26 12:21:07.110 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：定位 MBean 'h2:name=ServerInfo'：向 JMX 服务器注册为 MBean [org.h2.engine.ServerInfo]
2018-07-26 12:21:07.115 INFO 6484 --- [main] o.s.b.w.embedded.tomcat.TomcatWebServer：Tomcat 初始化端口：8080 (http)
2018-07-26 12:21:07.118 INFO 6484 --- [main] o.apache.catalina.core.StandardService：启动服务 [Tomcat]
2018-07-26 12:21:07.118 INFO 6484 --- [main] org.apache.catalina.core.StandardEngine：启动 Servlet 引擎：Apache Tomcat/8.5.27
2018-07-26 12:21:07.119 INFO 6484 --- [ost-startStop-1] o.a.catalina.core.AprLifecycleListener：在 java 上找不到基于 APR 的 Apache Tomcat Native 库，它允许在生产环境中实现最佳性能。 library.path: [C:\Program Files\Java\jdk1.8.0_171\bin;C:\WINDOWS\Sun\Java\bin;C:\WINDOWS\system32;C:\WINDOWS;C:/Program Files/Java /jdk1.8.0_171/jre/bin/server;C:/Program Files/Java/jdk1.8.0_171/jre/bin;C:/Program Files/Java/jdk1.8.0_171/jre/lib/amd64;C: \ProgramData\Oracle\Java\javapath;C:\WINDOWS\system32;C:\WINDOWS;C:\WINDOWS\System32\Wbem;C:\WINDOWS\System32\WindowsPowerShell\v1.0\;C:\Program Files\ Git\cmd;C:\Program Files\nodejs\;C:\Program Files (x86)\Brackets\command;C:\Users\John Doe\AppData\Local\Microsoft\WindowsApps;;.]
2018-07-26 12:21:07.154 INFO 6484 --- [ost-startStop-1] o.a.c.c.C.[Tomcat].[localhost].[/]：初始化 Spring 嵌入式 WebApplicationContext
2018-07-26 12:21:07.154 INFO 6484 --- [ost-startStop-1] o.s.web.context.ContextLoader：Root WebApplicationContext：初始化在 350 毫秒内完成
2018-07-26 12:21:07.295 INFO 6484 --- [ost-startStop-1] o.s.b.w.servlet.ServletRegistrationBean：Servlet dispatcherServlet 映射到 [/]
2018-07-26 12:21:07.296 INFO 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean：映射过滤器：'characterEncodingFilter' 到：[/*]
2018-07-26 12:21:07.296 INFO 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean：映射过滤器：'hiddenHttpMethodFilter' 到：[/*]
2018-07-26 12:21:07.296 INFO 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean：映射过滤器：'httpPutFormContentFilter' 到：[/*]
2018-07-26 12:21:07.296 INFO 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean：映射过滤器：'requestContextFilter' 到：[/*]
2018-07-26 12:21:07.363 INFO 6484 --- [main] j.LocalContainerEntityManagerFactoryBean：为持久性单元“默认”构建 JPA 容器 EntityManagerFactory
2018-07-26 12:21:07.364 INFO 6484 --- [主要] o.hibernate.jpa.internal.util.LogHelper：HHH000204：处理 PersistenceUnitInfo [
名称：默认
...]
2018-07-26 12:21:07.380 INFO 6484 --- [main] org.hibernate.Version : HHH000412: Hibernate Core {5.2.17.Final}
2018-07-26 12:21:07.381 INFO 6484 --- [main] org.hibernate.cfg.Environment: HHH000206: hibernate.properties not found
2018-07-26 12:21:07.381 INFO 6484 --- [main] org.hibernate.cfg.Environment：HHH000021：字节码提供程序名称：javassist
2018-07-26 12:21:07.402 INFO 6484 --- [main] o.hibernate.annotations.common.Version：HCANN000001：Hibernate Commons Annotations {5.0.1.Final}
2018-07-26 12:21:07.445 INFO 6484 --- [main] org.hibernate.dialect.Dialect：HHH000400：使用方言：org.hibernate.dialect.H2Dialect
2018-07-26 12:21:07.502 INFO 6484 --- [main] o.h.e.j.e.i.LobCreatorBuilderImpl：HHH000424：由于连接为空而禁用上下文 LOB 创建
2018-07-26 12:21:07.504 INFO 6484 --- [main] org.hibernate.type.BasicTypeRegistry：HHH000270：类型注册 [java.util.UUID] 覆盖以前的：org.hibernate.type.UUIDBinaryType@6e3c0c47
2018-07-26 12:21:07.620 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：在启动时为 JMX 暴露注册 bean
2018-07-26 12:21:07.621 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：已自动检测到名为“dataSource”的 Bean 以进行 JMX 暴露
2018-07-26 12:21:07.621 INFO 6484 --- [main] o.s.j.e.a.AnnotationMBeanExporter：已自动检测到名为“entityManagerFactory”的 Bean 以进行 JMX 暴露
2018-07-26 12:21:07.621 信息 6484 --- [主要] o.s.j.e.a.An