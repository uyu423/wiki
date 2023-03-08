---
title: Monitoreo de resorte de arranque con actuador
description: 
published: true
date: 2023-02-07T15:33:16.693Z
tags: 
editor: markdown
dateCreated: 2023-02-07T15:33:14.982Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot Monitoring with Actuator***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-monitoring-with-actuator)
{.links-list}


# Monitoreo de resorte de arranque con actuador

En una aplicación Spring Boot de producción, es importante poder monitorear la aplicación para poder identificar y diagnosticar cualquier problema que pueda surgir. Spring Boot proporciona una serie de funciones listas para usar para ayudar con esto, incluido el actuador.

Actuator es una herramienta que le permite monitorear y administrar su aplicación Spring Boot. Proporciona una serie de puntos finales que le permiten monitorear y administrar su aplicación, sin tener que escribir ningún código.

En este artículo, veremos cómo usar Actuator para monitorear una aplicación Spring Boot. También veremos cómo usar Actuator para crear puntos finales personalizados para exponer información específica de la aplicación.

## Habilitación del actuador

Para usar Actuator, primero debe agregar la dependencia spring-boot-starter-actuator a su proyecto. Esto se puede hacer agregando la siguiente dependencia a su archivo pom.xml:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Alternativamente, si está utilizando Gradle, puede agregar la siguiente dependencia a su archivo build.gradle:

```groovy
dependencies {
    compile('org.springframework.boot:spring-boot-starter-actuator')
}
```

Una vez que haya agregado la dependencia spring-boot-starter-actuator a su proyecto, el actuador se habilitará de manera predeterminada. De forma predeterminada, el Actuador solo será accesible para los usuarios con el rol de 'ADMIN'.

Para cambiar esto, puede agregar la siguiente propiedad a su archivo application.properties:

```properties
management.security.enabled=false
```

Esto deshabilitará la seguridad para los puntos finales del actuador. De manera alternativa, puede agregar la dependencia spring-boot-starter-security a su proyecto para configurar la seguridad de los puntos finales de Actuator.

## Puntos finales del actuador

El actuador expone una serie de puntos finales. Estos puntos finales se pueden usar para monitorear y administrar su aplicación. Los puntos finales se dividen en dos grupos:

* ProductionEndpoints: estos puntos finales están destinados para su uso en producción y brindan información sobre la salud y el estado de su aplicación.
* allEndpoints: estos puntos finales brindan información sobre la salud y el estado de su aplicación, así como información específica de la aplicación.

El grupo allEndpoints incluye todos los ProductionEndpoints, así como cualquier punto de enlace personalizado que haya creado.

En la siguiente tabla, se enumeran los puntos finales de producción proporcionados por el actuador:

| punto final | Descripción |
| --- | --- |
| /eventos de auditoría | Este punto final proporciona información sobre los eventos de la aplicación que se han auditado. |
| /frijoles | Este punto final proporciona información sobre los beans que ha creado el contenedor Spring. |
| /configprops | Este extremo proporciona información sobre las propiedades de configuración que se han establecido para su aplicación. |
| /volcado | Este punto final se puede usar para volcar el estado de su aplicación. Esto es útil para solucionar problemas. |
| /env | Este punto final proporciona información sobre las variables de entorno que se han establecido para su aplicación. |
| /ruta aérea | Este punto final proporciona información sobre las migraciones de bases de datos que Flyway ha aplicado. |
| /salud | Este extremo proporciona información sobre el estado de su aplicación. |
| /info | Este punto final proporciona información específica de la aplicación. |
| /liquibase | Este punto final proporciona información sobre las migraciones de bases de datos que ha aplicado Liquibase. |
| /registradores | Este punto final se puede utilizar para configurar el nivel de registro de su aplicación. |
| /métricas | Este punto final proporciona información sobre las métricas que se recopilaron para su aplicación. |
| /asignaciones | Este punto final proporciona información sobre las rutas @RequestMapping que se han definido para su aplicación. |
| /apagado | Este punto final se puede utilizar para cerrar su aplicación. |
| /rastreo | Este punto final proporciona información sobre las solicitudes HTTP que se han realizado a su aplicación. |

Para acceder a cualquiera de estos puntos finales, debe agregar el punto final a la ruta de su aplicación. Por ejemplo, si su aplicación se ejecuta en http://localhost:8080, accedería al punto final /health en http://localhost:8080/health.

## Leer puntos finales del actuador

Para leer la información de un punto final de Actuator, puede usar una herramienta como curl, wget o un navegador.

Por ejemplo, para leer el punto final /health, puede usar curl de la siguiente manera:

```
$ curl http://localhost:8080/health
```

Alternativamente, puede usar wget de la siguiente manera:

```
$ wget http://localhost:8080/health
```

Si usa un navegador para acceder al punto final /health, verá el siguiente resultado:

```json
{
    "status": "UP",
    "diskSpace": {
        "status": "UP",
        "total": 499963648,
        "free": 367030272,
        "threshold": 10485760
    },
    "db": {
        "status": "UP",
        "database": "H2",
        "hello": 1
    },
    "redis": {
        "status": "UP"
    }
}
```

El resultado del punto final /health es un documento JSON que contiene información sobre el estado de su aplicación. El campo de estado indica el estado general de su aplicación. Los campos diskSpace, db y redis contienen información sobre el estado de subsistemas específicos.

## Creación de terminales personalizados

Además de los puntos finales integrados, también puede crear puntos finales personalizados. Para hacer esto, debe crear una clase que implemente la interfaz org.springframework.boot.actuate.endpoint.annotation.Endpoint.

Por ejemplo, la siguiente clase define un punto final personalizado que devuelve una lista de usuarios:

```java
@Endpoint(id="users")
public class UserEndpoint {

    private List<User> users;

    @ReadOperation
    public List<User> getUsers() {
        return this.users;
    }

    public void setUsers(List<User> users) {
        this.users = users;
    }

}
```

La anotación @Endpoint se usa para anotar la clase. El atributo id se utiliza para especificar el identificador del punto final. Este es el identificador que se utilizará para acceder al punto final.

El método getUsers() se anota con la anotación @ReadOperation. Esta anotación indica que el método se puede utilizar para leer la información del punto final.

El método setUsers() se anota con la anotación @WriteOperation. Esta anotación indica que el método se puede utilizar para escribir la información en el punto final.

Para registrar el punto final, debe agregar la anotación @Component a la clase. Por ejemplo:

```java
@Component
@Endpoint(id="users")
public class UserEndpoint {
    // ...
}
```

Como alternativa, puede registrar el punto final agregándolo al contexto de la aplicación. Por ejemplo:

```java
@Configuration
public class EndpointConfig {

    @Bean
    public UserEndpoint userEndpoint() {
        return new UserEndpoint();
    }

}
```

Una vez que haya registrado el punto final, puede acceder a él agregando el identificador del punto final a la ruta de su aplicación. Por ejemplo, si su aplicación se ejecuta en http://localhost:8080, puede acceder al extremo de /users en http://localhost:8080/users.

## Conclusión

En este artículo, hemos visto cómo usar Actuator para monitorear una aplicación Spring Boot. También hemos visto cómo usar Actuator para crear puntos finales personalizados para exponer información específica de la aplicación.