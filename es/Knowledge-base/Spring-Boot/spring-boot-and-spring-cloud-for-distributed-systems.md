---
title: Spring Boot y Spring Cloud para sistemas distribuidos
description: 
published: true
date: 2023-02-03T19:17:27.803Z
tags: 
editor: markdown
dateCreated: 2023-02-03T19:17:22.855Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot and Spring Cloud for Distributed Systems***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-spring-cloud-for-distributed-systems)
{.links-list}


# Spring Boot y Spring Cloud para Sistemas Distribuidos

La nube se ha convertido en la nueva normalidad para muchas empresas y organizaciones. Es rentable, escalable y proporciona una serie de otros beneficios. Pero también puede ser complejo, con muchas partes móviles.

Una forma de facilitar el desarrollo de sistemas distribuidos en la nube es usar Spring Boot y Spring Cloud. En este artículo, veremos qué son estos dos marcos y cómo se pueden usar juntos.

## ¿Qué es Spring Boot?

Spring Boot es un marco que lo ayuda a crear aplicaciones basadas en Spring independientes y de grado de producción. Está diseñado para ponerlo en funcionamiento lo más rápido posible, con una configuración mínima.

Spring Boot viene con una serie de características, que incluyen:

- Servidores integrados que facilitan la implementación de sus aplicaciones
- Soporte para muchas fuentes de datos diferentes
- Una gran cantidad de dependencias iniciales, que se pueden usar para agregar dependencias comunes a su proyecto con un mínimo de configuración
- Configuración automática de Spring beans
- Configuración obstinada pero flexible.

Spring Boot facilita la creación de aplicaciones y servicios basados en Spring. Toma una visión obstinada de la plataforma Spring y lo pone en funcionamiento con un mínimo de configuración.

## ¿Qué es Nube de Primavera?

Spring Cloud es un conjunto de herramientas para crear aplicaciones nativas de la nube. Proporciona una serie de características, que incluyen:

- Service Discovery: un mecanismo para registrar y descubrir servicios
- Gestión de la configuración: un servicio de configuración distribuida
- Enrutamiento: un servicio de proxy inverso para enrutar solicitudes a servicios de back-end
- Equilibrio de carga: una biblioteca de equilibrio de carga del lado del cliente
- Circuit Breakers: una biblioteca para la gestión de fallas en sistemas distribuidos

Spring Cloud lo ayuda a crear aplicaciones nativas de la nube que son escalables, resistentes y se administran solas.

## Usando Spring Boot y Spring Cloud juntos

Spring Boot y Spring Cloud funcionan bien juntos. Spring Boot facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción, y Spring Cloud facilita la creación e implementación de microservicios.

Aquí hay un ejemplo simple de un microservicio creado con Spring Boot y Spring Cloud.

```java
@SpringBootApplication
@EnableDiscoveryClient
public class MyService {
    
    @Autowired
    private DiscoveryClient discoveryClient;
    
    @RequestMapping("/")
    public String home() {
        return "Hello from MyService";
    }
    
    @RequestMapping("/service-instances/{applicationName}")
    public List<ServiceInstance> serviceInstancesByApplicationName(
        @PathVariable String applicationName) {
        return this.discoveryClient.getInstances(applicationName);
    }
}
```

Este microservicio se registra con Spring Cloud DiscoveryClient, lo que permite que otros servicios lo descubran. También expone dos extremos REST: uno para devolver un saludo simple y otro para devolver una lista de ServiceInstances para un nombre de aplicación dado.

Para ejecutar este microservicio, puede usar el complemento Spring Boot Maven:

```
$ mvn spring-boot:run
```

A continuación, puede acceder al microservicio en http://localhost:8080.

## Conclusión

En este artículo, analizamos qué son Spring Boot y Spring Cloud y cómo se pueden usar juntos. También hemos visto un ejemplo simple de un microservicio creado con estos dos marcos.

Si está buscando una manera de simplificar el desarrollo de sistemas distribuidos en la nube, vale la pena echarle un vistazo a Spring Boot y Spring Cloud.