---
title: 097: Implementación de una aplicación Spring Boot con OpenShift
description: 
published: true
date: 2023-02-04T18:17:23.834Z
tags: 
editor: markdown
dateCreated: 2023-02-04T18:17:18.462Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [097: Deploying a Spring Boot Application with OpenShift***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/097-deploying-a-spring-boot-application-with-openshift)
{.links-list}


## Introducción

OpenShift es un producto de plataforma como servicio (PaaS) de Red Hat. Es una plataforma de aplicaciones local que permite a los desarrolladores desarrollar, alojar y escalar rápidamente aplicaciones en un entorno de nube.

OpenShift se basa en la parte superior de Kubernetes y proporciona un conjunto de herramientas para ayudar a los desarrolladores con la implementación, administración y escalado de aplicaciones.

En esta publicación, aprenderemos cómo implementar una aplicación Spring Boot en OpenShift. También aprenderemos a administrar y escalar la aplicación utilizando las herramientas de OpenShift.

## Requisitos previos

Antes de comenzar, hay algunas cosas que debemos tener en su lugar:

- Una cuenta de OpenShift. Si no tiene uno, puede registrarse para obtener una prueba gratuita [aquí] (https://www.openshift.com/pricing/index.html).
- Una aplicación Spring Boot. Si no tiene uno, puede crear uno simple usando [Spring Initializr] (https://start.spring.io/).
- La interfaz de línea de comandos [oc](https://docs.openshift.com/container-platform/3.11/cli_reference/get_started_cli.html# installing-the-oc-command-line-interface) para OpenShift.

## Implementación de la aplicación

Podemos implementar nuestra aplicación Spring Boot en OpenShift de dos maneras: usando la consola web de OpenShift o usando la interfaz de línea de comandos oc.

### Implementación mediante OpenShift Web Console

1. Inicie sesión en la consola web de OpenShift y haga clic en el botón "Crear proyecto".

2. Introduzca un nombre para el proyecto y haga clic en el botón "Crear".

3. En la página "Agregar al proyecto", seleccione la opción "Implementar imagen" y haga clic en el botón "Seleccionar imagen".

4. En el campo "Nombre de la imagen", ingrese el nombre de la imagen de la aplicación Spring Boot. Si la imagen no está en el registro de OpenShift, puede ingresar la URL completa de la imagen.

5. En la sección "Configuración de imagen", especifique el nombre de la aplicación, el puerto en el que se ejecutará la aplicación y la ruta al archivo jar de la aplicación.

6. Haga clic en el botón "Implementar".

7. En la página "Descripción general", debería ver la aplicación ejecutándose. Haga clic en el nombre de la aplicación para ir a la página de la aplicación.

8. En la página de la aplicación, verá la URL de la aplicación. Haga clic en la URL para abrir la aplicación en una nueva pestaña.

### Implementación mediante la interfaz de línea de comandos oc

1. Inicie sesión en el clúster de OpenShift con el comando de inicio de sesión oc.

2. Cree un nuevo proyecto usando el comando oc new-project.

3. Implemente la aplicación mediante el comando oc new-app. Especifique el nombre de la aplicación, el puerto en el que se ejecutará la aplicación y la ruta al archivo jar de la aplicación.

4. En la página "Descripción general", debería ver la aplicación ejecutándose. Haga clic en el nombre de la aplicación para ir a la página de la aplicación.

5. En la página de la aplicación, verá la URL de la aplicación. Haga clic en la URL para abrir la aplicación en una nueva pestaña.

## Administrar la aplicación

Una vez que se implementa la aplicación, podemos administrarla y escalarla mediante la consola web de OpenShift o la interfaz de línea de comandos oc.

### Gestión mediante la consola web de OpenShift

1. En la consola web de OpenShift, haga clic en el menú "Aplicaciones" y seleccione la opción "Implementaciones".

2. En la página "Implementaciones", verá una lista de todas las implementaciones en el proyecto. Haga clic en el nombre de la implementación para ir a la página de la implementación.

3. En la página de implementación, verá los detalles de la implementación, como la cantidad de réplicas, la estrategia de implementación y el historial de implementación.

4. Para escalar la implementación, haga clic en el botón "Escalar" e ingrese el número deseado de réplicas.

5. Para activar una nueva implementación, haga clic en el botón "Lanzamiento".

6. Para eliminar la implementación, haga clic en el botón "Eliminar".

### Gestión mediante la interfaz de línea de comandos oc

1. Inicie sesión en el clúster de OpenShift con el comando de inicio de sesión oc.

2. Para enumerar todas las implementaciones en el proyecto, use el comando oc get deployments.

3. Para obtener los detalles de una implementación, use el comando oc describe deployment.

4. Para escalar una implementación, utilice el comando oc scale deployment.

5. Para activar una nueva implementación, use el último comando oc rollout.

6. Para eliminar una implementación, use el comando oc delete deployment.

## Conclusión

En esta publicación, aprendimos cómo implementar una aplicación Spring Boot en OpenShift. También aprendimos a administrar y escalar la aplicación utilizando las herramientas de OpenShift.