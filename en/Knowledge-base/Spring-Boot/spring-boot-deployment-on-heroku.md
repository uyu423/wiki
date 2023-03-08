---
title: Spring Boot Deployment on Heroku
description: 
published: true
date: 2023-02-07T12:32:35.877Z
tags: 
editor: markdown
dateCreated: 2023-02-07T12:32:29.659Z
---

- [Implementación de Spring Boot en Heroku***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-deployment-on-heroku)
{.links-list}
- [Heroku 上的 Spring Boot 部署***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-deployment-on-heroku)
{.links-list}
- [Heroku에 스프링 부트 배포***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-deployment-on-heroku)
{.links-list}


# Spring Boot Deployment on Heroku

Heroku is a cloud platform as a service (PaaS) that supports several programming languages. One of these languages is Java. In this article, we will discuss how to deploy a Spring Boot application on Heroku.

## What is Spring Boot?

Spring Boot is a Java-based framework used to create microservices. It is developed by Pivotal Team and is a free and open-source project.

## What is Heroku?

Heroku is a cloud platform as a service (PaaS) that supports several programming languages.

Heroku is a Platform as a Service (PaaS) that allows developers to deploy, manage, and scale their applications. Heroku is simple and easy to use, and it offers a free plan for small applications.

## Prerequisites

Before you begin, you will need the following:

- A Heroku account
- A text editor
- JDK 8 or above
- Maven 3.3.9 or above

## Creating a Spring Boot Application

First, you will need to create a Spring Boot application. You can do this using the Spring Initializr.

Spring Initializr is a web application that allows you to create a Spring Boot application. It will generate a project structure for you and add the required dependencies.

To create a Spring Boot application, go to https://start.spring.io/, and select the following:

- Language: Java
- Spring Boot Version: 2.4.4
- Project: Maven Project
- Packaging: Jar
- Java Version: 8
- Group: com.heroku
- Artifact: demo

Click Generate Project to download the project.

## Creating a Procfile

Procfile is a text file that contains the commands that are executed by the app on startup. The Procfile must be placed in the root directory of your application.

Create a file named Procfile (without any extension) and add the following line to it.

    web:    java -jar target/demo-0.0.1-SNAPSHOT.jar

## Creating a Heroku App

Once you have created the Procfile, you can create a Heroku app.

Login to your Heroku account and click New -> Create new app.

Enter the following information:

- App Name: demo
- Region: Europe

Click Create App.

## Deploying the App to Heroku

Once the app is created, you can deploy the Spring Boot application to Heroku.

Heroku uses Git for deployment, so you will need to push your code to a Heroku Git repository.

First, you will need to add the Heroku Git repository as a remote to your local repository. To do this, run the following command:

    $ heroku git:remote -a demo

Then, you can push your code to the Heroku Git repository using the following command:

    $ git push heroku master

Once the code is pushed, Heroku will build and deploy the application.

You can view the logs using the following command:

    $ heroku logs --tail

## Conclusion

In this article, we have discussed how to deploy a Spring Boot application on Heroku.