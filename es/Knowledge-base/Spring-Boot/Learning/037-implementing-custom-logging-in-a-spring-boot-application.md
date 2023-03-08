---
title: 037: Implementación de registro personalizado en una aplicación Spring Boot
description: 
published: true
date: 2023-02-04T05:32:25.785Z
tags: 
editor: markdown
dateCreated: 2023-02-04T05:32:24.128Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [037: Implementing custom logging in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/037-implementing-custom-logging-in-a-spring-boot-application)
{.links-list}


# Implementando un registro personalizado en una aplicación Spring Boot

En esta publicación, veremos cómo implementar el registro personalizado en una aplicación Spring Boot. Cubriremos los siguientes temas:

* Configuración de Log4j2 para una aplicación Spring Boot
* Creación de un agregador Log4j2 personalizado
* Registro de eventos en una base de datos mediante un agregador personalizado

## Configuración de Log4j2 para una aplicación Spring Boot

Log4j2 es una biblioteca de registro popular para aplicaciones Java. Spring Boot proporciona soporte para Log4j2 listo para usar. Para configurar Log4j2 para una aplicación Spring Boot, necesitamos agregar un archivo de configuración de Log4j2 a la ruta de clase. El archivo de configuración Log4j2 debe llamarse log4j2.xml o log4j2.yaml.

Aquí hay un archivo de configuración Log4j2 simple que registrará todos los mensajes en la consola:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="warn">
  <Appenders>
    <Console name="Console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
  </Appenders>
  <Loggers>
    <Root level="info">
      <AppenderRef ref="Console"/>
    </Root>
  </Loggers>
</Configuration>
```

En el archivo de configuración Log4j2, debemos especificar los appenders que queremos usar. En este ejemplo, usamos un agregador de consola que registrará todos los mensajes en la consola. También necesitamos especificar los registradores que queremos usar. En este ejemplo, usamos el registrador raíz y hacemos referencia al agregador de consola que definimos anteriormente.

## Creando un agregador Log4j2 personalizado

Para registrar eventos en una base de datos, necesitamos crear un agregador Log4j2 personalizado. Un agregador Log4j2 es un complemento que nos permite especificar dónde queremos que se escriban nuestros registros. En nuestro caso, queremos escribir nuestros registros en una base de datos.

Nuestro agregador personalizado deberá implementar la siguiente interfaz:

```java
public interface Appender {
 
    void start();
 
    void stop();
 
    boolean isStarted();
 
    void append(LogEvent event);
 
    Layout getLayout();
 
    void setLayout(Layout layout);
 
    ErrorHandler getErrorHandler();
 
    void setErrorHandler(ErrorHandler errorHandler);
 
    Name getName();
 
    boolean ignoresThrowable();
}
```

Podemos comenzar creando una implementación básica de nuestro agregador personalizado:

```java
public class DatabaseAppender implements Appender {
 
    @Override
    public void start() {
 
    }
 
    @Override
    public void stop() {
 
    }
 
    @Override
    public boolean isStarted() {
        return false;
    }
 
    @Override
    public void append(LogEvent event) {
 
    }
 
    @Override
    public Layout getLayout() {
        return null;
    }
 
    @Override
    public void setLayout(Layout layout) {
 
    }
 
    @Override
    public ErrorHandler getErrorHandler() {
        return null;
    }
 
    @Override
    public void setErrorHandler(ErrorHandler errorHandler) {
 
    }
 
    @Override
    public Name getName() {
        return null;
    }
 
    @Override
    public boolean ignoresThrowable() {
        return false;
    }
}
```

En el método start(), necesitamos inicializar nuestra conexión a la base de datos. En el método stop(), necesitamos cerrar nuestra conexión a la base de datos. En el método append(), necesitamos insertar nuestro evento de registro en la base de datos.

## Registro de eventos en una base de datos mediante un agregador personalizado

Ahora que tenemos nuestro agregador personalizado, debemos configurar Log4j2 para usarlo. Podemos hacer esto agregando lo siguiente a nuestro archivo de configuración Log4j2:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="warn">
  <Appenders>
    <Console name="Console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
 
    <DatabaseAppender name="DatabaseAppender">
      <ConnectionString>jdbc:mysql://localhost:3306/test</ConnectionString>
      <DriverClassName>com.mysql.jdbc.Driver</DriverClassName>
      <UserName>root</UserName>
      <Password>root</Password>
    </DatabaseAppender>
  </Appenders>
 
  <Loggers>
    <Root level="info">
      <AppenderRef ref="Console"/>
      <AppenderRef ref="DatabaseAppender"/>
    </Root>
  </Loggers>
</Configuration>
```

En el archivo de configuración de Log4j2, agregamos un elemento <DatabaseAppender>. Este elemento tiene algunos atributos que debemos configurar:

* ConnectionString: La cadena de conexión JDBC para nuestra base de datos
* DriverClassName: el nombre de la clase de controlador JDBC
* UserName: El nombre de usuario de la base de datos
* Contraseña: La contraseña de la base de datos

También hemos agregado un elemento <AppenderRef> al registrador raíz. Este elemento hace referencia a nuestro DatabaseAppender.

Ahora que tenemos nuestro agregador personalizado configurado, podemos usarlo para registrar eventos en nuestra base de datos.