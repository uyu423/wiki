---
title: Integración de TypeScript con los servicios de AWS para el desarrollo sin servidor
description: 
published: true
date: 2023-02-15T15:56:17.425Z
tags: 
editor: markdown
dateCreated: 2023-02-15T15:56:15.443Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Integrating TypeScript with AWS Services for Serverless Development***English** document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-aws-services-for-serverless-development)
{.links-list}


# Integración de TypeScript con los servicios de AWS para el desarrollo sin servidor

TypeScript es un superconjunto escrito de JavaScript que se compila en JavaScript simple. Ofrece clases, módulos e interfaces para ayudarlo a crear componentes sólidos. TypeScript es fácil de aprender para desarrolladores familiarizados con JavaScript. En este artículo, exploraremos cómo usar TypeScript con los servicios de AWS para crear aplicaciones sin servidor.

## Configuración de mecanografiado

Primero, necesitamos configurar TypeScript en nuestra máquina de desarrollo. Usaremos el administrador de paquetes Node.js (npm) para instalar TypeScript.

```
npm install -g typescript
```

Después de instalar TypeScript, podemos verificar la instalación comprobando la versión de TypeScript.

```
tsc --version
```

## Configuración de AWS SDK para JavaScript

Ahora que tenemos TypeScript instalado, podemos instalar AWS SDK para JavaScript. El SDK nos proporcionará APIs para interactuar con los servicios de AWS desde nuestro código TypeScript. También podemos instalar el SDK usando npm.

```
npm install aws-sdk
```

## Escribiendo código TypeScript

Escribamos un código TypeScript para interactuar con los servicios de AWS. Comenzaremos escribiendo un programa simple para enumerar todos los cubos S3 en nuestra cuenta de AWS.

Primero, necesitamos importar el SDK de AWS en nuestro código TypeScript.

```typescript
import * as AWS from 'aws-sdk';
```

A continuación, debemos configurar el SDK de AWS con nuestras credenciales de AWS. Podemos hacer esto configurando la propiedad `AWS.config.credentials`. Hay varias formas de establecer las credenciales, pero por simplicidad, estableceremos las propiedades `accessKeyId` y `secretAccessKey` directamente.

```typescript
AWS.config.credentials = new AWS.Credentials({
  accessKeyId: '<Your Access Key>',
  secretAccessKey: '<Your Secret Key>'
});
```

Ahora que importamos el SDK de AWS y configuramos nuestras credenciales, podemos crear una instancia del servicio `S3`.

```typescript
const s3 = new AWS.S3();
```

El servicio `S3` proporciona una operación `listBuckets` que podemos usar para listar todos los cubos S3 en nuestra cuenta. La operación `listBuckets` devuelve una promesa, por lo que podemos usar las palabras clave `async/await` para que nuestro código sea más fácil de leer.

```typescript
async function listBuckets() {
  const response = await s3.listBuckets().promise();
  console.log(response.Buckets);
}

listBuckets();
```

Podemos compilar el código TypeScript a JavaScript usando el comando `tsc`.

```
tsc main.ts
```

Esto generará un archivo `main.js` en el mismo directorio. Podemos ejecutar el archivo JavaScript generado usando Node.js.

```
node main.js
```

## Integrando TypeScript con AWS Lambda

AWS Lambda es un servicio informático sin servidor que le permite ejecutar código sin aprovisionar ni administrar servidores. Lambda maneja toda la administración de los recursos informáticos subyacentes, por lo que puede concentrarse en escribir código que aporte valor a sus clientes.

AWS Lambda admite varios idiomas, pero Node.js es el idioma más popular para las funciones de Lambda. En esta sección, veremos cómo crear una función Lambda utilizando TypeScript.

Comenzaremos creando un nuevo directorio para nuestra función Lambda. Llamaremos a este directorio `lambda-ts`.

```
mkdir lambda-ts
cd lambda-ts
```

A continuación, inicializaremos el directorio como un proyecto de Node.js usando npm.

```
npm init -y
```

Ahora, necesitamos instalar el compilador de TypeScript y el SDK de AWS como dependencias para nuestro proyecto.

```
npm install --save-dev typescript
npm install aws-sdk
```

Ahora podemos crear un archivo `tsconfig.json` en el directorio `lambda-ts` para configurar el compilador de TypeScript.

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist"
  }
}
```

También crearemos un directorio `src` en el directorio `lambda-ts` para almacenar nuestro código TypeScript.

```
mkdir src
```

Ahora podemos crear un archivo TypeScript `src/index.ts` en el directorio `src`. Este archivo contendrá nuestro código de función Lambda.

```typescript
import * as AWS from 'aws-sdk';

export async function handler(event: any, context: any) {
  console.log('Hello, world!');
}
```

Podemos compilar el código TypeScript a JavaScript usando el comando `tsc`.

```
tsc
```

Esto generará un archivo `dist/index.js` en el directorio `lambda-ts`. Ahora podemos comprimir el contenido del directorio `dist` y cargar el archivo zip en AWS Lambda.

```
cd dist
zip -r ../function.zip .
```

Ahora podemos probar nuestra función Lambda usando la consola de AWS Lambda.

## Integrando TypeScript con AWS DynamoDB

AWS DynamoDB es un servicio de base de datos NoSQL rápido y escalable. En esta sección, veremos cómo usar TypeScript con DynamoDB.

Comenzaremos creando un nuevo directorio para nuestra aplicación DynamoDB. Llamaremos a este directorio `dynamodb-ts`.

```
mkdir dynamodb-ts
cd dynamodb-ts
```

A continuación, inicializaremos el directorio como un proyecto de Node.js usando npm.

```
npm init -y
```

Ahora, necesitamos instalar el compilador de TypeScript y el SDK de AWS como dependencias para nuestro proyecto.

```
npm install --save-dev typescript
npm install aws-sdk
```

Ahora podemos crear un archivo `tsconfig.json` en el directorio `dynamodb-ts` para configurar el compilador de TypeScript.

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist"
  }
}
```

También crearemos un directorio `src` en el directorio `dynamodb-ts` para almacenar nuestro código TypeScript.

```
mkdir src
```

Ahora podemos crear un archivo TypeScript `src/index.ts` en el directorio `src`. Este archivo contendrá nuestro código de DynamoDB.

```typescript
import * as AWS from 'aws-sdk';

AWS.config.update({ region: 'us-east-1' });

const dynamodb = new AWS.DynamoDB();

async function createTable() {
  const params = {
    TableName: 'Users',
    KeySchema: [
      { AttributeName: 'email', KeyType: 'HASH' } //Partition key
    ],
    AttributeDefinitions: [
      { AttributeName: 'email', AttributeType: 'S' }
    ],
    ProvisionedThroughput: {
      ReadCapacityUnits: 10,
      WriteCapacityUnits: 10
    }
  };

  try {
    const data = await dynamodb.createTable(params).promise();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

createTable();
```

Podemos compilar el código TypeScript a JavaScript usando el comando `tsc`.

```
tsc
```

Esto generará un archivo `dist/index.js` en el directorio `dynamodb-ts`. Ahora podemos ejecutar el archivo JavaScript generado usando Node.js.

```
node dist/index.js
```

## Integrando TypeScript con AWS S3

AWS S3 es un servicio de almacenamiento simple que ofrece alta disponibilidad y durabilidad. En esta sección, veremos cómo usar TypeScript con S3.

Comenzaremos creando un nuevo directorio para nuestra aplicación S3. Llamaremos a este directorio `s3-ts`.

```
mkdir s3-ts
cd s3-ts
```

A continuación, inicializaremos el directorio como un proyecto de Node.js usando npm.

```
npm init -y
```

Ahora, necesitamos instalar el compilador de TypeScript y el SDK de AWS como dependencias para nuestro proyecto.

```
npm install --save-dev typescript
npm install aws-sdk
```

Ahora podemos crear un archivo `tsconfig.json` en el directorio `s3-ts` para configurar el compilador de TypeScript.

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist"
  }
}
```

También crearemos un directorio `src` en el directorio `s3-ts` para almacenar nuestro código TypeScript.

```
mkdir src
```

Ahora podemos crear un archivo TypeScript `src/index.ts` en el directorio `src`. Este archivo contendrá nuestro código S3.

```typescript
import * as AWS from 'aws-sdk';

AWS.config.update({ region: 'us-east-1' });

const s3 = new AWS.S3();

async function putObject() {
  const params = {
    Bucket: '<Your Bucket Name>',
    Key: 'test.txt',
    Body: 'Hello, world!'
  };

  try {
    const data = await s3.putObject(params).promise();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

putObject();
```

Podemos compilar el código TypeScript a JavaScript usando el comando `tsc`.

```
tsc
```

Esto generará un archivo `dist/index.js` en el directorio `s3-ts`. Ahora podemos ejecutar el archivo JavaScript generado usando Node.js.

```
node dist/index.js
```

## Otras lecturas

- [Mecanografiado](https://www.typescriptlang.org/)
- [SDK de AWS para JavaScript](https://aws.amazon.com/sdk-for-node-js/)
- [AWS Lambda](https://aws.amazon.com/lambda/)
- [AWS DynamoDB](https://aws.amazon.com/dynamodb/)
- [AWS S3](https://aws.amazon.com/s3/)