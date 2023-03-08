---
title: 带有 SOAP 的 Spring Boot Web 服务
description: 
published: true
date: 2023-02-01T17:18:31.271Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:18:29.590Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Spring Boot Web Services with SOAP***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-web-services-with-soap)
{.links-list}


# 使用 SOAP 的 Spring Boot Web 服务

Web 服务已经存在一段时间了，它们仍然是现代 Web 和企业开发的重要组成部分。在本文中，我们将了解如何使用 Spring Boot 和 SOAP 创建 Web 服务。

我们将从了解 SOAP Web 服务的基础知识及其工作原理开始。然后，我们将使用 Spring Boot 创建一个简单的 Web 服务，并了解一些关键特性。最后，我们将了解如何从 Spring Boot 应用程序使用 SOAP Web 服务。

## 什么是 SOAP Web 服务？

SOAP Web 服务是可以通过网络访问的资源集合，通常使用 HTTP。这些资源通常使用 SOAP 客户端访问，该客户端向 Web 服务发出请求并接收响应。

SOAP 协议定义了许多关于如何创建和访问 Web 服务的规则。这些规则定义了 SOAP 客户端和服务器如何通信，以及如何格式化数据。

SOAP 的关键特性之一是它与语言无关。这意味着 SOAP Web 服务可以用任何编程语言创建，并由任何 SOAP 客户端使用。

## 使用 Spring Boot 创建 SOAP Web 服务

Spring Boot 使创建 SOAP Web 服务变得容易。在本节中，我们将创建一个简单的 Web 服务，它将返回一个国家列表。我们将从创建一个 Spring Boot 应用程序开始：

```
$ spring init -n web-service -dweb,soap countries-service
```

这将创建一个名为“web-service”的新 Spring Boot 应用程序，以及依赖项“web”和“soap”。

接下来，我们将创建一个 `Country` 类来表示我们将从我们的网络服务返回的国家：

```java
public class Country {
 
    private String name;
    private String capital;
    private String currency;
 
    // getters and setters
}
```

我们还将创建一个 CountryService 类，它将返回一个国家列表：

```java
@Service
public class CountryService {
 
    private static final List<Country> countries = Arrays.asList(
        new Country("Australia", "Canberra", "AUD"),
        new Country("Canada", "Ottawa", "CAD"),
        new Country("France", "Paris", "EUR"),
        new Country("Germany", "Berlin", "EUR"),
        new Country("India", "New Delhi", "INR"),
        new Country("Japan", "Tokyo", "JPY"),
        new Country("United Kingdom", "London", "GBP"),
        new Country("United States", "Washington D.C.", "USD")
    );
 
    public List<Country> getCountries() {
        return countries;
    }
}
```

最后，我们将创建一个 CountryController 以将我们的 CountryService 公开为 Web 服务：

```java
@RestController
@RequestMapping("/countries")
public class CountryController {
 
    @Autowired
    private CountryService countryService;
 
    @GetMapping
    public List<Country> getCountries() {
        return countryService.getCountries();
    }
}
```

我们现在可以运行我们的应用程序并在 http://localhost:8080/countries 访问我们的网络服务。

## 公开 SOAP Web 服务

默认情况下，我们的 Web 服务将作为 REST Web 服务公开。但是，我们也可以将其公开为 SOAP Web 服务。为此，我们需要将 spring-boot-starter-ws 依赖项添加到我们的项目中：

```
$ spring init -n web-service -dweb,soap,ws countries-service
```

这会将 `spring-boot-starter-ws` 依赖项添加到我们的项目中。

接下来，我们需要创建一个 `@Configuration` 类并使用 `@EnableWs` 注释它。这将在我们的应用程序中启用 Spring Web 服务框架：

```java
@Configuration
@EnableWs
public class WebServiceConfig extends WsConfigurerAdapter {
}
```

我们还需要创建一个“MessageDispatcherServlet”并将其注册到“ServletRegistrationBean”。该 servlet 将用于处理 SOAP 请求：

```java
@Bean
public ServletRegistrationBean messageDispatcherServlet(ApplicationContext applicationContext) {
    MessageDispatcherServlet servlet = new MessageDispatcherServlet();
    servlet.setApplicationContext(applicationContext);
    servlet.setTransformWsdlLocations(true);
    return new ServletRegistrationBean(servlet, "/ws/*");
}
```

我们还需要创建一个类型为“DefaultWsdl11Definition”的“@Bean”。该 bean 将用于为我们的 Web 服务生成 WSDL：

```java
@Bean(name = "countries")
public DefaultWsdl11Definition defaultWsdl11Definition(XsdSchema countriesSchema) {
    DefaultWsdl11Definition wsdl11Definition = new DefaultWsdl11Definition();
    wsdl11Definition.setPortTypeName("CountriesPort");
    wsdl11Definition.setLocationUri("/ws");
    wsdl11Definition.setTargetNamespace("http://springboot.it/countries");
    wsdl11Definition.setSchema(countriesSchema);
    return wsdl11Definition;
}
 
@Bean
public XsdSchema countriesSchema() {
    return new SimpleXsdSchema(new ClassPathResource("countries.xsd"));
}
```

`countries.xsd` 文件是使用 `jaxb2-maven-plugin` 从 `Country` 类生成的。

最后，我们需要创建一个“@WebService”端点。此端点将用于处理 SOAP 请求：

```java
@WebService
public class CountryEndpoint {
 
    @Autowired
    private CountryService countryService;
 
    @WebMethod
    public List<Country> getCountries() {
        return countryService.getCountries();
    }
}
```

我们现在可以运行我们的应用程序并在“http://localhost:8080/ws/countries.wsdl”访问我们的 SOAP Web 服务。

## 使用 SOAP Web 服务

在本节中，我们将了解如何从 Spring Boot 应用程序使用 SOAP Web 服务。我们将从创建一个新的 Spring Boot 应用程序开始：

```
$ spring init -n web-service -dweb,soap,ws countries-client
```

接下来，我们需要将 `jaxb2-maven-plugin` 添加到我们的项目中，以从 WSDL 生成 Java 类。我们可以通过将以下内容添加到我们的 `pom.xml` 文件来做到这一点：

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.jvnet.jaxb2.maven2</groupId>
            <artifactId>maven-jaxb2-plugin</artifactId>
            <version>0.13.2</version>
            <executions>
                <execution>
                    <goals>
                        <goal>generate</goal>
                    </goals>
                </execution>
            </executions>
            <configuration>
                <schemaLanguage>WSDL</schemaLanguage>
                <generatePackage>springboot.it.countries</generatePackage>
                <schemas>
                    <schema>
                        <url>http://localhost:8080/ws/countries.wsdl</url>
                    </schema>
                </schemas>
            </configuration>
        </plugin>
    </plugins>
</build>
```

这将生成 `countries.xsd` 文件以及 `Countries` 和 `Country` 类。

接下来，我们需要创建一个 `@Configuration` 类并使用 `@EnableWs` 注释它。这将在我们的应用程序中启用 Spring Web 服务框架：

```java
@Configuration
@EnableWs
public class WebServiceConfig extends WsConfigurerAdapter {
}
```

我们还需要创建一个“MessageDispatcherServlet”并将其注册到“ServletRegistrationBean”。该 servlet 将用于处理 SOAP 请求：

```java
@Bean
public ServletRegistrationBean messageDispatcherServlet(ApplicationContext applicationContext) {
    MessageDispatcherServlet servlet = new MessageDispatcherServlet();
    servlet.setApplicationContext(applicationContext);
    servlet.setTransformWsdlLocations(true);
    return new ServletRegistrationBean(servlet, "/ws/*");
}
```

我们还需要创建一个类型为“DefaultWsdl11Definition”的“@Bean”。该 bean 将用于为我们的 Web 服务生成 WSDL：

```java
@Bean(name = "countries")
public DefaultWsdl11Definition defaultWsdl11Definition(XsdSchema countriesSchema) {
    DefaultWsdl11Definition wsdl11Definition = new DefaultWsdl11Definition();
    wsdl11Definition.setPortTypeName("CountriesPort");
    wsdl11Definition.setLocationUri("/ws");
    wsdl11Definition.setTargetNamespace("http://springboot.it/countries");
    wsdl11Definition.setSchema(countriesSchema);
    return wsdl11Definition;
}
 
@Bean
public XsdSchema countriesSchema() {
    return new SimpleXsdSchema(new ClassPathResource("countries.xsd"));
}
```

`countries.xsd` 文件是使用 `jaxb2-maven-plugin` 从 `Country` 类生成的。

我们现在可以运行我们的应用程序并在“http://localhost:8080/ws/countries.wsdl”访问我们的 SOAP Web 服务。

## 结论

在本文中，我们了解了如何使用 Spring Boot 创建 SOAP Web 服务。我们还了解了如何从 Spring Boot 应用程序使用 SOAP Web 服务。

有关使用 Spring Boot 的 SOAP Web 服务的更多信息，请查看以下资源：

* [Spring Boot 参考文档：SOAP Web 服务](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#boot-features-webservices)
* [Spring Boot Web 服务教程](https://spring.io/guides/gs/producing-web-service/)
* [Spring Boot Web 服务示例](https://www.concretepage.com/spring-boot/spring-boot-soap-web-service-example)