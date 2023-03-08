---
title: 050: Integración con un servicio de notificación mediante Spring Boot (Twilio, Slack)
description: 
published: true
date: 2023-02-04T16:32:26.913Z
tags: 
editor: markdown
dateCreated: 2023-02-04T16:32:25.327Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [050: Integrating with a notification service using Spring Boot (Twilio, Slack)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/050-integrating-with-a-notification-service-using-spring-boot-twilio-slack)
{.links-list}


# 050: Integración con un servicio de notificaciones usando Spring Boot (Twilio, Slack)

En esta publicación, veremos cómo integrarse con un servicio de notificación usando Spring Boot. Usaremos Twilio y Slack para nuestros ejemplos, pero los mismos principios se pueden aplicar a otros servicios de notificación.

## Configuración de su entorno

Antes de comenzar, deberá configurar su entorno. Para esta publicación, asumiremos que está utilizando un entorno de desarrollo Java.

Primero, deberá instalar Spring Boot CLI. Puede encontrar instrucciones para hacerlo aquí: https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started-installing-spring-boot.html

Una vez que haya instalado Spring Boot CLI, deberá crear un nuevo proyecto. Puede hacerlo ejecutando el siguiente comando:

```
$ spring init -d=web,jpa,thymeleaf my-project
```

Esto creará un nuevo proyecto Spring Boot con las dependencias web, JPA y Thymeleaf.

A continuación, deberá agregar las siguientes dependencias a su proyecto:

```
$ cd my-project
$ ./mvnw install

...

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-thymeleaf</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>com.twilio.sdk</groupId>
        <artifactId>twilio-java-sdk</artifactId>
        <version>7.0.0</version>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

## Configuración de Twilio

Ahora que tenemos nuestro proyecto configurado, podemos comenzar a configurar Twilio. Lo primero que deberá hacer es registrarse para obtener una cuenta de Twilio. Puedes hacerlo aquí: https://www.twilio.com/try-twilio

Una vez que tenga una cuenta, deberá crear un nuevo proyecto. Puede hacerlo haciendo clic en el botón "Crear un nuevo proyecto" en el tablero.

Asigne un nombre a su proyecto y haga clic en "Crear proyecto".

Una vez que haya creado su proyecto, deberá generar una nueva clave de API. Puede hacerlo haciendo clic en el enlace "Claves API" en el lado izquierdo del tablero.

Haga clic en el botón "Crear una nueva clave API" y asigne un nombre a su clave.

Una vez que haya creado su clave, deberá copiarla en su portapapeles. Lo usaremos en un momento.

## Configuración de la holgura

Ahora que tenemos nuestra cuenta de Twilio configurada, podemos comenzar a configurar Slack. Lo primero que deberá hacer es registrarse para obtener una cuenta de Slack. Puedes hacerlo aquí: https://slack.com/

Una vez que tenga una cuenta, deberá crear un nuevo canal. Puede hacerlo haciendo clic en el enlace "Canales" en el lado izquierdo del tablero.

Asigne un nombre a su canal y haga clic en "Crear canal".

Una vez que haya creado su canal, deberá invitar a los miembros de su equipo. Puede hacerlo haciendo clic en el enlace "Invitar a personas" en el lado derecho del canal.

Ingrese las direcciones de correo electrónico de las personas que desea invitar y haga clic en "Enviar invitaciones".

## Envío de notificaciones

Ahora que tenemos nuestro entorno configurado, podemos comenzar a enviar notificaciones.

Para enviar una notificación mediante Twilio, deberá utilizar el siguiente código:

```java
// Replace these with your own values
String accountSid = "YOUR_TWILIO_ACCOUNT_SID";
String authToken = "YOUR_TWILIO_AUTH_TOKEN";

// Initialize the Twilio client
Twilio.init(accountSid, authToken);

// Create the notification
Notification notification = Notification.creator(
        new PhoneNumber("+11234567890"), // to
        new PhoneNumber("+10987654321"), // from
        "Hello world!" // body
).create();
```

Para enviar una notificación mediante Slack, deberá utilizar el siguiente código:

```java
// Replace these with your own values
String channelId = "YOUR_SLACK_CHANNEL_ID";
String apiKey = "YOUR_SLACK_API_KEY";

// Initialize the Slack client
Slack slack = Slack.getInstance(apiKey);

// Create the notification
Notification notification = slack.notify(
        channelId, // channel
        "Hello world!" // message
);
```

## Conclusión

En esta publicación, hemos visto cómo integrarse con un servicio de notificación usando Spring Boot. Hemos usado Twilio y Slack para nuestros ejemplos, pero los mismos principios se pueden aplicar a otros servicios de notificación.