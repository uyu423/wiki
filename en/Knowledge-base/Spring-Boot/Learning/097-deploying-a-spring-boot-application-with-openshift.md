---
title: 097: Deploying a Spring Boot Application with OpenShift
description: 
published: true
date: 2023-02-04T18:17:20.245Z
tags: 
editor: markdown
dateCreated: 2023-02-04T18:17:18.461Z
---

- [097: Implementación de una aplicación Spring Boot con OpenShift***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/097-deploying-a-spring-boot-application-with-openshift)
{.links-list}
- [097：使用 OpenShift 部署 Spring Boot 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/097-deploying-a-spring-boot-application-with-openshift)
{.links-list}
- [097: OpenShift로 스프링 부트 애플리케이션 배포***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/097-deploying-a-spring-boot-application-with-openshift)
{.links-list}


## Introduction

OpenShift is a Platform as a Service (PaaS) product from Red Hat. It is an on-premise application platform that allows developers to quickly develop, host, and scale applications in a cloud environment.

OpenShift is based on top of Kubernetes and provides a set of tools to help developers with application deployment, management, and scaling.

In this post, we will learn how to deploy a Spring Boot application on OpenShift. We will also learn how to manage and scale the application using OpenShift tools.

## Prerequisites

Before we start, there are a few things that we need to have in place:

- An OpenShift account. If you don't have one, you can sign up for a free trial [here](https://www.openshift.com/pricing/index.html).
- A Spring Boot application. If you don't have one, you can create a simple one using the [Spring Initializr](https://start.spring.io/).
- The [oc](https://docs.openshift.com/container-platform/3.11/cli_reference/get_started_cli.html#installing-the-oc-command-line-interface) command line interface for OpenShift.

## Deploying the Application

We can deploy our Spring Boot application on OpenShift in two ways: using the OpenShift web console or using the oc command line interface.

### Deploying using the OpenShift Web Console

1. Log in to the OpenShift web console and click on the "Create Project" button.

2. Enter a name for the project and click on the "Create" button.

3. In the "Add to Project" page, select the "Deploy Image" option and click on the "Select Image" button.

4. In the "Image Name" field, enter the name of the Spring Boot application image. If the image is not in the OpenShift registry, you can enter the full URL of the image.

5. In the "Image Configuration" section, specify the name of the application, the port that the application will be running on, and the path to the application's jar file.

6. Click on the "Deploy" button.

7. In the "Overview" page, you should see the application running. Click on the application name to go to the application's page.

8. In the application page, you will see the application's URL. Click on the URL to open the application in a new tab.

### Deploying using the oc Command Line Interface

1. Log in to the OpenShift cluster using the oc login command.

2. Create a new project using the oc new-project command.

3. Deploy the application using the oc new-app command. Specify the name of the application, the port that the application will be running on, and the path to the application's jar file.

4. In the "Overview" page, you should see the application running. Click on the application name to go to the application's page.

5. In the application page, you will see the application's URL. Click on the URL to open the application in a new tab.

## Managing the Application

Once the application is deployed, we can manage and scale it using the OpenShift web console or the oc command line interface.

### Managing using the OpenShift Web Console

1. In the OpenShift web console, click on the "Applications" menu and select the "Deployments" option.

2. In the "Deployments" page, you will see a list of all the deployments in the project. Click on the name of the deployment to go to the deployment's page.

3. In the deployment page, you will see the deployment's details, such as the number of replicas, the deployment strategy, and the rollout history.

4. To scale the deployment, click on the "Scale" button and enter the desired number of replicas.

5. To trigger a new rollout, click on the "Rollout" button.

6. To delete the deployment, click on the "Delete" button.

### Managing using the oc Command Line Interface

1. Log in to the OpenShift cluster using the oc login command.

2. To list all the deployments in the project, use the oc get deployments command.

3. To get the details of a deployment, use the oc describe deployment command.

4. To scale a deployment, use the oc scale deployment command.

5. To trigger a new rollout, use the oc rollout latest command.

6. To delete a deployment, use the oc delete deployment command.

## Conclusion

In this post, we learned how to deploy a Spring Boot application on OpenShift. We also learned how to manage and scale the application using OpenShift tools.