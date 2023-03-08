---
title: Protección de aplicaciones TypeScript con JWT y Bcrypt
description: 
published: true
date: 2023-02-07T18:18:08.496Z
tags: 
editor: markdown
dateCreated: 2023-02-07T18:18:06.781Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Securing TypeScript Applications with JWT and Bcrypt***English** document is available*](/en/Knowledge-base/TypeScript/securing-typescript-applications-with-jwt-and-bcrypt)
{.links-list}


# Protección de aplicaciones TypeScript con JWT y Bcrypt

La importancia de la seguridad en las aplicaciones web no puede subestimarse. En este artículo, exploraremos dos métodos populares para proteger las aplicaciones TypeScript: JSON Web Tokens (JWT) y bcrypt. Veremos cómo usar cada una de estas tecnologías para asegurar una aplicación de TypeScript y también aprenderemos acerca de algunos de los peligros potenciales asociados con cada enfoque.

## ¿Qué es el token web JSON (JWT)?

JSON Web Token (JWT) es una forma popular de transmitir datos de forma segura entre dos partes. JWT se compone de tres partes:

- **Encabezado**: contiene el algoritmo utilizado para generar la firma JWT, así como el tipo de JWT (normalmente "JWT").
- **Payload**: Contiene los datos que se van a transmitir. Estos datos normalmente se codifican con Base64.
- **Firma**: Esto se usa para verificar que los datos en la carga útil no hayan sido alterados. La firma se genera utilizando el encabezado y la carga útil, así como una clave secreta.

Un caso de uso común para JWT es transmitir información sobre un usuario autenticado entre una aplicación web y un servidor back-end. Por ejemplo, cuando un usuario inicia sesión en una aplicación web, se puede usar un JWT para transmitir información sobre el usuario (como el nombre del usuario y la dirección de correo electrónico) al servidor back-end. El servidor back-end puede usar esta información para generar una respuesta que se adapte al usuario.

Otro caso de uso común para JWT es transmitir información sobre la sesión de un usuario desde una aplicación web a un servidor back-end. Esto se hace a menudo para evitar tener que almacenar información confidencial (como el ID de sesión de un usuario) en una cookie. Cuando caduca la sesión de un usuario, el JWT se puede utilizar para invalidar la sesión del usuario en el servidor backend.

## ¿Qué es bcrypt?

Bcrypt es una función de hashing de contraseñas que está diseñada para ser costosa desde el punto de vista computacional. Esto es importante porque dificulta que un atacante extraiga una contraseña por fuerza bruta.

Bcrypt se usa típicamente junto con una sal. Un salt es una cadena generada aleatoriamente que se usa para hacer que la función de hash de contraseña sea más difícil de calcular. La sal generalmente se almacena junto con la contraseña codificada.

## ¿Cómo usar JWT para asegurar una aplicación TypeScript?

La forma más común de usar JWT en una aplicación TypeScript es usar el paquete [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken). Este paquete proporciona un conjunto de funciones auxiliares que facilitan la generación y verificación de JWT.

Para usar jsonwebtoken, primero debemos instalarlo:

```
npm install jsonwebtoken
```

Una vez que jsonwebtoken está instalado, podemos usarlo para generar un JWT:

```javascript
const jwt = require('jsonwebtoken');

const payload = {
  userId: 123,
  email: 'user@example.com',
  name: 'John Doe',
};

const secret = 'secret';

const token = jwt.sign(payload, secret);
```

La función `jwt.sign()` toma dos argumentos: la carga útil y el secreto. La carga útil son los datos que queremos codificar en el JWT, y el secreto se usa para generar la firma JWT.

Una vez que hayamos generado el JWT, podemos transmitirlo al servidor backend. El servidor backend puede usar la función `jwt.verify()` para verificar el JWT:

```javascript
const jwt = require('jsonwebtoken');

const token = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEyMywiZW1haWwiOiJ1c2VyQGV4YW1wbGUuY29tIiwibmFtZSI6IkpvaG4gRG9lIn0.S30gaSmqhzPZU6mxPiwm53cH-j2dhYfBYuYTR3LsyiE';

const secret = 'secret';

const payload = jwt.verify(token, secret);
```

La función `jwt.verify()` toma dos argumentos: el token y el secreto. El token es el JWT que queremos verificar y el secreto se usa para verificar la firma JWT.

Si el JWT es válido, la función `jwt.verify()` devolverá la carga útil decodificada. Si el JWT no es válido, la función `jwt.verify()` generará un error.

## ¿Cómo usar bcrypt para asegurar una aplicación TypeScript?

La forma más común de usar bcrypt en una aplicación TypeScript es usar el paquete [bcryptjs](https://www.npmjs.com/package/bcryptjs). Este paquete proporciona un conjunto de funciones auxiliares que facilitan la generación y verificación de hashes de bcrypt.

Para usar bcryptjs, primero debemos instalarlo:

```
npm install bcryptjs
```

Una vez que bcryptjs está instalado, podemos usarlo para codificar una contraseña:

```javascript
const bcrypt = require('bcryptjs');

const password = 'secret';

const salt = bcrypt.genSaltSync(10);

const hash = bcrypt.hashSync(password, salt);
```

La función `bcrypt.hashSync()` toma dos argumentos: la contraseña y la sal. La contraseña es la contraseña que queremos codificar, y la sal se usa para hacer que la función de cifrado de contraseña sea más difícil de calcular.

Una vez que hemos generado el hash, podemos transmitirlo al servidor backend. El servidor backend puede usar la función `bcrypt.compareSync()` para comparar el hash con la contraseña:

```javascript
const bcrypt = require('bcryptjs');

const password = 'secret';

const hash = '$2a$10$2znyB6.qE1T.1S7X3C5NU.7bHJNz5KUzHJZzM6DQLN8tm4Gxe6Ay';

bcrypt.compareSync(password, hash); // true
```

La función `bcrypt.compareSync()` toma dos argumentos: la contraseña y el hash. La contraseña es la contraseña que queremos comparar y el hash es el hash bcrypt con el que queremos compararlo.

Si la contraseña es válida, la función `bcrypt.compareSync()` devolverá `verdadero`. Si la contraseña no es válida, la función `bcrypt.compareSync()` devolverá `falso`.

## ¿Cuáles son algunos peligros potenciales asociados con JWT?

Un peligro potencial asociado con JWT es que los datos en la carga útil no están encriptados. Esto significa que si un atacante logra obtener el JWT, podrá ver los datos en la carga útil.

Otro peligro potencial asociado con JWT es que el secreto utilizado para generar la firma JWT debe mantenerse en secreto. Si el secreto se ve comprometido, un atacante podrá generar su propio JWT con los datos que elija.

## ¿Cuáles son algunos peligros potenciales asociados con bcrypt?

Un peligro potencial asociado con bcrypt es que es una función hash unidireccional. Esto significa que una vez que se ha cifrado una contraseña, no se puede revertir. Esto puede dificultar la recuperación de una contraseña si se olvida.

Otro peligro potencial asociado con bcrypt es que computacionalmente es costoso. Esto puede dificultar el uso de bcrypt en grandes conjuntos de datos.

## Recursos externos

- [Token web JSON](https://jwt.io/)
- [Bcrypt](https://en.wikipedia.org/wiki/Bcrypt)
- [Cómo usar tokens web JSON (JWT) para autenticar usuarios en una aplicación TypeScript](https://auth0.com/blog/how-to-use-jwts-to-authenticate-users-in-a-typescript- solicitud/)
- [Cómo asegurar una aplicación TypeScript con Bcrypt](https://www.sitepoint.com/secure-typescript-application-bcrypt/)