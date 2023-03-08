---
title: Integración de TypeScript con AWS Lambda para funciones sin servidor
description: 
published: true
date: 2023-02-11T02:17:23.605Z
tags: 
editor: markdown
dateCreated: 2023-02-11T02:17:21.924Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Integrating TypeScript with AWS Lambda for Serverless Functions***English** document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-aws-lambda-for-serverless-functions)
{.links-list}


# Integración de TypeScript con AWS Lambda para funciones sin servidor

TypeScript es un lenguaje de programación gratuito y de código abierto desarrollado y mantenido por Microsoft. Es un superconjunto de JavaScript que agrega escritura y programación orientada a objetos basada en clases al lenguaje.

AWS Lambda es un servicio informático basado en la nube que le permite ejecutar código sin aprovisionar ni administrar servidores. Es una plataforma sin servidor que ejecuta su código en respuesta a eventos y administra automáticamente los recursos informáticos por usted.

Puede usar TypeScript con AWS Lambda para escribir funciones sin servidor. En este artículo, le mostraremos cómo escribir una función TypeScript e implementarla en AWS Lambda.

## Escribir una función de TypeScript

Una función TypeScript es una pieza de código que se ejecuta en respuesta a un evento. Puede activarse mediante una solicitud HTTP, una operación de base de datos o cualquier otra cosa.

Vamos a crear una función de TypeScript que se active mediante una solicitud HTTP. Primero, cree un archivo llamado `index.ts` y agréguele el siguiente código:

```typescript
import { APIGatewayProxyEvent, APIGatewayProxyResult } from 'aws-lambda';

export const handler = async (event: APIGatewayProxyEvent): Promise<APIGatewayProxyResult> => {
  const body = JSON.parse(event.body);

  return {
    statusCode: 200,
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      message: `Hello, ${body.name}`
    })
  };
};
```

Esta función se activa mediante una solicitud HTTP y devuelve un mensaje de bienvenida. La función `handler` es el punto de entrada para la función. Toma un objeto `evento` como argumento y devuelve una `Promesa` que se resuelve en un objeto `APIGatewayProxyResult`.

El objeto `event` contiene información sobre la solicitud HTTP, como los encabezados, el cuerpo y los parámetros de consulta. La propiedad `body` del objeto `event` contiene el cuerpo de la solicitud codificado en JSON.

La función `handler` analiza el cuerpo de la solicitud y devuelve una respuesta codificada en JSON. La propiedad `statusCode` de la respuesta se establece en `200` para indicar que la solicitud fue exitosa. La propiedad `headers` se usa para establecer el encabezado `Content-Type` de la respuesta. La propiedad `body` contiene el mensaje que se devuelve a la persona que llama.

## Desplegando la Función

Ahora que hemos escrito nuestra función TypeScript, debemos implementarla en AWS Lambda. Usaremos [Serverless Framework](https://serverless.com/) para implementar nuestra función.

Serverless Framework es un marco basado en Node.js que le permite implementar aplicaciones sin servidor en AWS Lambda. Facilita la administración de sus funciones sin servidor y proporciona muchas funciones, como [control de versiones de funciones] (https://serverless.com/blog/serverless-app-versioning/), [alias de funciones] (https:// serverless.com/blog/serverless-app-aliases/), y [etapas de función](https://serverless.com/blog/serverless-app-stages/).

Primero, instale Serverless Framework usando npm:

```
npm install -g serverless
```

A continuación, cree un archivo llamado `serverless.yml` en la raíz de su proyecto y agréguele el siguiente código:

```yaml
service: my-service

provider:
  name: aws
  runtime: nodejs8.10

functions:
  myFunction:
    handler: index.handler
    events:
      - http:
          path: /
          method: post
```

Este archivo contiene la configuración de su aplicación sin servidor. La propiedad `servicio` es el nombre de su aplicación. La propiedad `provider` se utiliza para configurar el proveedor (en este caso, AWS). La propiedad `runtime` se usa para especificar el tiempo de ejecución de Node.js que usará su función.

La propiedad `functions` se utiliza para configurar sus funciones sin servidor. En este caso, tenemos una función llamada `myFunction`. La propiedad `handler` se utiliza para especificar el punto de entrada de la función (`index.handler`). La propiedad `events` se utiliza para configurar el evento que activará la función. En este caso, hemos configurado un evento HTTP que se activará cuando se realice una solicitud `POST` a la ruta `/`.

Ahora que hemos configurado nuestra aplicación sin servidor, podemos implementarla usando el comando `implementar sin servidor`:

```
serverless deploy
```

Este comando implementará su aplicación sin servidor en AWS. Creará una función AWS Lambda y una API de Amazon API Gateway.

Puede probar su función haciendo una solicitud `POST` a la ruta `/`. Deberías ver un mensaje como este:

```
{
    "message": "Hello, John"
}
```

## Terminando

En este artículo, le mostramos cómo escribir una función de TypeScript e implementarla en AWS Lambda. TypeScript es un excelente lenguaje para escribir funciones sin servidor porque agrega verificación de tipos y programación orientada a objetos basada en clases a JavaScript.

Si desea obtener más información sobre TypeScript, consulte el [sitio web de TypeScript] (https://www.typescriptlang.org/).

Si desea obtener más información sobre AWS Lambda, consulte la [documentación de AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/getting-started.html).