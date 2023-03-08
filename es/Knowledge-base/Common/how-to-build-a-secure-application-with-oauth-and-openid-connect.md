---
title: Cómo construir una aplicación segura con OAuth y OpenID Connect
description: 
published: true
date: 2023-02-03T16:17:25.535Z
tags: 
editor: markdown
dateCreated: 2023-02-03T16:17:23.897Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [How to Build a Secure Application with OAuth and OpenID Connect***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-secure-application-with-oauth-and-openid-connect)
{.links-list}


# Cómo construir una aplicación segura con OAuth y OpenID Connect

La web moderna tiene que ver con el acceso a datos y servicios de una variedad de fuentes diferentes. Sin embargo, esto puede suponer un riesgo para la seguridad si no se hace correctamente. En este artículo, le mostraremos cómo crear una aplicación segura con OAuth y OpenID Connect.

## ¿Qué es OAuth?

OAuth es un estándar abierto para la autorización que le permite acceder de forma segura a datos y servicios de una variedad de fuentes diferentes. Funciona al permitirle especificar a qué datos y servicios desea acceder y luego autorizar su acceso a esos recursos.

## ¿Qué es OpenID Connect?

OpenID Connect es un protocolo de autenticación que se basa en OAuth. Le permite autenticar a los usuarios con una variedad de proveedores diferentes, como Facebook o Google.

## Cómo usar OAuth y OpenID Connect

Para utilizar OAuth y OpenID Connect, deberá registrar su aplicación con un proveedor. Cada proveedor tiene su propio proceso para hacer esto, por lo que no entraremos en detalles aquí.

Una vez que haya registrado su aplicación, deberá especificar a qué datos y servicios desea acceder. Esto se hace creando un "alcance" para su aplicación. Un ámbito es simplemente una lista de permisos que solicita al proveedor.

Por ejemplo, si está creando una aplicación de lista de tareas pendientes, puede solicitar los siguientes ámbitos:

- Acceso de lectura y escritura a la lista de tareas del usuario
- Acceso de lectura a la información del perfil del usuario

Una vez que haya creado su ámbito, deberá enviar al usuario al extremo de autorización del proveedor. Esta es una URL que el proveedor utilizará para autorizar su acceso a los datos del usuario.

El punto final de autorización le pedirá al usuario que inicie sesión y luego le pedirá que le otorgue a su aplicación acceso a los datos y servicios que ha especificado en su alcance.

Una vez que el usuario haya otorgado acceso a su aplicación, el proveedor redirigirá al usuario a su aplicación con un código de autorización. Luego, este código se puede cambiar por un token de acceso, que se puede usar para acceder a los datos del usuario.

## Cómo proteger su aplicación

Una vez que tenga un token de acceso, deberá tomar algunas precauciones para asegurarse de que se use de forma segura.

Primero, nunca debe almacenar el token de acceso en texto sin formato. En su lugar, debe almacenarlo en un formato cifrado.

En segundo lugar, solo debe enviar el token de acceso a través de una conexión cifrada, como HTTPS.

En tercer lugar, debe asegurarse de que el token de acceso solo se use para los datos y servicios para los que fue diseñado. Por ejemplo, si su aplicación solo necesita acceso de lectura a la lista de tareas del usuario, entonces el token de acceso solo debe usarse para ese propósito.

## Conclusión

En este artículo, le mostramos cómo crear una aplicación segura con OAuth y OpenID Connect. Al tomar las precauciones descritas en este artículo, puede asegurarse de que su aplicación sea segura y que los datos de su usuario estén protegidos.