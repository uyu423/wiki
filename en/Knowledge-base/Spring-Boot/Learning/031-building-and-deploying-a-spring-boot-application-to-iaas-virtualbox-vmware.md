---
title: 031: Building and deploying a Spring Boot application to IaaS (Virtualbox, VMware)
description: 
published: true
date: 2023-02-03T23:32:15.346Z
tags: 
editor: markdown
dateCreated: 2023-02-03T23:32:10.310Z
---

- [031: Creación e implementación de una aplicación Spring Boot para IaaS (Virtualbox, VMware)***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/031-building-and-deploying-a-spring-boot-application-to-iaas-virtualbox-vmware)
{.links-list}
- [031：构建 Spring Boot 应用程序并将其部署到 IaaS（Virtualbox、VMware）***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/031-building-and-deploying-a-spring-boot-application-to-iaas-virtualbox-vmware)
{.links-list}
- [031: IaaS(Virtualbox, VMware)에 Spring Boot 애플리케이션 구축 및 배포***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/031-building-and-deploying-a-spring-boot-application-to-iaas-virtualbox-vmware)
{.links-list}


# 031: Building and deploying a Spring Boot application to IaaS (Virtualbox, VMware)

In this post, we'll learn how to build and deploy a Spring Boot application to IaaS (Virtualbox, VMware).

We'll start by creating a new Spring Boot project using the Spring Initializr. For our project, we'll need to select the Web and Thymeleaf dependencies.

Once our project is created, we'll add a simple controller that will render a Thymeleaf template.

@Controller public class HomeController { @RequestMapping("/") public String home(Model model) { model.addAttribute("message", "Hello, World!"); return "home"; } }

Our template will just display the message that we passed from the controller.

<html> <head> <title>Hello, World!</title> </head> <body> <p th:text="${message}"></p> </body> </html>

Now that our application is complete, we'll need to package it as a JAR file. We can do this by running the following command from the project's root directory:

./mvnw package

This will create a JAR file in the target/ directory.

We can now deploy this JAR file to our IaaS provider. We'll need to create a new VM and install the Java Runtime Environment (JRE).

Once our VM is up and running, we can SCP the JAR file over to the VM and run it using the following command:

java -jar spring-boot-app.jar

Our application will now be accessible at http://{vm-ip-address}:8080.

That's all there is to it! In this post, we learned how to build and deploy a Spring Boot application to IaaS (Virtualbox, VMware).