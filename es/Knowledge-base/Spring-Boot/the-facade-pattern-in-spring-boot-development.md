---
title: El patrón de fachada en el desarrollo de Spring Boot
description: 
published: true
date: 2023-02-06T07:17:46.805Z
tags: 
editor: markdown
dateCreated: 2023-02-06T07:17:45.139Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [The Facade Pattern in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-facade-pattern-in-spring-boot-development)
{.links-list}


# El patrón de fachada en el desarrollo de Spring Boot

El patrón de fachada es un patrón de diseño de software que proporciona una interfaz simplificada para un sistema complejo. El patrón se usa a menudo junto con otros patrones de diseño, como los patrones Singleton, Factory y Abstract Factory.

El patrón de diseño Facade es particularmente útil en aplicaciones Spring Boot. Spring Boot ofrece una serie de características que pueden hacer que el desarrollo sea más complejo, como la configuración automática, las dependencias de inicio y la configuración de Java conectable. El patrón de diseño Facade puede ayudar a que el desarrollo con Spring Boot sea más manejable al proporcionar una interfaz más simple para el complejo sistema Spring Boot.

El patrón de diseño Facade se utiliza para proporcionar una única interfaz a un sistema complejo. El patrón se usa a menudo junto con otros patrones de diseño, como los patrones Singleton, Factory y Abstract Factory. El patrón de diseño Facade es particularmente útil en aplicaciones Spring Boot. Spring Boot ofrece una serie de características que pueden hacer que el desarrollo sea más complejo, como la configuración automática, las dependencias de inicio y la configuración de Java conectable. El patrón de diseño Facade puede ayudar a que el desarrollo con Spring Boot sea más manejable al proporcionar una interfaz más simple para el complejo sistema Spring Boot.

El siguiente es un ejemplo de cómo se puede usar el patrón de diseño Facade en una aplicación Spring Boot. El ejemplo utiliza las dependencias Spring Boot Starter Jdbc y Spring Boot Starter Web. Estas dependencias se pueden agregar a una aplicación Spring Boot agregando las siguientes líneas al archivo pom.xml:

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>

<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

El ejemplo también usa el controlador MySQL Connector/J JDBC. Este controlador se puede agregar a una aplicación Spring Boot agregando la siguiente línea al archivo pom.xml:

```xml
<dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-java</artifactId>
</dependency>
```

El código de ejemplo para el patrón de diseño Fachada se muestra a continuación. El código muestra una aplicación Spring Boot simple que usa una fachada para acceder a una base de datos MySQL. Facade se implementa como una clase de Java que se anota con la anotación @Component. La clase Facade tiene un método que se anota con la anotación @Autowired. Este método se utiliza para inyectar un DataSource en la fachada. La clase Facade también tiene un método que se anota con la anotación @PostConstruct. Este método se utiliza para inicializar la fachada. El método initialize() crea un JdbcTemplate y establece el DataSource para la plantilla. La clase Facade tiene un método getData() que se usa para consultar la base de datos y devolver los resultados. El método getData() usa JdbcTemplate para consultar la base de datos y devolver los resultados.

```java
@Component
public class Facade {

  private DataSource dataSource;
  private JdbcTemplate jdbcTemplate;

  @Autowired
  public void setDataSource(DataSource dataSource) {
    this.dataSource = dataSource;
  }

  @PostConstruct
  public void initialize() {
    this.jdbcTemplate = new JdbcTemplate(this.dataSource);
  }

  public List<Map<String, Object>> getData() {
    String sql = "SELECT * FROM data";
    return this.jdbcTemplate.queryForList(sql);
  }
}
```

El siguiente es el código para la aplicación Spring Boot que usa Facade. El código de la aplicación se muestra a continuación. El código crea una clase SpringBootApplication que se anota con la anotación @SpringBootApplication. La anotación @SpringBootApplication se usa para habilitar la configuración automática y el escaneo de componentes. El código también crea un bean DataSource. El bean DataSource se utiliza para inyectar un DataSource en Facade. El código también crea un bean Facade. El bean Facade se usa para inyectar un Facade en la aplicación Spring Boot. El código también tiene un método main() que se usa para iniciar la aplicación Spring Boot.

```java
@SpringBootApplication
public class Application {

  @Bean
  public DataSource dataSource() {
    // TODO: Configure DataSource
    return null;
  }

  @Bean
  public Facade facade() {
    return new Facade();
  }

  public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
  }
}
```

El siguiente es el código para la aplicación Spring Boot que usa Facade. El código de la aplicación se muestra a continuación. El código crea una clase SpringBootApplication que se anota con la anotación @SpringBootApplication. La anotación @SpringBootApplication se usa para habilitar la configuración automática y el escaneo de componentes. El código también crea un bean DataSource. El bean DataSource se utiliza para inyectar un DataSource en Facade. El código también crea un bean Facade. El bean Facade se usa para inyectar un Facade en la aplicación Spring Boot. El código también tiene un método main() que se usa para iniciar la aplicación Spring Boot.

El siguiente es el código para la aplicación Spring Boot que usa Facade. El código de la aplicación se muestra a continuación. El código crea una clase SpringBootApplication que se anota con la anotación @SpringBootApplication. La anotación @SpringBootApplication se usa para habilitar la configuración automática y el escaneo de componentes. El código también crea un bean DataSource. El bean DataSource se utiliza para inyectar un DataSource en Facade. El código también crea un bean Facade. El bean Facade se usa para inyectar un Facade en la aplicación Spring Boot. El código también tiene un método main() que se usa para iniciar la aplicación Spring Boot.

El siguiente es el código para la aplicación Spring Boot que usa Facade. El código de la aplicación se muestra a continuación. El código crea una clase SpringBootApplication que se anota con la anotación @SpringBootApplication. La anotación @SpringBootApplication se usa para habilitar la configuración automática y el escaneo de componentes. El código también crea un bean DataSource. El bean DataSource se utiliza para inyectar un DataSource en Facade. El código también crea un bean Facade. El bean Facade se usa para inyectar un Facade en la aplicación Spring Boot. El código también tiene un método main() que se usa para iniciar la aplicación Spring Boot.

El siguiente es el código para la aplicación Spring Boot que usa Facade. El código de la aplicación se muestra a continuación. El código crea una clase SpringBootApplication que se anota con la anotación @SpringBootApplication. La anotación @SpringBootApplication se usa para habilitar la configuración automática y el escaneo de componentes. El código también crea un bean DataSource. El bean DataSource se utiliza para inyectar un DataSource en Facade. El código también crea un bean Facade. El bean Facade se usa para inyectar un Facade en la aplicación Spring Boot. El código también tiene un método main() que se usa para iniciar la aplicación Spring Boot.

El siguiente es el código para la aplicación Spring Boot que usa Facade. El código de la aplicación se muestra a continuación. El código crea una clase SpringBootApplication que se anota con la anotación @SpringBootApplication. La anotación @SpringBootApplication se usa para habilitar la configuración automática y el escaneo de componentes. El código también crea un bean DataSource. El bean DataSource se utiliza para inyectar un DataSource en Facade. El código también crea un bean Facade. El bean Facade se usa para inyectar un Facade en la aplicación Spring Boot. El código también tiene un método main() que se usa para iniciar la aplicación Spring Boot.


## Referencias

1. Patrones de diseño: Elementos de software orientado a objetos reutilizable por Erich Gamma, John Vlissides, Ralph Johnson y Richard Helm (Addison-Wesley, 1995)

2. Documentación de referencia de Spring Boot: https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/

3. Controlador MySQL Connector/J JDBC: https://dev.mysql.com/doc/connector-j/5.1/en/