---
title: 013: Implementación de autorización en Nest.js
description: 
published: true
date: 2023-02-14T23:32:20.845Z
tags: 
editor: markdown
dateCreated: 2023-02-14T23:32:18.984Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [013: Implementing authorization in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/013-implementing-authorization-in-nest-js)
{.links-list}


# Implementando la autorización en Nest.js

Nest.js es un marco de Node.js para crear aplicaciones escalables del lado del servidor. Utiliza JavaScript progresivo, está construido con TypeScript (preserva la compatibilidad con JavaScript puro) y combina elementos de programación orientada a objetos, programación funcional y programación reactiva funcional.

En esta publicación, nos centraremos en cómo implementar la autorización en una aplicación Nest.js. Veremos qué es la autorización y por qué es importante, antes de pasar a cómo implementarla en Nest.js.

## ¿Qué es la autorización?

La autorización es el proceso de determinar si un usuario puede realizar una acción o acceder a un recurso. Suele implicar comprobar que el usuario tiene los permisos necesarios para realizar la acción.

En una aplicación web, la autorización generalmente se realiza verificando la identidad del usuario y luego comparándola con una lista de usuarios autorizados. Si el usuario está autorizado, se le permite acceder al recurso. Si no están autorizados, no se les permite acceder al recurso.

Hay dos tipos principales de autorización:

- **Autenticación**: Este es el proceso de verificar que el usuario es quien dice ser. En una aplicación web, esto generalmente se hace comparando las credenciales del usuario (por ejemplo, nombre de usuario y contraseña) con una base de datos de usuarios.

- **Autorización**: Este es el proceso de verificar que el usuario tiene los permisos necesarios para acceder a un recurso. En una aplicación web, esto generalmente se hace verificando la identidad del usuario con una lista de usuarios autorizados. Si el usuario está autorizado, se le permite acceder al recurso. Si no están autorizados, no se les permite acceder al recurso.

## ¿Por qué es importante la autorización?

La autorización es importante porque ayuda a mantener segura su aplicación. Al permitir que solo los usuarios autorizados accedan a los recursos, puede ayudar a evitar el acceso no autorizado a datos confidenciales.

## Implementando la autorización en Nest.js

Nest.js proporciona varias formas de implementar la autorización. En esta sección, veremos dos de las formas más comunes: usar el decorador `@Authorized()` y los protectores `CanActivate`.

### Usando el decorador `@Authorized()`

El decorador `@Authorized()` se puede usar para restringir el acceso a un controlador o acción. Toma un solo argumento, que es la lista de roles que pueden acceder al controlador o la acción.

Por ejemplo, el siguiente controlador solo sería accesible para los usuarios con la función "ADMIN":

```typescript
@Controller('/users')
@Authorized(['ADMIN'])
export class UserController {

}
```

Si un usuario sin el rol `ADMIN` intentara acceder al punto final `/usuarios`, recibiría un error `no autorizado`.

### Uso de los protectores `CanActivate`

Los guardias `CanActivate` se pueden usar para restringir el acceso a una ruta. Toman un solo argumento, que es la lista de roles que pueden acceder a la ruta.

Por ejemplo, la siguiente ruta solo sería accesible para los usuarios con el rol "ADMIN":

```typescript
@Get('/users')
@CanActivate(['ADMIN'])
export class UserController {

}
```

Si un usuario sin el rol `ADMIN` intentara acceder al punto final `/usuarios`, recibiría un error `no autorizado`.

## Información adicional

- Documentación de Nest.js: https://docs.nestjs.com/
- Documentación de TypeScript: https://www.typescriptlang.org/docs/handbook/basic-types.html