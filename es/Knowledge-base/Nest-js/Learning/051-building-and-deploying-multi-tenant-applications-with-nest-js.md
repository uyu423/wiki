---
title: 051: Creación e implementación de aplicaciones multiusuario con Nest.js
description: 
published: true
date: 2023-02-02T01:17:44.943Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:17:40.781Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [051: Building and deploying multi-tenant applications with Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/051-building-and-deploying-multi-tenant-applications-with-nest-js)
{.links-list}


# Introducción

Nest.js es un marco de Node.js para crear aplicaciones escalables del lado del servidor. Utiliza TypeScript, un superconjunto de JavaScript, y combina los beneficios de Node.js y TypeScript para desarrollar aplicaciones.

Nest.js es un marco que lo ayuda a crear aplicaciones del lado del servidor Node.js eficientes y escalables. El marco utiliza TypeScript, un superconjunto de JavaScript, y combina los beneficios de Node.js y TypeScript para desarrollar aplicaciones.

Nest.js es un marco para crear aplicaciones del lado del servidor Node.js eficientes y escalables. Utiliza TypeScript, un superconjunto de JavaScript, y combina los beneficios de Node.js y TypeScript. Con Nest.js, puede desarrollar aplicaciones que son más fáciles de mantener, más fáciles de escalar y más comprobables que las aplicaciones escritas en Vanilla Node.js.

# ¿Qué es una aplicación multiusuario?

Una aplicación multiinquilino es una aplicación que está diseñada para atender a varios inquilinos. Un arrendatario es un grupo de usuarios que comparten un acceso común a la aplicación.

Las aplicaciones multiinquilino están diseñadas para atender a varios inquilinos. Un arrendatario es un grupo de usuarios que comparten un acceso común a la aplicación.

Las aplicaciones multiusuario tienen algunas características clave que las diferencian de las aplicaciones tradicionales:

- Cada inquilino tiene su propia instancia dedicada de la aplicación.
- Los inquilinos pueden estar aislados unos de otros.
- Los inquilinos pueden tener diferentes niveles de acceso a la aplicación.

# ¿Por qué utilizar una aplicación multiusuario?

Las aplicaciones multiusuario tienen algunas ventajas clave sobre las aplicaciones tradicionales:

- Aislamiento: Los inquilinos están aislados unos de otros. Esto significa que otro inquilino no puede acceder a los datos de un arrendatario.
- Seguridad: los inquilinos pueden tener diferentes niveles de acceso a la aplicación. Esto significa que puede controlar quién tiene acceso a qué datos.
- Escalabilidad: cada inquilino tiene su propia instancia dedicada de la aplicación. Esto significa que la aplicación puede escalar para satisfacer las necesidades de cada arrendatario.

# Cómo crear una aplicación multiusuario con Nest.js

Crear una aplicación multiinquilino con Nest.js es fácil. Nest.js proporciona un TenantModule que puede usar para aislar a los inquilinos entre sí.

Para usar TenantModule, debe crear un TenantModule para cada inquilino. TenantModule contiene la configuración del inquilino.

```javascript
import { Module } from '@nestjs/common';
import { TenantModule } from '@nestjs/tenant';

@Module({
  imports: [
    TenantModule.forRoot({
      tenants: [
        {
          id: 'tenant-1',
          name: 'Tenant 1',
          database: 'tenant1'
        },
        {
          id: 'tenant-2',
          name: 'Tenant 2',
          database: 'tenant2'
        }
      ]
    })
  ]
})
export class AppModule {}
```

El método forRoot() toma un objeto de opciones que contiene una matriz de inquilinos. La matriz de inquilinos contiene objetos que tienen una propiedad de identificación, nombre y base de datos.

La propiedad id es el identificador único del inquilino. El nombre de la propiedad es el nombre del inquilino. La propiedad de la base de datos es el nombre de la base de datos que usará el arrendatario.

# Cómo implementar una aplicación multiusuario

La implementación de una aplicación multiinquilino es fácil. Nest.js proporciona un TenantModule que puede usar para implementar su aplicación en múltiples inquilinos.

Para usar TenantModule, debe crear un TenantModule para cada inquilino. TenantModule contiene la configuración del inquilino.

```javascript
import { Module } from '@nestjs/common';
import { TenantModule } from '@nestjs/tenant';

@Module({
  imports: [
    TenantModule.forRoot({
      tenants: [
        {
          id: 'tenant-1',
          name: 'Tenant 1',
          database: 'tenant1'
        },
        {
          id: 'tenant-2',
          name: 'Tenant 2',
          database: 'tenant2'
        }
      ]
    })
  ]
})
export class AppModule {}
```

El método forRoot() toma un objeto de opciones que contiene una matriz de inquilinos. La matriz de inquilinos contiene objetos que tienen una propiedad de identificación, nombre y base de datos.

La propiedad id es el identificador único del inquilino. El nombre de la propiedad es el nombre del inquilino. La propiedad de la base de datos es el nombre de la base de datos que usará el arrendatario.

# Conclusión

En esta publicación, aprendimos sobre las aplicaciones multiusuario y cómo crearlas e implementarlas con Nest.js. Las aplicaciones multiusuario tienen algunas ventajas clave sobre las aplicaciones tradicionales, incluido el aislamiento, la seguridad y la escalabilidad.