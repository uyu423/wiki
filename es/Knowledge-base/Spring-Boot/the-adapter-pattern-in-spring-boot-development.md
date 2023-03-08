---
title: El patrón de adaptador en el desarrollo de Spring Boot
description: 
published: true
date: 2023-02-01T18:18:13.024Z
tags: 
editor: markdown
dateCreated: 2023-02-01T18:18:11.346Z
---

> Este artículo se tradujo automáticamente con la **API de Google Cloud Translation**.
Algunas páginas pueden leerse mejor que el original.{.is-info}

- [The Adapter Pattern in Spring Boot Development***Spanish** version of this document is available*](/es/Knowledge-base/Spring-Boot/the-adapter-pattern-in-spring-boot-development)
{.links-list}



# El patrón de adaptador en el desarrollo de Spring Boot

En el desarrollo de software, el patrón de adaptador es un patrón de diseño de software que permite que un componente de software funcione con otros componentes de software con los que normalmente no puede funcionar. A menudo se utiliza para hacer que los componentes de software existentes funcionen con componentes de software nuevos, o para hacer que los componentes de software nuevos funcionen con componentes de software existentes.

El patrón de adaptador es un tipo de patrón estructural y es uno de los patrones de diseño más utilizados en el desarrollo de software. El patrón de adaptador se utiliza para resolver el problema de las interfaces incompatibles.

En este artículo, veremos cómo usar el patrón de adaptador en el desarrollo de Spring Boot. También veremos algunos ejemplos de código para ilustrar cómo se puede usar el patrón de adaptador en la práctica.

## ¿Qué es el patrón de adaptador?

Como mencionamos anteriormente, el patrón de adaptador es un patrón de diseño de software que permite que un componente de software funcione con otros componentes de software con los que normalmente no puede funcionar.

El patrón adaptador también se conoce como patrón envolvente. El patrón de adaptador se utiliza para resolver el problema de las interfaces incompatibles.

El patrón de adaptador es un tipo de patrón estructural y es uno de los patrones de diseño más utilizados en el desarrollo de software. El patrón de adaptador se utiliza para resolver el problema de las interfaces incompatibles.

Hay dos tipos de patrón de adaptador: patrón de adaptador de clase y patrón de adaptador de objeto.

## Patrón de adaptador de clase

El patrón de adaptador de clase es un tipo de patrón de adaptador que utiliza la herencia para adaptar una clase a otra.

En el patrón de adaptador de clase, la clase adaptadora hereda de la clase adaptada. La clase adaptadora implementa la interfaz de destino y delega los métodos de la interfaz de destino a la clase adaptada.

Aquí hay un ejemplo de cómo se puede usar el patrón de adaptador de clase en Java.

Tenemos una clase llamada `Logger`, que es una clase adaptada. La clase `Logger` tiene un método llamado `log()`.

```java
public class Logger {
   public void log(String message) {
      // log the message
   }
}
```

También tenemos una clase llamada `ConsoleLogger`, que es una clase adaptadora. La clase `ConsoleLogger` hereda de la clase `Logger`. La clase `ConsoleLogger` implementa la interfaz `Logger` y delega el método `log()` a la clase `Logger`.

```java
public class ConsoleLogger extends Logger implements Logger {
   public void log(String message) {
      super.log(message);
   }
}
```

## Patrón de adaptador de objeto

El patrón de adaptador de objeto es un tipo de patrón de adaptador que utiliza la composición para adaptar un objeto a otro.

En el patrón de adaptador de objeto, la clase de adaptador contiene una instancia de la clase adaptada. La clase adaptadora implementa la interfaz de destino y delega los métodos de la interfaz de destino a la clase adaptada.

Aquí hay un ejemplo de cómo se puede usar el patrón de adaptador de objetos en Java.

Tenemos una clase llamada `Logger`, que es una clase adaptada. La clase `Logger` tiene un método llamado `log()`.

```java
public class Logger {
   public void log(String message) {
      // log the message
   }
}
```

También tenemos una clase llamada `ConsoleLogger`, que es una clase adaptadora. La clase `ConsoleLogger` contiene una instancia de la clase `Logger`. La clase `ConsoleLogger` implementa la interfaz `Logger` y delega el método `log()` a la clase `Logger`.

```java
public class ConsoleLogger {
   private Logger logger;

   public ConsoleLogger(Logger logger) {
      this.logger = logger;
   }

   public void log(String message) {
      logger.log(message);
   }
}
```

## ¿Cómo usar el patrón de adaptador en Spring Boot?

En esta sección, veremos cómo usar el patrón de adaptador en el desarrollo de Spring Boot.

Usaremos el patrón de adaptador de clase en nuestros ejemplos.

### Ejemplo 1

En este ejemplo, usaremos el patrón de adaptador para adaptar una clase `Logger` a la clase `ConsoleLogger`.

Primero, necesitamos crear una clase `Logger`.

```java
public class Logger {
   public void log(String message) {
      // log the message
   }
}
```

A continuación, necesitamos crear una clase `ConsoleLogger`. La clase `ConsoleLogger` hereda de la clase `Logger`. La clase `ConsoleLogger` implementa la interfaz `Logger` y delega el método `log()` a la clase `Logger`.

```java
public class ConsoleLogger extends Logger implements Logger {
   public void log(String message) {
      super.log(message);
   }
}
```

Ahora, podemos usar la clase `ConsoleLogger` en nuestra aplicación Spring Boot.

```java
@SpringBootApplication
public class Application {

   public static void main(String[] args) {
      SpringApplication.run(Application.class, args);
   }

   @Bean
   public Logger logger() {
      return new ConsoleLogger();
   }
}
```

En el método `logger()`, estamos creando un bean de tipo `Logger`, que es la clase `ConsoleLogger`.

Ahora, podemos inyectar el bean `Logger` en nuestra aplicación y usarlo para registrar mensajes.

```java
@Component
public class MyComponent {

   private Logger logger;

   @Autowired
   public MyComponent(Logger logger) {
      this.logger = logger;
   }

   public void doSomething() {
      logger.log("Doing something");
   }
}
```

En la clase `MyComponent`, estamos inyectando el bean `Logger` en el campo `logger`. Entonces estamos usando el campo `logger` para registrar un mensaje.

### Ejemplo 2

En este ejemplo, usaremos el patrón de adaptador para adaptar una clase `RestTemplate` a la clase `MyRestTemplate`.

Primero, necesitamos crear una clase `RestTemplate`.

```java
public class RestTemplate {

   public void getForObject(String url, Class responseType) {
      // GET request to the given URL
   }

   public void postForObject(String url, Object request, Class responseType) {
      // POST request to the given URL
   }
}
```

A continuación, necesitamos crear una clase `MyRestTemplate`. La clase `MyRestTemplate` hereda de la clase `RestTemplate`. La clase `MyRestTemplate` implementa la interfaz `RestTemplate` y delega los métodos `getForObject()` y `postForObject()` a la clase `RestTemplate`.

```java
public class MyRestTemplate extends RestTemplate implements RestTemplate {

   public void getForObject(String url, Class responseType) {
      super.getForObject(url, responseType);
   }

   public void postForObject(String url, Object request, Class responseType) {
      super.postForObject(url, request, responseType);
   }
}
```

Ahora, podemos usar la clase `MyRestTemplate` en nuestra aplicación Spring Boot.

```java
@SpringBootApplication
public class Application {

   public static void main(String[] args) {
      SpringApplication.run(Application.class, args);
   }

   @Bean
   public RestTemplate restTemplate() {
      return new MyRestTemplate();
   }
}
```

En el método `restTemplate()`, estamos creando un bean de tipo `RestTemplate`, que es la clase `MyRestTemplate`.

Ahora, podemos inyectar el bean `RestTemplate` en nuestra aplicación y usarlo para realizar solicitudes HTTP.

```java
@Component
public class MyComponent {

   private RestTemplate restTemplate;

   @Autowired
   public MyComponent(RestTemplate restTemplate) {
      this.restTemplate = restTemplate;
   }

   public void doSomething() {
      restTemplate.getForObject("http://example.com", String.class);
   }
}
```

En la clase `MyComponent`, inyectamos el bean `RestTemplate` en el campo `restTemplate`. Entonces estamos usando el campo `restTemplate` para hacer una solicitud GET a la URL `http://example.com`.

## Conclusión

En este artículo, hemos analizado cómo usar el patrón de adaptador en el desarrollo de Spring Boot. También hemos visto algunos ejemplos de código para ilustrar cómo se puede usar el patrón de adaptador en la práctica.