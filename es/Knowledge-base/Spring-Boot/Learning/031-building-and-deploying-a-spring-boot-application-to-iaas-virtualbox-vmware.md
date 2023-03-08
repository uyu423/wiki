---
title: 031: Creación e implementación de una aplicación Spring Boot para IaaS (Virtualbox, VMware)
description: 
published: true
date: 2023-02-03T23:32:11.908Z
tags: 
editor: markdown
dateCreated: 2023-02-03T23:32:10.309Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [031: Building and deploying a Spring Boot application to IaaS (Virtualbox, VMware)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/031-building-and-deploying-a-spring-boot-application-to-iaas-virtualbox-vmware)
{.links-list}


# 031: Construcción e implementación de una aplicación Spring Boot para IaaS (Virtualbox, VMware)

En esta publicación, aprenderemos cómo crear e implementar una aplicación Spring Boot en IaaS (Virtualbox, VMware).

Comenzaremos creando un nuevo proyecto Spring Boot utilizando Spring Initializr. Para nuestro proyecto, necesitaremos seleccionar las dependencias Web y Thymeleaf.

Una vez que se crea nuestro proyecto, agregaremos un controlador simple que generará una plantilla de Thymeleaf.

@Controller public class HomeController { @RequestMapping("/") public String home(modelo modelo) { model.addAttribute("mensaje", "¡Hola, mundo!"); volver a casa"; } }

Nuestra plantilla solo mostrará el mensaje que pasamos desde el controlador.

<html> <head> <title>¡Hola, mundo!</title> </head> <body> <p th:text="${mensaje}"></p> </body> </html>

Ahora que nuestra aplicación está completa, necesitaremos empaquetarla como un archivo JAR. Podemos hacer esto ejecutando el siguiente comando desde el directorio raíz del proyecto:

Paquete ./mvnw

Esto creará un archivo JAR en el directorio target/.

Ahora podemos implementar este archivo JAR en nuestro proveedor de IaaS. Tendremos que crear una nueva máquina virtual e instalar Java Runtime Environment (JRE).

Una vez que nuestra VM esté en funcionamiento, podemos SCP el archivo JAR en la VM y ejecutarlo con el siguiente comando:

java -jar spring-boot-aplicación.jar

Ahora se podrá acceder a nuestra aplicación en http://{vm-ip-address}:8080.

¡Eso es todo al respecto! En esta publicación, aprendimos cómo crear e implementar una aplicación Spring Boot en IaaS (Virtualbox, VMware).