---
title: Protección de aplicaciones backend con OAuth y JWT
description: 
published: true
date: 2023-02-01T22:43:39.840Z
tags: 
editor: markdown
dateCreated: 2023-02-01T22:43:38.246Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Securing Backend Applications with OAuth and JWT***English** document is available*](/en/Knowledge-base/Backend/securing-backend-applications-with-oauth-and-jwt)
{.links-list}


# Protección de aplicaciones backend con OAuth y JWT

El auge de las aplicaciones de una sola página y los clientes móviles ha dado lugar a una nueva era de seguridad de back-end. En el pasado, la mayoría de las aplicaciones de back-end se procesaban en el lado del servidor, lo que significa que el servidor generaba el HTML y lo enviaba al cliente. Esto significaba que todos los datos confidenciales se guardaban en el servidor y el cliente solo veía el HTML.

Hoy en día, con la representación del lado del cliente, el cliente tiene acceso a los datos y el HTML se genera en el lado del cliente. Esto significa que los datos ya no están seguros en el servidor y deben protegerse.

Una forma de proteger los datos es usar OAuth. OAuth es un protocolo de autorización que permite a un usuario otorgar acceso a una aplicación de terceros a sus datos. La aplicación de terceros tendrá entonces un token de acceso que puede usar para acceder a los datos.

Otra forma de proteger los datos es usar JSON Web Tokens (JWT). JWT es un estándar para codificar datos en un objeto JSON. Luego, los datos se firman con una clave secreta y cualquiera que tenga la clave puede decodificarlos.

Tanto OAuth como JWT tienen sus ventajas y desventajas. OAuth es más seguro pero JWT es más fácil de implementar. En este artículo, aprenderemos a usar tanto OAuth como JWT para proteger una aplicación de back-end.

## autenticación

OAuth es un protocolo de autorización que permite a un usuario otorgar acceso a una aplicación de terceros a sus datos. La aplicación de terceros tendrá entonces un token de acceso que puede usar para acceder a los datos.

OAuth es más seguro que JWT porque utiliza códigos de autorización. Los códigos de autorización solo son válidos para un solo uso y luego se invalidan. Esto significa que si un hacker se hiciera con un código de autorización, solo podría utilizarlo una vez.

JWT, por otro lado, usa tokens de actualización. Los tokens de actualización son válidos por un período de tiempo más largo y se pueden usar para generar nuevos tokens de acceso. Esto significa que si un pirata informático se apoderara de un token de actualización, podría seguir generando nuevos tokens de acceso y obtener acceso a los datos.

OAuth también es más seguro porque usa SSL. SSL es un protocolo que encripta datos. Esto significa que si un hacker interceptara los datos, no podría leerlos.

JWT no utiliza SSL. Esto significa que si un pirata informático interceptara los datos, podría leerlos.

Para usar OAuth, deberá registrar su aplicación con un proveedor de OAuth. Luego, el proveedor le dará una identificación de cliente y un secreto de cliente. La identificación del cliente se usa para identificar su aplicación y el secreto del cliente se usa para autenticar su aplicación.

A continuación, deberá redirigir al usuario a la página de autorización del proveedor. Luego se le pedirá al usuario que le conceda a su aplicación acceso a sus datos.

Si el usuario otorga acceso a su aplicación, el proveedor redirigirá al usuario a su URI de redirección con un código de autorización. Luego, su aplicación utilizará el código de autorización para solicitar un token de acceso al proveedor.

Luego, el proveedor devolverá un token de acceso a su aplicación. Luego, su aplicación puede usar el token de acceso para acceder a los datos.

## JWT

JWT es un estándar para codificar datos en un objeto JSON. Luego, los datos se firman con una clave secreta y cualquiera que tenga la clave puede decodificarlos.

JWT es más fácil de implementar que OAuth porque no requiere que registre su aplicación con un proveedor. Deberá generar una clave secreta, que se puede hacer con una herramienta como OpenSSL.

Para codificar datos con JWT, deberá codificar los datos en base64. A continuación, los datos se pueden firmar con la clave secreta. A continuación, la firma se puede codificar en base64. Los datos, la firma y la clave secreta se pueden concatenar y colocar en un objeto JSON.

Luego, el objeto JSON se puede pasar al cliente. El cliente puede entonces decodificar los datos y verificar la firma. Si la firma es válida, se puede confiar en los datos.

Para decodificar los datos, el cliente necesitará la clave secreta. Esto significa que deberá enviar la clave secreta al cliente, lo cual no es ideal desde el punto de vista de la seguridad.

## Conclusión

Tanto OAuth como JWT tienen sus ventajas y desventajas. OAuth es más seguro pero JWT es más fácil de implementar. En este artículo, hemos aprendido a usar tanto OAuth como JWT para proteger una aplicación de back-end.