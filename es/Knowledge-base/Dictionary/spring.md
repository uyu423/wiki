---
title: Spring
description: 
published: true
date: 2023-02-03T03:24:13.515Z
tags: 
editor: markdown
dateCreated: 2023-02-03T03:24:07.874Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring***English** document is available*](/en/Knowledge-base/Dictionary/spring)
{.links-list}


# Descripción general
Spring es un marco de aplicación de código abierto para el desarrollo de Java. Proporciona un modelo integral de programación y configuración para aplicaciones empresariales modernas basadas en Java. Está diseñado para facilitar el proceso de desarrollo al proporcionar un enfoque coherente para crear y mantener aplicaciones empresariales.

# Descripción
Spring es un marco de aplicación y un contenedor de inversión de control (IoC) para la plataforma Java. Está diseñado para simplificar el desarrollo de aplicaciones empresariales proporcionando un modelo de programación coherente y un conjunto de herramientas para gestionar las complejidades del desarrollo de aplicaciones empresariales. Spring permite a los desarrolladores centrarse en la lógica comercial de la aplicación, en lugar de las complejidades de la infraestructura subyacente.

Las características principales de Spring incluyen: inyección de dependencia, programación orientada a aspectos, acceso a datos y gestión de transacciones, mensajería y desarrollo web. Spring también proporciona una variedad de herramientas para probar y administrar la aplicación, incluida la integración con marcos web populares como Struts y JSF.

Spring es altamente extensible y se puede utilizar para crear una amplia variedad de aplicaciones, desde aplicaciones web simples hasta aplicaciones empresariales complejas. Se puede utilizar para desarrollar aplicaciones para la web, el escritorio y los dispositivos móviles.

# Historia
Spring fue lanzado inicialmente en 2003 por Rod Johnson, el fundador del proyecto Spring Framework. Desde entonces, se ha convertido en uno de los frameworks de aplicaciones más populares para el desarrollo de Java. Ahora es administrado por la división SpringSource de VMware, Inc.

# Características
Spring proporciona un modelo integral de programación y configuración para aplicaciones empresariales modernas basadas en Java. Ofrece una amplia gama de características, que incluyen:

- Inyección de dependencias: el marco de inyección de dependencias de Spring permite a los desarrolladores inyectar fácilmente objetos en la aplicación sin tener que crear y administrar manualmente las dependencias.

- Programación orientada a aspectos (AOP): el marco AOP de Spring permite a los desarrolladores agregar fácilmente preocupaciones transversales a sus aplicaciones sin tener que administrar manualmente el código.

- Acceso a datos y gestión de transacciones: Spring proporciona un enfoque coherente para gestionar el acceso a los datos y las transacciones. Es compatible con una amplia variedad de bases de datos y sistemas de gestión de transacciones.

- Mensajería: Spring proporciona un enfoque coherente para la mensajería, incluida la compatibilidad con sistemas de mensajería populares como JMS, AMQP y STOMP.

- Desarrollo web: Spring proporciona un enfoque consistente para el desarrollo web, incluido el soporte para marcos web populares como Struts y JSF.

# Ejemplo
El siguiente ejemplo demuestra cómo usar Spring para crear una aplicación web simple.

Primero, definimos las dependencias que necesitamos en la aplicación:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>4.1.6.RELEASE</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-tx</artifactId>
        <version>4.1.6.RELEASE</version>
    </dependency>
</dependencies>
```

A continuación, creamos una clase de configuración para configurar la aplicación:

```java
@Configuration
@EnableWebMvc
@ComponentScan("com.example.web")
public class WebConfig {

    @Bean
    public ViewResolver viewResolver() {
        InternalResourceViewResolver resolver = new InternalResourceViewResolver();
        resolver.setPrefix("/WEB-INF/views/");
        resolver.setSuffix(".jsp");
        return resolver;
    }
}
```

Finalmente, creamos un controlador para manejar las solicitudes:

```java
@Controller
public class HomeController {

    @RequestMapping("/")
    public String home() {
        return "home";
    }

}
```

# Pros y contras
Las principales ventajas de Spring son su facilidad de uso, extensibilidad y amplia gama de funciones. Proporciona un enfoque coherente para el desarrollo que facilita el mantenimiento y la ampliación de las aplicaciones. Además, su compatibilidad con marcos y bases de datos web populares lo convierte en una buena opción para desarrollar aplicaciones empresariales.

La principal desventaja de Spring es su complejidad. Puede ser difícil de aprender y comprender, y su gran cantidad de características puede dificultar su mantenimiento. Además, su dependencia de la configuración XML puede dificultar la depuración y la resolución de problemas.

# Tecnología relacionada
Spring está estrechamente relacionado con otros marcos de aplicaciones de código abierto, como Apache Struts y Grails. También está relacionado con tecnologías Java EE populares, como JSF y EJB.

# Digresión
Spring se ha convertido en uno de los frameworks de aplicaciones más populares para el desarrollo de Java. Lo utilizan muchas organizaciones grandes, como eBay, LinkedIn y Netflix.

# Otros
Spring es un proyecto de código abierto y se publica bajo la Licencia Apache. Es desarrollado y mantenido activamente por la división SpringSource de VMware, Inc.