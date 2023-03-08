---
title: 033: Implementación del envío de correo electrónico en una aplicación Spring Boot
description: 
published: true
date: 2023-02-04T01:32:45.725Z
tags: 
editor: markdown
dateCreated: 2023-02-04T01:32:44.103Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [033: Implementing email sending in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/033-implementing-email-sending-in-a-spring-boot-application)
{.links-list}


El envío de correos electrónicos es una parte fundamental de muchas aplicaciones. Se utiliza para todo, desde notificar a los usuarios sobre eventos del sistema hasta enviar restablecimientos de contraseña y correos electrónicos de confirmación.

En esta publicación, exploraremos cómo agregar capacidades de correo electrónico a una aplicación Spring Boot. Cubriremos los siguientes temas:

* Configuración del envío de correo electrónico en Spring Boot
* Envío de correos electrónicos simples
* Envío de correos electrónicos HTML
* Envío de archivos adjuntos

## Configuración del envío de correo electrónico en Spring Boot

Spring Boot facilita la configuración del envío de correo electrónico en su aplicación. Todo lo que necesita es agregar la dependencia correcta y configurar algunas propiedades en su archivo application.properties.

Lo primero que debe hacer es agregar la dependencia spring-boot-starter-mail a su proyecto. Este iniciador extraerá todas las dependencias que necesita para comenzar a enviar correos electrónicos en Spring Boot.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
</dependency>
```

Una vez que tenga la dependencia en su lugar, puede configurar las siguientes propiedades en su archivo application.properties:

* spring.mail.host= # host del servidor SMTP. Por ejemplo, smtp.gmail.com.
* spring.mail.port= # puerto del servidor SMTP. Por ejemplo, 587.
* spring.mail.username= # Nombre de usuario de la cuenta a usar para conectarse al servidor SMTP.
* spring.mail.password= # Contraseña de la cuenta a usar para conectarse al servidor SMTP.
* spring.mail.protocol= # Protocolo a usar cuando se conecta al servidor SMTP. Por ejemplo, SMTP.
* spring.mail.properties.mail.smtp.auth=true # Indica si usar la autenticación al conectarse al servidor SMTP.
* spring.mail.properties.mail.smtp.starttls.enable=true # Si usar STARTTLS al conectarse al servidor SMTP.

## Envío de correos electrónicos simples

Ahora que tiene el correo electrónico configurado en su aplicación Spring Boot, echemos un vistazo a cómo enviar un correo electrónico simple.

Lo primero que necesita es una instancia de la interfaz JavaMailSender. Esta interfaz proporciona métodos para enviar correos electrónicos. Puede inyectar esta interfaz en su aplicación Spring Boot usando la anotación @Autowired.

```java
@Autowired
private JavaMailSender javaMailSender;
```

Una vez que tenga una instancia de la interfaz JavaMailSender, puede usar el siguiente código para enviar un correo electrónico simple:

```java
javaMailSender.send(new MimeMessagePreparator() {
    public void prepare(MimeMessage mimeMessage) throws Exception {
        MimeMessageHelper messageHelper = new MimeMessageHelper(mimeMessage, true);
        messageHelper.setFrom("sender@example.com");
        messageHelper.setTo("receiver@example.com");
        messageHelper.setSubject("Email subject");
        messageHelper.setText("Email body");
    }
});
```

En el código anterior, usamos el método send() de la interfaz JavaMailSender para enviar un correo electrónico. También usamos MimeMessagePreparator para preparar el mensaje de correo electrónico.

MimeMessagePreparator es una interfaz que le permite preparar una instancia de MimeMessage antes de enviarla. Esto es útil si necesita hacer cosas como establecer encabezados o archivos adjuntos en el correo electrónico.

En el código anterior, usamos la clase MimeMessageHelper para ayudarnos a preparar el mensaje de correo electrónico. La clase MimeMessageHelper proporciona métodos convenientes para configurar encabezados de correo electrónico y contenido del cuerpo comunes.

Una vez que se prepara el mensaje de correo electrónico, se pasa al método send() de la interfaz JavaMailSender y se envía el correo electrónico.

## Envío de correos electrónicos HTML

Además de enviar correos electrónicos de texto simple, también puede enviar correos electrónicos HTML usando Spring Boot. Para hacer esto, solo necesita configurar el mensaje de texto del correo electrónico para que sea una cadena HTML.

```java
javaMailSender.send(new MimeMessagePreparator() {
    public void prepare(MimeMessage mimeMessage) throws Exception {
        MimeMessageHelper messageHelper = new MimeMessageHelper(mimeMessage, true);
        messageHelper.setFrom("sender@example.com");
        messageHelper.setTo("receiver@example.com");
        messageHelper.setSubject("Email subject");
        messageHelper.setText("<p>Email body</p>", true);
    }
});
```

En el código anterior, estamos configurando el mensaje de texto del correo electrónico para que sea una cadena HTML. También estamos configurando el segundo parámetro del método setText() en verdadero. Esto le dice a MimeMessageHelper que el mensaje de texto es HTML y debe representarse como tal.

## Envío de archivos adjuntos

También puede enviar archivos adjuntos con sus mensajes de correo electrónico usando Spring Boot. Para hacer esto, solo necesita usar el método addAttachment() de la clase MimeMessageHelper.

```java
javaMailSender.send(new MimeMessagePreparator() {
    public void prepare(MimeMessage mimeMessage) throws Exception {
        MimeMessageHelper messageHelper = new MimeMessageHelper(mimeMessage, true);
        messageHelper.setFrom("sender@example.com");
        messageHelper.setTo("receiver@example.com");
        messageHelper.setSubject("Email subject");
        messageHelper.setText("Email body");
        messageHelper.addAttachment("attachment.txt", new File("attachment.txt"));
    }
});
```

En el código anterior, usamos el método addAttachment() para agregar un archivo adjunto al mensaje de correo electrónico. El primer parámetro es el nombre del archivo adjunto y el segundo parámetro es el archivo que se adjuntará.

Puede llamar al método addAttachment() varias veces para agregar varios archivos adjuntos a un mensaje de correo electrónico.

## Conclusión

En esta publicación, hemos visto cómo agregar capacidades de correo electrónico a una aplicación Spring Boot. Hemos cubierto los siguientes temas:

* Configuración del envío de correo electrónico en Spring Boot
* Envío de correos electrónicos simples
* Envío de correos electrónicos HTML
* Envío de archivos adjuntos

Con el conocimiento que ha adquirido en esta publicación, debería poder agregar capacidades de correo electrónico a cualquier aplicación Spring Boot.