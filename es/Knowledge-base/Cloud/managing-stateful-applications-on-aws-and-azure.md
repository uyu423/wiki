---
title: Administración de aplicaciones con estado en AWS y Azure
description: 
published: true
date: 2023-02-15T16:17:29.525Z
tags: 
editor: markdown
dateCreated: 2023-02-15T16:17:21.591Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Managing Stateful Applications on AWS and Azure***English** document is available*](/en/Knowledge-base/Cloud/managing-stateful-applications-on-aws-and-azure)
{.links-list}


# Administración de aplicaciones con estado en AWS y Azure

## ¿Qué son las aplicaciones con estado?

Una aplicación con estado es aquella que mantiene datos o información de estado entre sesiones de usuario. Esto contrasta con las aplicaciones sin estado, que no mantienen ningún dato ni información de estado en las sesiones de los usuarios.

Las aplicaciones con estado suelen ser más complejas de administrar que las aplicaciones sin estado, ya que requieren el uso de una base de datos para almacenar datos.

## ¿Por qué son importantes las aplicaciones con estado?

Las aplicaciones con estado son importantes porque permiten a los usuarios mantener una experiencia coherente en varias sesiones. Por ejemplo, una aplicación con estado podría permitir que un usuario inicie y cierre sesión en su cuenta sin perder sus datos.

Las aplicaciones con estado también son importantes para las aplicaciones críticas del negocio, donde la consistencia de los datos es esencial.

## ¿Cómo se pueden administrar las aplicaciones con estado en AWS y Azure?

Las aplicaciones con estado se pueden administrar en AWS y Azure mediante una variedad de métodos.

### Método 1: usar los servicios administrados de AWS y Azure

AWS y Azure ofrecen una variedad de servicios administrados que se pueden usar para administrar aplicaciones con estado. Estos servicios incluyen:

-AWS DynamoDB
-AWS RDS
-AWS ElastiCache
-Azure Cosmos DB
- Base de datos Azure SQL

El uso de estos servicios puede simplificar el proceso de administración de aplicaciones con estado, ya que se encargan de muchas de las tareas de infraestructura subyacentes.

### Método 2: usar una herramienta de terceros

Hay una serie de herramientas de terceros que se pueden usar para administrar aplicaciones con estado en AWS y Azure. Estas herramientas incluyen:

- Terraformar
-Ansible
- Marioneta
- Cocinero

El uso de una herramienta de terceros puede ser una buena opción si desea tener más control sobre la administración de sus aplicaciones con estado.

### Método 3: Utilice una solución personalizada

Si tiene requisitos específicos para sus aplicaciones con estado, es posible que deba desarrollar una solución personalizada. Esto podría implicar el uso de una combinación de servicios de AWS y Azure, o el desarrollo de sus propios scripts y herramientas.

## Conclusión

Las aplicaciones con estado son importantes para mantener la coherencia de los datos en varias sesiones de usuario. Hay varias formas diferentes de administrar aplicaciones con estado en AWS y Azure, incluido el uso de servicios administrados, herramientas de terceros o el desarrollo de una solución personalizada.