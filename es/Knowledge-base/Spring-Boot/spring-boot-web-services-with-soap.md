---
title: Servicios web Spring Boot con SOAP
description: 
published: true
date: 2023-02-01T17:18:31.301Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:18:29.589Z
---

> Este artículo se tradujo automáticamente con la **API de Google Cloud Translation**.
Algunas páginas pueden leerse mejor que el original.{.is-info}

- [Spring Boot Web Services with SOAP***Spanish** version of this document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-web-services-with-soap)
{.links-list}


# Servicios web Spring Boot con SOAP

Los servicios web existen desde hace un tiempo y continúan siendo una parte importante del desarrollo web y empresarial moderno. En este artículo, veremos cómo crear servicios web con Spring Boot y SOAP.

Comenzaremos analizando los conceptos básicos de los servicios web SOAP y cómo funcionan. Luego, crearemos un servicio web simple con Spring Boot y veremos algunas de las características clave. Finalmente, veremos cómo consumir un servicio web SOAP desde una aplicación Spring Boot.

## ¿Qué es un servicio web SOAP?

Un servicio web SOAP es una colección de recursos a los que se puede acceder a través de la red, normalmente mediante HTTP. Por lo general, se accede a estos recursos mediante un cliente SOAP, que realiza una solicitud al servicio web y recibe una respuesta.

El protocolo SOAP define una serie de reglas sobre cómo se pueden crear y acceder a los servicios web. Estas reglas definen cómo se comunican el servidor y el cliente SOAP, y cómo se formatean los datos.

Una de las características clave de SOAP es que es independiente del idioma. Esto significa que un servicio web SOAP puede crearse en cualquier lenguaje de programación y ser consumido por cualquier cliente SOAP.

## Creación de un servicio web SOAP con Spring Boot

Spring Boot facilita la creación de un servicio web SOAP. En esta sección, crearemos un servicio web simple que devolverá una lista de países. Comenzaremos creando una aplicación Spring Boot:

```
$ spring init -n web-service -dweb,soap countries-service
```

Esto creará una nueva aplicación Spring Boot con el nombre `web-service` y las dependencias `web` y `soap`.

A continuación, crearemos una clase `País` para representar los países que devolveremos desde nuestro servicio web:

```java
public class Country {
 
    private String name;
    private String capital;
    private String currency;
 
    // getters and setters
}
```

También crearemos una clase `CountryService` que devolverá una lista de países:

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

Finalmente, crearemos un `CountryController` para exponer nuestro `CountryService` como un servicio web:

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

Ahora podemos ejecutar nuestra aplicación y acceder a nuestro servicio web en `http://localhost:8080/countries`.

## Exponiendo un servicio web SOAP

De forma predeterminada, nuestro servicio web estará expuesto como un servicio web REST. Sin embargo, también podemos exponerlo como un servicio web SOAP. Para hacer esto, necesitamos agregar la dependencia `spring-boot-starter-ws` a nuestro proyecto:

```
$ spring init -n web-service -dweb,soap,ws countries-service
```

Esto agregará la dependencia `spring-boot-starter-ws` a nuestro proyecto.

A continuación, necesitamos crear una clase `@Configuration` y anotarla con `@EnableWs`. Esto habilitará el marco de Spring Web Services en nuestra aplicación:

```java
@Configuration
@EnableWs
public class WebServiceConfig extends WsConfigurerAdapter {
}
```

También necesitamos crear un `MessageDispatcherServlet` y registrarlo con `ServletRegistrationBean`. Este servlet se usará para manejar solicitudes SOAP:

```java
@Bean
public ServletRegistrationBean messageDispatcherServlet(ApplicationContext applicationContext) {
    MessageDispatcherServlet servlet = new MessageDispatcherServlet();
    servlet.setApplicationContext(applicationContext);
    servlet.setTransformWsdlLocations(true);
    return new ServletRegistrationBean(servlet, "/ws/*");
}
```

También necesitamos crear un `@Bean` de tipo `DefaultWsdl11Definition`. Este bean se usará para generar el WSDL para nuestro servicio web:

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

El archivo `countries.xsd` se genera a partir de la clase `Country` utilizando `jaxb2-maven-plugin`.

Finalmente, necesitamos crear un punto final `@WebService`. Este punto final se usará para manejar solicitudes SOAP:

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

Ahora podemos ejecutar nuestra aplicación y acceder a nuestro servicio web SOAP en `http://localhost:8080/ws/countries.wsdl`.

## Consumo de un servicio web SOAP

En esta sección, veremos cómo consumir un servicio web SOAP desde una aplicación Spring Boot. Comenzaremos creando una nueva aplicación Spring Boot:

```
$ spring init -n web-service -dweb,soap,ws countries-client
```

A continuación, debemos agregar `jaxb2-maven-plugin` a nuestro proyecto para generar las clases de Java desde el WSDL. Podemos hacer esto agregando lo siguiente a nuestro archivo `pom.xml`:

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

Esto generará el archivo `countries.xsd` y las clases `Countries` y `Country`.

A continuación, necesitamos crear una clase `@Configuration` y anotarla con `@EnableWs`. Esto habilitará el marco de Spring Web Services en nuestra aplicación:

```java
@Configuration
@EnableWs
public class WebServiceConfig extends WsConfigurerAdapter {
}
```

También necesitamos crear un `MessageDispatcherServlet` y registrarlo con `ServletRegistrationBean`. Este servlet se usará para manejar solicitudes SOAP:

```java
@Bean
public ServletRegistrationBean messageDispatcherServlet(ApplicationContext applicationContext) {
    MessageDispatcherServlet servlet = new MessageDispatcherServlet();
    servlet.setApplicationContext(applicationContext);
    servlet.setTransformWsdlLocations(true);
    return new ServletRegistrationBean(servlet, "/ws/*");
}
```

También necesitamos crear un `@Bean` de tipo `DefaultWsdl11Definition`. Este bean se usará para generar el WSDL para nuestro servicio web:

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

El archivo `countries.xsd` se genera a partir de la clase `Country` utilizando `jaxb2-maven-plugin`.

Ahora podemos ejecutar nuestra aplicación y acceder a nuestro servicio web SOAP en `http://localhost:8080/ws/countries.wsdl`.

## Conclusión

En este artículo, hemos visto cómo crear un servicio web SOAP con Spring Boot. También hemos visto cómo consumir un servicio web SOAP desde una aplicación Spring Boot.

Para obtener más información sobre los servicios web SOAP con Spring Boot, consulte los siguientes recursos:

* [Documentación de referencia de Spring Boot: servicios web SOAP] (https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#boot-features-webservices)
* [Tutorial de servicios web Spring Boot](https://spring.io/guides/gs/producing-web-service/)
* [Ejemplo de servicios web Spring Boot](https://www.concretepage.com/spring-boot/spring-boot-soap-web-service-example)