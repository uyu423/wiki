---
title: Spring Boot Web Services with SOAP
description: 
published: true
date: 2023-02-01T17:18:33.663Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:18:29.582Z
---

- [Servicios web Spring Boot con SOAP***Spanish** version of this document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-web-services-with-soap)
{.links-list}
- [SOAP를 사용하는 Spring Boot 웹 서비스***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-web-services-with-soap)
{.links-list}
- [带有 SOAP 的 Spring Boot Web 服务***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-web-services-with-soap)
{.links-list}


# Spring Boot Web Services with SOAP

Web services have been around for a while now, and they continue to be an important part of modern web and enterprise development. In this article, we'll take a look at how to create web services with Spring Boot and SOAP.

We'll start by looking at the basics of SOAP web services and how they work. We'll then create a simple web service with Spring Boot and take a look at some of the key features. Finally, we'll see how to consume a SOAP web service from a Spring Boot application.

## What is a SOAP Web Service?

A SOAP web service is a collection of resources that can be accessed over the network, typically using HTTP. These resources are typically accessed using a SOAP client, which makes a request to the web service and receives a response.

The SOAP protocol defines a number of rules for how web services can be created and accessed. These rules define how the SOAP client and server communicate, and how the data is formatted.

One of the key features of SOAP is that it is language-independent. This means that a SOAP web service can be created in any programming language, and consumed by any SOAP client.

## Creating a SOAP Web Service with Spring Boot

Spring Boot makes it easy to create a SOAP web service. In this section, we'll create a simple web service that will return a list of countries. We'll start by creating a Spring Boot application:

```
$ spring init -n web-service -dweb,soap countries-service
```

This will create a new Spring Boot application with the name `web-service`, and the dependencies `web` and `soap`.

Next, we'll create a `Country` class to represent the countries that we'll be returning from our web service:

```java
public class Country {
 
    private String name;
    private String capital;
    private String currency;
 
    // getters and setters
}
```

We'll also create a `CountryService` class that will return a list of countries:

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

Finally, we'll create a `CountryController` to expose our `CountryService` as a web service:

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

We can now run our application and access our web service at `http://localhost:8080/countries`.

## Exposing a SOAP Web Service

By default, our web service will be exposed as a REST web service. However, we can also expose it as a SOAP web service. To do this, we need to add the `spring-boot-starter-ws` dependency to our project:

```
$ spring init -n web-service -dweb,soap,ws countries-service
```

This will add the `spring-boot-starter-ws` dependency to our project.

Next, we need to create a `@Configuration` class and annotate it with `@EnableWs`. This will enable the Spring Web Services framework in our application:

```java
@Configuration
@EnableWs
public class WebServiceConfig extends WsConfigurerAdapter {
}
```

We also need to create a `MessageDispatcherServlet` and register it with the `ServletRegistrationBean`. This servlet will be used to handle SOAP requests:

```java
@Bean
public ServletRegistrationBean messageDispatcherServlet(ApplicationContext applicationContext) {
    MessageDispatcherServlet servlet = new MessageDispatcherServlet();
    servlet.setApplicationContext(applicationContext);
    servlet.setTransformWsdlLocations(true);
    return new ServletRegistrationBean(servlet, "/ws/*");
}
```

We also need to create a `@Bean` of type `DefaultWsdl11Definition`. This bean will be used to generate the WSDL for our web service:

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

The `countries.xsd` file is generated from the `Country` class using the `jaxb2-maven-plugin`.

Finally, we need to create a `@WebService` endpoint. This endpoint will be used to handle SOAP requests:

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

We can now run our application and access our SOAP web service at `http://localhost:8080/ws/countries.wsdl`.

## Consuming a SOAP Web Service

In this section, we'll see how to consume a SOAP web service from a Spring Boot application. We'll start by creating a new Spring Boot application:

```
$ spring init -n web-service -dweb,soap,ws countries-client
```

Next, we need to add the `jaxb2-maven-plugin` to our project to generate the Java classes from the WSDL. We can do this by adding the following to our `pom.xml` file:

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

This will generate the `countries.xsd` file and the `Countries` and `Country` classes.

Next, we need to create a `@Configuration` class and annotate it with `@EnableWs`. This will enable the Spring Web Services framework in our application:

```java
@Configuration
@EnableWs
public class WebServiceConfig extends WsConfigurerAdapter {
}
```

We also need to create a `MessageDispatcherServlet` and register it with the `ServletRegistrationBean`. This servlet will be used to handle SOAP requests:

```java
@Bean
public ServletRegistrationBean messageDispatcherServlet(ApplicationContext applicationContext) {
    MessageDispatcherServlet servlet = new MessageDispatcherServlet();
    servlet.setApplicationContext(applicationContext);
    servlet.setTransformWsdlLocations(true);
    return new ServletRegistrationBean(servlet, "/ws/*");
}
```

We also need to create a `@Bean` of type `DefaultWsdl11Definition`. This bean will be used to generate the WSDL for our web service:

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

The `countries.xsd` file is generated from the `Country` class using the `jaxb2-maven-plugin`.

We can now run our application and access our SOAP web service at `http://localhost:8080/ws/countries.wsdl`.

## Conclusion

In this article, we've looked at how to create a SOAP web service with Spring Boot. We've also seen how to consume a SOAP web service from a Spring Boot application.

For more information on SOAP web services with Spring Boot, check out the following resources:

* [Spring Boot Reference Documentation: SOAP Web Services](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#boot-features-webservices)
* [Spring Boot Web Services Tutorial](https://spring.io/guides/gs/producing-web-service/)
* [Spring Boot Web Services Example](https://www.concretepage.com/spring-boot/spring-boot-soap-web-service-example)