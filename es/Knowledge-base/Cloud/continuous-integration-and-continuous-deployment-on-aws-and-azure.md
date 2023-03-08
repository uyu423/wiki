---
title: Integración continua e implementación continua en AWS y Azure
description: 
published: true
date: 2023-02-04T16:55:55.241Z
tags: 
editor: markdown
dateCreated: 2023-02-04T16:55:49.810Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Continuous Integration and Continuous Deployment on AWS and Azure***English** document is available*](/en/Knowledge-base/Cloud/continuous-integration-and-continuous-deployment-on-aws-and-azure)
{.links-list}


# Integración Continua e Implementación Continua en AWS y Azure

Las plataformas en la nube como AWS y Azure ofrecen muchos beneficios para los desarrolladores, incluida la capacidad de escalar recursos rápidamente y la flexibilidad para usar una variedad de herramientas y lenguajes de programación. Estas plataformas también facilitan la configuración de canalizaciones de integración continua (CI) e implementación continua (CD).

En este artículo, veremos cómo configurar canalizaciones de CI/CD en AWS y Azure. También discutiremos algunos de los beneficios y desafíos de usar estas plataformas para CI/CD.

## ¿Qué es la Integración Continua?

La integración continua (CI) es la práctica de crear y probar automáticamente los cambios de código a medida que se realizan. Esto permite a los desarrolladores detectar y corregir errores rápidamente y ayuda a garantizar que la base del código esté siempre en un estado de implementación.

 Las canalizaciones de CI generalmente se activan mediante confirmaciones de código y, por lo general, incluyen los siguientes pasos:

- El código se construye y prueba automáticamente.
- Se ejecutan pruebas automatizadas para comprobar si hay errores.
- Si pasan las pruebas, el código se implementa en un entorno de prueba.
- Si las pruebas fallan, el código no se implementa y se notifica a los desarrolladores.

## ¿Qué es la implementación continua?

La implementación continua (CD) es la práctica de implementar automáticamente cambios de código en un entorno de producción. Esto permite a los desarrolladores obtener nuevas funciones y correcciones para los usuarios lo más rápido posible.

Las canalizaciones de CD suelen incluir los siguientes pasos:

- El código se construye y prueba automáticamente.
- Si pasan las pruebas, el código se implementa en un entorno de producción.
- Si las pruebas fallan, el código no se implementa y se notifica a los desarrolladores.

## Configuración de una canalización de CI/CD en AWS

AWS ofrece una serie de servicios que se pueden utilizar para configurar canalizaciones de CI/CD. En esta sección, veremos cómo configurar una canalización de CI/CD simple con AWS CodePipeline y AWS CodeBuild.

### Requisitos previos

Antes de comenzar, necesitará lo siguiente:

- Una cuenta de AWS
- Una cuenta de GitHub
- Un repositorio de código en GitHub

### Configuración de AWS CodePipeline

AWS CodePipeline es un servicio que se puede utilizar para automatizar el proceso de creación, prueba e implementación de cambios de código.

Para configurar una canalización de CI mediante CodePipeline, deberá crear una nueva canalización de CodePipeline. Para hacer esto, inicie sesión en la consola de AWS y navegue hasta el servicio de CodePipeline.

Haga clic en el botón "Crear tubería" para comenzar.

En la página "Seleccionar configuración de canalización", asigne un nombre a su canalización y elija una región. Luego, haga clic en el botón "Siguiente".

En la página "Agregar fuente", seleccione "GitHub" como proveedor de fuente. Luego, elija el repositorio y la rama que desea usar para su canalización. Finalmente, haga clic en el botón "Siguiente".

En la página "Agregar etapa de compilación", seleccione "AWS CodeBuild" como proveedor de compilación. Luego, elija un nombre para su etapa de construcción y haga clic en el botón "Siguiente".

En la página "Configurar etapa de compilación", seleccione el sistema operativo "Linux, Ubuntu" y el tiempo de ejecución "Estándar". Luego, elija la imagen "aws/codebuild/standard:4.0".

En la sección "EnvironmentVariables", agregue las siguientes variables de entorno:

- "Nombre": "NOMBRE_REPOSITORIO"
- "Valor": "Tu nombre de repositorio de GitHub"

En la sección "BuildSpec", ingrese los siguientes comandos de compilación:

- "versión: 0.2"
- "etapas:"
- "pre_construir:"
- "comandos:"
- "echo Iniciando sesión en GitHub..."
- "${{git-credencial}} relleno"
- "construir:"
- "comandos:"
- "Echo Build comenzó el `fecha`"
- "Echo Sitio de construcción..."
- "hugo"
- "post_construcción:"
- "comandos:"
- "construcción de eco completada en `fecha`"

Haga clic en el botón "Guardar proyecto de compilación" para guardar su proyecto de compilación.

En la página "Agregar etapa de implementación", seleccione "AWS CodeDeploy" como proveedor de implementación. Luego, elija un nombre para su etapa de implementación y haga clic en el botón "Siguiente".

En la página "Configurar etapa de implementación", seleccione el tipo de instancia "EC2/local" y el tipo de implementación "Predeterminado". Luego, ingrese la siguiente configuración de implementación:

- "Nombre de la aplicación": "Su nombre de repositorio de GitHub"
- "Nombre del grupo de implementación": "Su nombre de repositorio de GitHub-implementación"
- "ARN del rol de servicio": "arn:aws:iam::aws:policy/service-role/AWSCodeDeployRole"

Haga clic en el botón "Guardar grupo de implementación" para guardar su grupo de implementación.

En la página "Revisar", revise la configuración de su canalización y luego haga clic en el botón "Crear canalización".

Su canalización de CI ahora está lista para usar. Cada vez que realice cambios en el código de su repositorio de GitHub, CodePipeline compilará e implementará automáticamente su código.

## Configuración de una canalización de CI/CD en Azure

Azure ofrece una serie de servicios que se pueden usar para configurar canalizaciones de CI/CD. En esta sección, veremos cómo configurar una canalización de CI/CD simple mediante Azure DevOps y Azure Pipelines.

### Requisitos previos

Antes de comenzar, necesitará lo siguiente:

- Una cuenta azul
- Una cuenta de GitHub
- Un repositorio de código en GitHub

### Configuración de Azure DevOps

Azure DevOps es un servicio que se puede usar para automatizar el proceso de creación, prueba e implementación de cambios de código.

Para configurar una canalización de CI con Azure DevOps, deberá crear un nuevo proyecto de Azure DevOps. Para hacer esto, inicie sesión en Azure Portal y navegue hasta el servicio Azure DevOps.

Haga clic en el botón "Nuevo proyecto" para comenzar.

Asigne un nombre a su proyecto y luego haga clic en el botón "Crear".

Su proyecto de Azure DevOps ahora está listo para usar.

### Configuración de Azure Pipelines

Azure Pipelines es un servicio que se puede usar para automatizar el proceso de creación, prueba e implementación de cambios de código.

Para configurar una canalización de CI mediante Azure Pipelines, deberá crear una nueva canalización de Azure. Para hacer esto, inicie sesión en Azure Portal y navegue hasta el servicio Azure Pipelines.

Haga clic en el botón "Nueva canalización" para comenzar.

En la página "Seleccionar una fuente", seleccione "GitHub" como proveedor de fuente. Luego, elija el repositorio y la rama que desea usar para su canalización. Finalmente, haga clic en el botón "Continuar".

En la página "Seleccionar una plantilla", seleccione la plantilla "Canalización inicial" y haga clic en el botón "Continuar".

En la página "Configura tu tubería", ingresa el siguiente código YAML:

- desencadenar:
- sucursales:
- incluir:
- maestro
- camino: /
- Léame.md
- etapas:
- - Etapa: Construir
- trabajos:
- - trabajo: Construir
- pasos:
- - pago: uno mismo
- - tarea: UseDotNet@2
- entradas:
- tipo de paquete: SDK
- versión: 3.1.100
- - tarea: DotNetCoreCLI@2
- entradas:
- comando: construir
- argumentos: --configuration Release
- - etapa: Prueba
- trabajos:
- - trabajo: Prueba
- pasos:
- - pago: uno mismo
- - tarea: DotNetCoreCLI@2
- entradas:
- comando: prueba
- argumentos: --no-build --configuration Release
- - Etapa: Implementar
- trabajos:
- - trabajo: Implementar
- pasos:
- - pago: uno mismo
- - tarea: Copiar archivos@2
- entradas:
- Carpeta de origen: '$(Pipeline.Área de trabajo)'
- Contenido: '**/*'
- Carpeta de destino: '$(Build.ArtifactStagingDirectory)'
- - tarea: PublishBuildArtifacts@1
- entradas:
- PathtoPublish: '$(Build.ArtifactStagingDirectory)'
- Nombre del artefacto: 'soltar'
- publicarUbicación: 'Contenedor'

Haga clic en el botón "Guardar y ejecutar" para guardar su tubería y ejecutarla.

Su canalización de CI ahora está lista para usar. Siempre que realice cambios en el código de su repositorio de GitHub, Azure Pipelines compilará e implementará automáticamente su código.

## Conclusión

En este artículo, hemos analizado cómo configurar canalizaciones de CI/CD en AWS y Azure. También hemos discutido algunos de los beneficios y desafíos de usar estas plataformas para CI/CD.