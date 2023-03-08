---
title: SOAP를 사용하는 Spring Boot 웹 서비스
description: 
published: true
date: 2023-02-01T17:18:31.224Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:18:29.588Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Spring Boot Web Services with SOAP***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-web-services-with-soap)
{.links-list}


# SOAP를 사용한 스프링 부트 웹 서비스

웹 서비스는 한동안 사용되어 왔으며 계속해서 최신 웹 및 엔터프라이즈 개발의 중요한 부분입니다. 이 기사에서는 Spring Boot 및 SOAP를 사용하여 웹 서비스를 만드는 방법을 살펴보겠습니다.

먼저 SOAP 웹 서비스의 기본 사항과 작동 방식을 살펴보겠습니다. 그런 다음 Spring Boot로 간단한 웹 서비스를 만들고 몇 가지 주요 기능을 살펴보겠습니다. 마지막으로 Spring Boot 애플리케이션에서 SOAP 웹 서비스를 사용하는 방법을 살펴보겠습니다.

## SOAP 웹 서비스란?

SOAP 웹 서비스는 일반적으로 HTTP를 사용하여 네트워크를 통해 액세스할 수 있는 리소스 모음입니다. 이러한 리소스는 일반적으로 웹 서비스에 요청하고 응답을 받는 SOAP 클라이언트를 사용하여 액세스됩니다.

SOAP 프로토콜은 웹 서비스를 만들고 액세스할 수 있는 방법에 대한 여러 규칙을 정의합니다. 이러한 규칙은 SOAP 클라이언트와 서버가 통신하는 방법과 데이터 형식을 정의합니다.

SOAP의 주요 기능 중 하나는 언어 독립적이라는 것입니다. 즉, SOAP 웹 서비스는 모든 프로그래밍 언어로 생성될 수 있으며 모든 SOAP 클라이언트에서 사용할 수 있습니다.

## Spring Boot로 SOAP 웹 서비스 만들기

Spring Boot를 사용하면 SOAP 웹 서비스를 쉽게 만들 수 있습니다. 이 섹션에서는 국가 목록을 반환하는 간단한 웹 서비스를 만듭니다. Spring Boot 애플리케이션을 만드는 것으로 시작하겠습니다.

```
$ spring init -n web-service -dweb,soap countries-service
```

이것은 `web-service`라는 이름과 `web` 및 `soap` 종속성을 가진 새로운 Spring Boot 애플리케이션을 생성합니다.

다음으로 웹 서비스에서 반환할 국가를 나타내는 `Country` 클래스를 만듭니다.

```java
public class Country {
 
    private String name;
    private String capital;
    private String currency;
 
    // getters and setters
}
```

또한 국가 목록을 반환하는 `CountryService` 클래스를 만듭니다.

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

마지막으로 `CountryService`를 웹 서비스로 노출하기 위해 `CountryController`를 생성합니다.

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

이제 애플리케이션을 실행하고 `http://localhost:8080/countries`에서 웹 서비스에 액세스할 수 있습니다.

## SOAP 웹 서비스 노출

기본적으로 웹 서비스는 REST 웹 서비스로 노출됩니다. 그러나 이를 SOAP 웹 서비스로 노출할 수도 있습니다. 이렇게 하려면 프로젝트에 `spring-boot-starter-ws` 종속성을 추가해야 합니다.

```
$ spring init -n web-service -dweb,soap,ws countries-service
```

그러면 프로젝트에 `spring-boot-starter-ws` 종속성이 추가됩니다.

다음으로 `@Configuration` 클래스를 만들고 `@EnableWs`로 주석을 추가해야 합니다. 이렇게 하면 애플리케이션에서 Spring 웹 서비스 프레임워크가 활성화됩니다.

```java
@Configuration
@EnableWs
public class WebServiceConfig extends WsConfigurerAdapter {
}
```

또한 `MessageDispatcherServlet`을 생성하고 `ServletRegistrationBean`에 등록해야 합니다. 이 서블릿은 SOAP 요청을 처리하는 데 사용됩니다.

```java
@Bean
public ServletRegistrationBean messageDispatcherServlet(ApplicationContext applicationContext) {
    MessageDispatcherServlet servlet = new MessageDispatcherServlet();
    servlet.setApplicationContext(applicationContext);
    servlet.setTransformWsdlLocations(true);
    return new ServletRegistrationBean(servlet, "/ws/*");
}
```

또한 `DefaultWsdl11Definition` 유형의 `@Bean`을 생성해야 합니다. 이 bean은 웹 서비스용 WSDL을 생성하는 데 사용됩니다.

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

`countries.xsd` 파일은 `jaxb2-maven-plugin`을 사용하여 `Country` 클래스에서 생성됩니다.

마지막으로 `@WebService` 엔드포인트를 생성해야 합니다. 이 엔드포인트는 SOAP 요청을 처리하는 데 사용됩니다.

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

이제 애플리케이션을 실행하고 `http://localhost:8080/ws/countries.wsdl`에서 SOAP 웹 서비스에 액세스할 수 있습니다.

## SOAP 웹 서비스 사용

이 섹션에서는 Spring Boot 애플리케이션에서 SOAP 웹 서비스를 사용하는 방법을 살펴봅니다. 새로운 Spring Boot 애플리케이션을 생성하는 것으로 시작하겠습니다.

```
$ spring init -n web-service -dweb,soap,ws countries-client
```

다음으로 프로젝트에 'jaxb2-maven-plugin'을 추가하여 WSDL에서 Java 클래스를 생성해야 합니다. `pom.xml` 파일에 다음을 추가하여 이를 수행할 수 있습니다.

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

이렇게 하면 `countries.xsd` 파일과 `Countries` 및 `Country` 클래스가 생성됩니다.

다음으로 `@Configuration` 클래스를 만들고 `@EnableWs`로 주석을 추가해야 합니다. 이렇게 하면 애플리케이션에서 Spring 웹 서비스 프레임워크가 활성화됩니다.

```java
@Configuration
@EnableWs
public class WebServiceConfig extends WsConfigurerAdapter {
}
```

또한 `MessageDispatcherServlet`을 생성하고 `ServletRegistrationBean`에 등록해야 합니다. 이 서블릿은 SOAP 요청을 처리하는 데 사용됩니다.

```java
@Bean
public ServletRegistrationBean messageDispatcherServlet(ApplicationContext applicationContext) {
    MessageDispatcherServlet servlet = new MessageDispatcherServlet();
    servlet.setApplicationContext(applicationContext);
    servlet.setTransformWsdlLocations(true);
    return new ServletRegistrationBean(servlet, "/ws/*");
}
```

또한 `DefaultWsdl11Definition` 유형의 `@Bean`을 생성해야 합니다. 이 bean은 웹 서비스용 WSDL을 생성하는 데 사용됩니다.

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

`countries.xsd` 파일은 `jaxb2-maven-plugin`을 사용하여 `Country` 클래스에서 생성됩니다.

이제 애플리케이션을 실행하고 `http://localhost:8080/ws/countries.wsdl`에서 SOAP 웹 서비스에 액세스할 수 있습니다.

## 결론

이 기사에서는 Spring Boot로 SOAP 웹 서비스를 만드는 방법을 살펴보았습니다. Spring Boot 애플리케이션에서 SOAP 웹 서비스를 사용하는 방법도 살펴보았습니다.

Spring Boot를 사용하는 SOAP 웹 서비스에 대한 자세한 내용은 다음 리소스를 확인하세요.

* [Spring Boot 참조 문서: SOAP 웹 서비스](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#boot-features-webservices)
* [Spring Boot 웹 서비스 자습서](https://spring.io/guides/gs/producing-web-service/)
* [Spring Boot 웹 서비스 예제](https://www.concretepage.com/spring-boot/spring-boot-soap-web-service-example)