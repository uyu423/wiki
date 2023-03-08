---
title: Implementación de autenticación y autorización para aplicaciones back-end
description: 
published: true
date: 2023-02-09T02:17:46.867Z
tags: 
editor: markdown
dateCreated: 2023-02-09T02:17:45.266Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Implementing Authentication and Authorization for Backend Applications***English** document is available*](/en/Knowledge-base/Backend/implementing-authentication-and-authorization-for-backend-applications)
{.links-list}

      
# Implementación de autenticación y autorización para aplicaciones backend

Ha creado una excelente aplicación de back-end y ahora es el momento de agregar autenticación y autorización. Pero, ¿por dónde empiezas?

Hay muchas formas de implementar la autenticación y la autorización para las aplicaciones de back-end. En este artículo, le daremos una descripción general de los métodos más comunes y le ofreceremos algunos consejos prácticos para cada uno.

## Autenticación

La autenticación es el proceso de verificar que un usuario es quien dice ser. La forma más común de hacerlo es con un nombre de usuario y una contraseña.

Cuando un usuario intente iniciar sesión en su aplicación, deberá verificar que su nombre de usuario y contraseña sean correctos. Esto se puede hacer con una base de datos de usuarios o con un servicio externo como Active Directory.

Si el nombre de usuario y la contraseña son correctos, deberá generar un token que el usuario pueda usar para acceder a la aplicación. Este token debe ser único para el usuario y debe almacenarse de forma segura.

Una forma de generar un token es usar un token web JSON (JWT). Los JWT contienen información sobre el usuario y están firmados con un secreto. Esto significa que puede estar seguro de que el token no ha sido manipulado.

Para usar un JWT, primero deberá crear un secreto. Esto se puede hacer con una herramienta como openssl:

```
 openssl rand -base64 32
```

Una vez que tenga un secreto, puede crear un JWT:

```
jwt.sign({ user_id: 1 }, secret, { expiresIn: '1h' })
```

Esto generará un token que caduca en una hora. Puede usar este token para autenticar al usuario cuando realiza una solicitud a su aplicación.

Para verificar el token, necesitará el secreto que se usó para crearlo. Luego puede usar esto para verificar el token:

```
jwt.verify(token, secret)
```

Si el token es válido, puede estar seguro de que el usuario es quien dice ser.

Otra forma de generar un token es usar una herramienta como Auth0. Auth0 es un servicio que proporciona autenticación y autorización como un servicio. Esto significa que no tiene que preocuparse por crear su propio sistema de autenticación y autorización.

Con Auth0, puede crear un token iniciando la sesión de un usuario con su nombre de usuario y contraseña. Auth0 luego generará un token para el usuario. Este token se puede usar para autenticar al usuario cuando realiza una solicitud a su aplicación.

Para verificar el token, deberá usar el servicio Auth0. Luego puede usar el servicio Auth0 para verificar el token y obtener información sobre el usuario:

```
auth0.verifyToken(token, function(err, user) {
  if (err) {
    // the token is invalid
  } else {
    // the token is valid
    // you can use the user object to get information about the user
  }
})
```

 Auth0 también proporciona una forma de generar tokens para llamadas API. Esto significa que puede usar Auth0 para autenticar y autorizar usuarios para su API.

## Autorización

La autorización es el proceso de determinar si un usuario tiene acceso a un determinado recurso. Por ejemplo, es posible que desee permitir que un usuario lea un archivo, pero no que escriba en él. O quizás desee permitir que un usuario elimine un registro, pero no crearlo ni actualizarlo.

Hay dos formas comunes de implementar la autorización: control de acceso basado en funciones y control de acceso basado en notificaciones.

Con el control de acceso basado en roles, a un usuario se le asigna un rol. Este rol define lo que el usuario puede hacer. Por ejemplo, un usuario puede tener el rol de "administrador", lo que le permite acceder a todos los recursos. O un usuario puede tener el rol de "usuario" que solo le permite acceder a ciertos recursos.

Con el control de acceso basado en reclamos, a un usuario se le asigna uno o más reclamos. Cada reclamación define lo que el usuario puede hacer. Por ejemplo, un usuario puede tener el reclamo "can_read" que le permite leer un recurso. O un usuario podría tener el reclamo de "can_write" que le permite escribir en un recurso.

Para implementar la autorización, deberá decidir qué enfoque usar. Recomendamos utilizar el control de acceso basado en roles para la mayoría de las aplicaciones.

Una vez que haya decidido qué enfoque usar, deberá implementarlo.

Si está utilizando el control de acceso basado en roles, deberá crear una tabla de roles en su base de datos. Esta tabla contendrá los roles que se pueden asignar a sus usuarios. Cada rol tendrá un nombre y una descripción.

También deberá crear una tabla de usuarios. Esta tabla contendrá los usuarios en su sistema. Cada usuario tendrá un role_id que corresponde a un rol en la tabla de roles.

Para autorizar a un usuario, deberá verificar su role_id en la tabla de roles. Por ejemplo, si un usuario intenta acceder a un recurso para el que no tiene permiso, puede devolver un error:

```
if (user.role_id != 1) {
  return res.status(403).send('You do not have permission to access this resource');
}
```

Si usa el control de acceso basado en notificaciones, deberá crear una tabla de notificaciones en su base de datos. Esta tabla contendrá las reclamaciones que se pueden asignar a sus usuarios. Cada reclamo tendrá un nombre y una descripción.

También deberá crear una tabla user_claims. Esta tabla contendrá las reclamaciones de cada usuario. Cada reclamo tendrá un user_id que corresponde a un usuario en la tabla de usuarios.

Para autorizar a un usuario, deberá consultar su tabla user_claims. Por ejemplo, si un usuario intenta acceder a un recurso para el que no tiene permiso, puede devolver un error:

```
if (!user_claims.includes('can_read')) {
  return res.status(403).send('You do not have permission to access this resource');
}
```

## Conclusión

Hay muchas formas de implementar la autenticación y la autorización para las aplicaciones de back-end. En este artículo, le brindamos una descripción general de los métodos más comunes y le ofrecemos algunos consejos prácticos para cada uno.

Esperamos que este artículo haya sido útil y que ahora comprenda mejor cómo implementar la autenticación y la autorización para su aplicación de back-end.