---
title: El patrón Decorator en el desarrollo de Spring Boot
description: 
published: true
date: 2023-02-08T16:32:25.905Z
tags: 
editor: markdown
dateCreated: 2023-02-08T16:32:24.341Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [The Decorator Pattern in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-decorator-pattern-in-spring-boot-development)
{.links-list}


# El patrón Decorator en el desarrollo de Spring Boot

Decorator Pattern es un patrón de diseño de software que permite la modificación de objetos existentes sin cambiar su funcionalidad principal. Esto se logra envolviendo el objeto original con un objeto decorador que contiene la funcionalidad deseada.

En Spring Boot, el patrón Decorator se puede usar para agregar dinámicamente nuevas funciones a beans existentes sin cambiar su código. Esto se hace envolviendo el bean original con un bean decorador que contiene la funcionalidad deseada.

Por ejemplo, digamos que tenemos un bean simple que contiene un mensaje:

```java
public class MessageBean {
  
  private String message;
  
  public MessageBean(String message) {
    this.message = message;
  }
  
  public String getMessage() {
    return message;
  }
}
```

Podemos usar el patrón Decorator para agregar dinámicamente una nueva funcionalidad a este bean sin cambiar su código. Por ejemplo, podemos crear un bean decorador que agregue una marca de tiempo al mensaje:

```java
public class TimestampDecorator implements MessageBean {
  
  private MessageBean messageBean;
  
  public TimestampDecorator(MessageBean messageBean) {
    this.messageBean = messageBean;
  }
  
  @Override
  public String getMessage() {
    return messageBean.getMessage() + " - " + new Date();
  }
}
```

Ahora, cuando inyectamos MessageBean en nuestro código, podemos especificar que queremos usar TimestampDecorator:

```java
@Autowired
@Qualifier("timestampDecorator")
private MessageBean messageBean;
```

Esto agregará la marca de tiempo actual al mensaje cuando llamemos al método getMessage():

```java
messageBean.getMessage(); // "Hello World! - Thu Jan 01 00:00:00 EST 1970"
```

Decorator Pattern es una forma útil de agregar dinámicamente nuevas funciones a beans existentes sin cambiar su código. Esto se puede usar para agregar marcas de tiempo, registro, seguridad o cualquier otra funcionalidad deseada.