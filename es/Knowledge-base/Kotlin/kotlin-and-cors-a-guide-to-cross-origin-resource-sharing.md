---
title: Kotlin y CORS: una guía para compartir recursos entre orígenes
description: 
published: true
date: 2023-02-12T06:56:06.997Z
tags: 
editor: markdown
dateCreated: 2023-02-12T06:56:05.334Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin and CORS: A Guide to Cross-Origin Resource Sharing***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-cors-a-guide-to-cross-origin-resource-sharing)
{.links-list}

      
Kotlin y CORS: una guía para compartir recursos entre orígenes

El intercambio de recursos de origen cruzado (CORS) es un mecanismo que permite que los recursos restringidos en una página web se soliciten desde otro dominio fuera del dominio desde el que se sirvió el primer recurso. Una página web puede incrustar libremente imágenes, hojas de estilo, scripts, iframes y videos de origen cruzado.

El mecanismo CORS funciona agregando encabezados HTTP a solicitudes y respuestas HTTP entre dominios.

## ¿Cómo funciona CORS?

Cuando un navegador envía una solicitud a un servidor, el navegador incluye un encabezado de origen. Este encabezado indica el dominio de la página que está realizando la solicitud.

Luego, el servidor puede optar por permitir o denegar la solicitud, según el valor del encabezado de origen.

Si el servidor permite la solicitud, incluirá los siguientes encabezados en la respuesta:
- Access-Control-Allow-Origin: este encabezado indica que el servidor permite la solicitud de origen cruzado.
- Access-Control-Allow-Methods: este encabezado indica los métodos (por ejemplo, GET, POST, etc.) que el cliente puede usar.
- Access-Control-Allow-Headers: Este encabezado indica los encabezados que el cliente puede usar.
- Access-Control-Expose-Headers: este encabezado indica a qué encabezados puede acceder el cliente.

Si el servidor no permite la solicitud, devolverá un error.

## ¿Por qué es importante CORS?

El mecanismo CORS proporciona una forma para que las aplicaciones basadas en navegador realicen solicitudes de origen cruzado sin dejar de respetar la política del mismo origen.

La política del mismo origen es una medida de seguridad diseñada para evitar solicitudes de origen cruzado. Sin embargo, existen muchos usos legítimos para las solicitudes de origen cruzado, como realizar una solicitud a un dominio diferente para recuperar datos o utilizar un servicio de terceros.

CORS proporciona una forma de permitir este tipo de solicitudes de origen cruzado y al mismo tiempo brinda cierta protección contra solicitudes maliciosas.

## ¿Cuáles son algunos ejemplos de CORS?

Estos son algunos ejemplos de cómo se puede usar CORS:

- Una página web que realiza una solicitud de origen cruzado para recuperar datos de un servicio de terceros.
- Una página web que realiza una solicitud de origen cruzado para cargar un script de un dominio diferente.
- Una página web que realiza una solicitud de origen cruzado a un iframe que está incrustado en la página.

## ¿Cuáles son algunas limitaciones de CORS?

CORS no es una solución perfecta. La mayor limitación es que no es compatible con todos los navegadores.

Además, las solicitudes malintencionadas pueden eludir CORS. Por ejemplo, una solicitud malintencionada puede usar el objeto XMLHttpRequest para realizar una solicitud de origen cruzado sin los encabezados CORS.

## ¿Cómo puedo usar CORS?

Si desea utilizar CORS, debe configurar un servidor que admita CORS.

 configurar un servidor está más allá del alcance de este artículo, pero puede encontrar más información en la sección de recursos a continuación.

Una vez que tenga un servidor habilitado para CORS, puede realizar solicitudes de origen cruzado utilizando las API XMLHttpRequest o Fetch.

## ¿Qué es una solicitud de verificación previa?

Una solicitud de verificación previa es una solicitud HTTP que se envía antes de una solicitud de origen cruzado. La solicitud de verificación previa se utiliza para determinar si es seguro enviar la solicitud de origen cruzado.

La solicitud de verificación previa se envía con los siguientes encabezados:
- Origen: El dominio de la página que está realizando la solicitud.
- Access-Control-Request-Method: el método (por ejemplo, GET, POST, etc.) que se utilizará para la solicitud de origen cruzado.
- Access-Control-Request-Headers: los encabezados que se utilizarán para la solicitud de origen cruzado.

Luego, el servidor puede optar por permitir o denegar la solicitud, según los valores de estos encabezados.

Si el servidor permite la solicitud, incluirá los siguientes encabezados en la respuesta:
- Access-Control-Allow-Origin: este encabezado indica que el servidor permite la solicitud de origen cruzado.
- Access-Control-Allow-Methods: este encabezado indica los métodos (por ejemplo, GET, POST, etc.) que el cliente puede usar.
- Access-Control-Allow-Headers: Este encabezado indica los encabezados que el cliente puede usar.
- Access-Control-Max-Age: este encabezado indica cuánto tiempo se puede almacenar en caché la respuesta.

Si el servidor no permite la solicitud, devolverá un error.

## ¿Qué es una solicitud de verificación previa?

Una solicitud de verificación previa es una solicitud HTTP que se envía antes de una solicitud de origen cruzado. La solicitud de verificación previa se utiliza para determinar si es seguro enviar la solicitud de origen cruzado.

La solicitud de verificación previa se envía con los siguientes encabezados:
- Origen: El dominio de la página que está realizando la solicitud.
- Access-Control-Request-Method: el método (por ejemplo, GET, POST, etc.) que se utilizará para la solicitud de origen cruzado.
- Access-Control-Request-Headers: los encabezados que se utilizarán para la solicitud de origen cruzado.

Luego, el servidor puede optar por permitir o denegar la solicitud, según los valores de estos encabezados.

Si el servidor permite la solicitud, incluirá los siguientes encabezados en la respuesta:
- Access-Control-Allow-Origin: este encabezado indica que el servidor permite la solicitud de origen cruzado.
- Access-Control-Allow-Methods: este encabezado indica los métodos (por ejemplo, GET, POST, etc.) que el cliente puede usar.
- Access-Control-Allow-Headers: Este encabezado indica los encabezados que el cliente puede usar.
- Access-Control-Max-Age: este encabezado indica cuánto tiempo se puede almacenar en caché la respuesta.

Si el servidor no permite la solicitud, devolverá un error.

## ¿Cuáles son algunos consejos para usar CORS?

Estos son algunos consejos para usar CORS:

- Use las API XMLHttpRequest o Fetch para realizar solicitudes de origen cruzado.
- Establezca el encabezado Origen en el dominio de la página que realiza la solicitud.
- Establezca el encabezado Access-Control-Request-Method en el método (por ejemplo, GET, POST, etc.) que se usará para la solicitud de origen cruzado.
- Establezca el encabezado Access-Control-Request-Headers en los encabezados que se usarán para la solicitud de origen cruzado.
- Si el servidor permite la solicitud, incluirá los siguientes encabezados en la respuesta: Access-Control-Allow-Origin, Access-Control-Allow-Methods, Access-Control-Allow-Headers y Access-Control-Max-Age .
- Si el servidor no permite la solicitud, devolverá un error.

## Conclusión

CORS es un mecanismo que permite solicitar recursos restringidos en una página web desde otro dominio fuera del dominio desde el cual se sirvió el primer recurso. Una página web puede incrustar libremente imágenes, hojas de estilo, scripts, iframes y videos de origen cruzado.

El mecanismo CORS funciona agregando encabezados HTTP a solicitudes y respuestas HTTP entre dominios.

Cuando un navegador envía una solicitud a un servidor, el navegador incluye un encabezado de origen. Este encabezado indica el dominio de la página que está realizando la solicitud.

Luego, el servidor puede optar por permitir o denegar la solicitud, según el valor del encabezado de origen.

Si el servidor permite la solicitud, incluirá los siguientes encabezados en la respuesta: Access-Control-Allow-Origin, Access-Control-Allow-Methods, Access-Control-Allow-Headers y Access-Control-Expose-Headers.

Si el servidor no permite la solicitud, devolverá un error.

El mecanismo CORS proporciona una forma para que las aplicaciones basadas en navegador realicen solicitudes de origen cruzado sin dejar de respetar la política del mismo origen.

La política del mismo origen es una medida de seguridad diseñada para evitar solicitudes de origen cruzado. Sin embargo, existen muchos usos legítimos para las solicitudes de origen cruzado, como realizar una solicitud a un dominio diferente para recuperar datos o utilizar un servicio de terceros.

CORS proporciona una forma de permitir este tipo de solicitudes de origen cruzado y al mismo tiempo brinda cierta protección contra solicitudes maliciosas.

Si desea utilizar CORS, debe configurar un servidor que admita CORS. configurar un servidor está más allá del alcance de este artículo, pero puede encontrar más información en la sección de recursos a continuación.

Una vez que tenga un servidor habilitado para CORS, puede realizar solicitudes de origen cruzado utilizando las API XMLHttpRequest o Fetch.

Una solicitud de verificación previa es una solicitud HTTP que se envía antes de una solicitud de origen cruzado. La solicitud de verificación previa se utiliza para determinar si es seguro enviar la solicitud de origen cruzado.

La solicitud de verificación previa se envía con los siguientes encabezados: Origen, Access-Control-Request-Method y Access-Control-Request-Headers.

Luego, el servidor puede optar por permitir o denegar la solicitud, según los valores de estos encabezados.

Si el servidor permite la solicitud, incluirá los siguientes encabezados en la respuesta: Access-Control-Allow-Origin, Access-Control-Allow-Methods, Access-Control-Allow-Headers y Access-Control-Max-Age.

Si el servidor no permite la solicitud, devolverá un error.

Estos son algunos consejos para usar CORS:

- Use las API XMLHttpRequest o Fetch para realizar solicitudes de origen cruzado.
- Establezca el encabezado Origen en el dominio de la página que realiza la solicitud.
- Establezca el encabezado Access-Control-Request-Method en el método (por ejemplo, GET, POST, etc.) que se usará para la solicitud de origen cruzado.
- Establezca el encabezado Access-Control-Request-Headers en los encabezados que se usarán para la solicitud de origen cruzado.
- Si el servidor permite la solicitud, incluirá los siguientes encabezados en la respuesta: Access-Control-Allow-Origin, Access-Control-Allow-Methods, Access-Control-Allow-Headers y Access-Control-Max-Age .
- Si el servidor no permite la solicitud, devolverá un error.