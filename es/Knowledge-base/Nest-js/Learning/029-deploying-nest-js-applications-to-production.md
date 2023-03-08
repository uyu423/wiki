---
title: 029: Implementación de aplicaciones Nest.js en producción
description: 
published: true
date: 2023-02-09T18:17:35.586Z
tags: 
editor: markdown
dateCreated: 2023-02-09T18:17:33.934Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [029: Deploying Nest.js applications to production***English** document is available*](/en/Knowledge-base/Nest-js/Learning/029-deploying-nest-js-applications-to-production)
{.links-list}


# Implementación de aplicaciones Nest.js en producción

## Introducción

Nest.js es un marco de Node.js para crear aplicaciones del lado del servidor. Es un marco relativamente nuevo y está ganando popularidad debido a su facilidad de uso y escalabilidad.

El marco Nest.js se basa en el marco Express.js y utiliza TypeScript, un superconjunto de JavaScript, para el desarrollo.

Las aplicaciones de Nest.js se pueden implementar en una variedad de entornos de producción, como servidores locales, servidores basados en la nube o incluso en entornos sin servidor.

En esta publicación, nos centraremos en cómo implementar una aplicación Nest.js en un entorno de producción.

## Requisitos previos

Antes de comenzar, hay algunas cosas que necesitará:

- Una aplicación Nest.js. Si no tiene uno, puede crear uno simple usando la CLI de Nest.js.
- Un entorno de producción. Puede ser un servidor local, un servidor basado en la nube o un entorno sin servidor.
- Un nombre de dominio. Esto es opcional, pero se recomienda si desea que su aplicación sea accesible para el mundo.

## Implementación en un entorno de producción

Hay dos formas principales de implementar una aplicación Nest.js en un entorno de producción:

- Implementación mediante una herramienta específica de Nest.js, como la CLI de Nest.js o Nest.js Deployer.
- Implementación manual.

### Implementación con una herramienta específica de Nest.js

La forma más sencilla de implementar una aplicación Nest.js en un entorno de producción es utilizar una herramienta específica de Nest.js.

Hay dos herramientas principales que se pueden usar para esto: la CLI de Nest.js y el Deployer de Nest.js.

La CLI de Nest.js es una interfaz de línea de comandos que se puede usar para implementar aplicaciones de Nest.js. Se instala como un módulo global de Node.js y se puede usar para implementar aplicaciones en una variedad de entornos de producción, como servidores locales, servidores basados en la nube o incluso entornos sin servidor.

Para usar la CLI de Nest.js, primero debe instalarla usando npm:

```
npm install -g @nestjs/cli
```

Una vez que se instala la CLI de Nest.js, puede usarla para implementar su aplicación Nest.js.

Por ejemplo, para implementar su aplicación Nest.js en un servidor local, usaría el siguiente comando:

```
nest deploy --server=on-premises
```

Esto implementaría su aplicación Nest.js en un servidor local.

Nest.js Deployer es una herramienta que se puede usar para implementar aplicaciones Nest.js en una variedad de entornos de producción, como servidores locales, servidores basados en la nube o incluso entornos sin servidor.

Para usar Nest.js Deployer, primero debe instalarlo usando npm:

```
npm install -g @nestjs/deployer
```

Una vez que se instala Nest.js Deployer, puede usarlo para implementar su aplicación Nest.js.

Por ejemplo, para implementar su aplicación Nest.js en un servidor local, usaría el siguiente comando:

```
deployer deploy --server=on-premises
```

Esto implementaría su aplicación Nest.js en un servidor local.

### Implementación manual

Si no desea utilizar una herramienta específica de Nest.js para implementar su aplicación Nest.js, puede implementarla manualmente.

Para implementar su aplicación Nest.js manualmente, deberá:

- Cree su aplicación Nest.js.
- Implemente su aplicación en su entorno de producción.

#### Creación de su aplicación Nest.js

El primer paso es crear su aplicación Nest.js.

Para hacer esto, deberá usar la CLI de Nest.js.

La CLI de Nest.js es una interfaz de línea de comandos que se puede usar para crear aplicaciones de Nest.js. Se instala como un módulo global de Node.js y se puede usar para crear aplicaciones para una variedad de entornos de producción, como servidores locales, servidores basados en la nube o incluso entornos sin servidor.

Para usar la CLI de Nest.js, primero debe instalarla usando npm:

```
npm install -g @nestjs/cli
```

Una vez que se instala la CLI de Nest.js, puede usarla para crear su aplicación Nest.js.

Por ejemplo, para crear su aplicación Nest.js para un servidor local, usaría el siguiente comando:

```
nest build --server=on-premises
```

Esto crearía su aplicación Nest.js para un servidor local.

#### Implementación de su aplicación en su entorno de producción

El siguiente paso es implementar su aplicación en su entorno de producción.

La forma en que implemente su aplicación dependerá de su entorno de producción.

Por ejemplo, si está implementando en un servidor local, deberá usar una herramienta como scp para copiar los archivos de su aplicación en el servidor.

Si está implementando en un servidor basado en la nube, necesitará usar una herramienta como AWS Elastic Beanstalk para implementar su aplicación.

Si está implementando en un entorno sin servidor, necesitará usar una herramienta como AWS Lambda para implementar su aplicación.

## Conclusión

En esta publicación, hemos cubierto cómo implementar una aplicación Nest.js en un entorno de producción.

Hemos visto dos formas principales de hacer esto:

- Implementación mediante una herramienta específica de Nest.js, como la CLI de Nest.js o Nest.js Deployer.
- Despliegue manual.

Cualquiera que sea el método que elija, asegúrese de probar su aplicación a fondo en su entorno de producción antes de ponerla a disposición de sus usuarios.