---
title: Habilitación del uso compartido de recursos entre orígenes (CORS) para el acceso seguro a la API
description: 
published: true
date: 2023-02-05T01:17:32.833Z
tags: 
editor: markdown
dateCreated: 2023-02-05T01:17:31.137Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Enabling Cross-Origin Resource Sharing (CORS) for Secure API Access***English** document is available*](/en/Knowledge-base/Backend/enabling-cross-origin-resource-sharing-cors-for-secure-api-access)
{.links-list}


# Habilitación del intercambio de recursos de origen cruzado (CORS) para el acceso seguro a la API

## Introducción

En pocas palabras, el intercambio de recursos de origen cruzado (CORS) es un mecanismo que permite que los recursos restringidos en una página web se soliciten desde otro dominio fuera del dominio desde el que se sirvió el primer recurso. Una página web puede incrustar libremente imágenes, hojas de estilo, scripts, iframes y videos de origen cruzado.

Para que los navegadores realicen solicitudes de origen cruzado, una aplicación web primero debe habilitar CORS. No es necesario habilitar CORS para solicitudes del mismo origen, es decir, solicitudes que se realizan al mismo dominio, protocolo y número de puerto que la página misma.

## Cómo funciona CORS

Cuando un navegador realiza una solicitud de origen cruzado, el navegador envía una solicitud al servidor con un encabezado "Origin". El encabezado `Origin` indica el origen de la solicitud, es decir, el dominio, el protocolo y el número de puerto donde se originó la solicitud.

El servidor puede optar por permitir o bloquear la solicitud en función del encabezado `Origen`. Si el servidor permite la solicitud, establecerá un encabezado `Access-Control-Allow-Origin` en la respuesta. El valor del encabezado `Access-Control-Allow-Origin` puede ser un origen específico (por ejemplo, `https://example.com`), un comodín (`*`) o `null`.

Si el encabezado `Access-Control-Allow-Origin` no está presente en la respuesta, o si su valor no es un origen válido, entonces el navegador bloqueará la respuesta.

## Por qué CORS es importante

Sin CORS, el navegador bloqueará las solicitudes de origen cruzado. Esto es importante porque evita que los scripts maliciosos realicen solicitudes no autorizadas a su API.

## Habilitación de CORS

### Configuración del encabezado `Access-Control-Allow-Origin`

El encabezado `Access-Control-Allow-Origin` le dice al navegador si debe o no permitir solicitudes de origen cruzado desde el origen donde se originó la solicitud.

Puede configurar el encabezado `Access-Control-Allow-Origin` en la respuesta HTTP de su servidor. El valor del encabezado puede ser un origen específico (por ejemplo, `https://example.com`), un comodín (`*`) o `null`.

Si desea permitir solicitudes de origen cruzado desde cualquier origen, puede establecer el encabezado `Access-Control-Allow-Origin` en `*`.

```
Access-Control-Allow-Origin: *
```

Si desea permitir solicitudes de origen cruzado desde un origen específico, puede establecer el encabezado `Access-Control-Allow-Origin` en el origen de la solicitud.

```
Access-Control-Allow-Origin: https://example.com
```

Si desea permitir solicitudes de orígenes cruzados de múltiples orígenes, puede establecer el encabezado `Access-Control-Allow-Origin` en una lista de orígenes separados por comas.

```
Access-Control-Allow-Origin: https://example.com,https://example.org
```

Si desea permitir solicitudes de origen cruzado de todos los orígenes excepto un origen específico, puede establecer el encabezado `Access-Control-Allow-Origin` en `*` y el encabezado `Access-Control-Expose-Headers` en `Origin `.

```
Access-Control-Allow-Origin: *
Access-Control-Expose-Headers: Origin
```

### Configuración del encabezado `Access-Control-Allow-Credentials`

El encabezado `Access-Control-Allow-Credentials` le dice al navegador si debe o no enviar cookies con solicitudes de origen cruzado.

Si desea permitir que se envíen cookies con solicitudes de origen cruzado, puede establecer el encabezado `Access-Control-Allow-Credentials` en `true`.

```
Access-Control-Allow-Credentials: true
```

Si desea permitir que se envíen cookies con solicitudes de origen cruzado desde un origen específico, puede establecer el encabezado `Access-Control-Allow-Origin` en el origen de la solicitud y `Access-Control-Allow-Credentials` encabezado a `verdadero`.

```
Access-Control-Allow-Origin: https://example.com
Access-Control-Allow-Credentials: true
```

### Configuración del encabezado `Access-Control-Expose-Headers`

El encabezado `Access-Control-Expose-Headers` le dice al navegador qué encabezados debe permitir que se expongan al cliente.

Si desea permitir que las solicitudes de origen cruzado expongan todos los encabezados, puede configurar el encabezado `Access-Control-Expose-Headers` en `*`.

```
Access-Control-Expose-Headers: *
```

Si desea permitir que las solicitudes de origen cruzado expongan un encabezado específico, puede configurar el encabezado `Access-Control-Expose-Headers` en el encabezado que desea permitir.

```
Access-Control-Expose-Headers: Content-Type
```

Si desea permitir que las solicitudes de origen cruzado expongan múltiples encabezados, puede configurar el encabezado `Access-Control-Expose-Headers` en una lista de encabezados separados por comas.

```
Access-Control-Expose-Headers: Content-Type,X-Custom-Header
```

## Solicitudes comprobadas

Algunas solicitudes de origen cruzado se verifican previamente. Una solicitud comprobada es una solicitud que se realiza con un método HTTP `OPTIONS` y que tiene un encabezado `Origin`.

El navegador envía una solicitud de verificación previa al servidor para verificar si el servidor permite la solicitud de origen cruzado. El servidor puede optar por permitir o bloquear la solicitud de verificación previa.

Si el servidor permite la solicitud de verificación previa, establecerá un encabezado `Access-Control-Allow-Methods` en la respuesta. El valor del encabezado `Access-Control-Allow-Methods` es una lista separada por comas de los métodos HTTP que permite el servidor.

Si el servidor permite la solicitud de verificación previa y el método de solicitud es `GET`, `HEAD` o `POST`, el servidor establecerá un encabezado `Access-Control-Allow-Headers` en la respuesta. El valor del encabezado `Access-Control-Allow-Headers` es una lista separada por comas de los encabezados HTTP que permite el servidor.

## CORS y Seguridad

CORS es un mecanismo de seguridad que se puede usar para proteger su API de solicitudes maliciosas. Al habilitar CORS, puede especificar qué orígenes pueden realizar solicitudes de origen cruzado a su API.

## Conclusión

En este artículo, hemos cubierto qué es CORS, cómo funciona y por qué es importante. También mostramos cómo habilitar CORS en su servidor.