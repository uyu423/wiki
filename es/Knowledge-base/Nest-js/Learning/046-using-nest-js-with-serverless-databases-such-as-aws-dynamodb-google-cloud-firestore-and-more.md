---
title: 046: uso de Nest.js con bases de datos sin servidor como AWS DynamoDB, Google Cloud Firestore y más
description: 
published: true
date: 2023-02-11T22:55:34.659Z
tags: 
editor: markdown
dateCreated: 2023-02-11T22:55:27.838Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [046: Using Nest.js with serverless databases such as AWS DynamoDB, Google Cloud Firestore, and more***English** document is available*](/en/Knowledge-base/Nest-js/Learning/046-using-nest-js-with-serverless-databases-such-as-aws-dynamodb-google-cloud-firestore-and-more)
{.links-list}


# Usar Nest.js con bases de datos sin servidor como AWS DynamoDB, Google Cloud Firestore y más

Nest.js es un marco poderoso para crear aplicaciones del lado del servidor. Se basa en TypeScript y Node.js, y utiliza el marco Express.js. Nest.js es una excelente opción para crear aplicaciones sin servidor porque es fácil de usar y tiene una buena compatibilidad con TypeScript.

En esta publicación, aprenderemos a usar Nest.js con bases de datos sin servidor como AWS DynamoDB, Google Cloud Firestore y más. También aprenderemos a implementar nuestra aplicación Nest.js en AWS Lambda.

## Uso de Nest.js con AWS DynamoDB

AWS DynamoDB es una base de datos sin servidor popular. Es una base de datos NoSQL rápida y escalable. DynamoDB es una excelente opción para aplicaciones sin servidor que necesitan una base de datos rápida y escalable.

Para usar DynamoDB con Nest.js, debemos instalar el paquete @nestjs/aws-serverless-dynamodb. Este paquete proporciona un asignador de datos de DynamoDB para Nest.js.

```bash
$ npm install @nestjs/aws-serverless-dynamodb
```

Una vez que se instala el paquete, podemos crear un asignador de datos de DynamoDB.

```typescript
import { DynamoDB } from '@nestjs/aws-serverless-dynamodb';

@Injectable()
export class DynamoDbMapper {
  constructor(private readonly dynamoDb: DynamoDB) {}
}
```

El asignador de datos de DynamoDB proporciona un cliente de DynamoDB que podemos usar para acceder a DynamoDB.

Para usar el asignador de datos de DynamoDB, debemos crear una tabla de DynamoDB. Podemos hacer esto usando la Consola de administración de AWS.

Una vez que se crea la tabla de DynamoDB, debemos crear un módulo Nest.js que importe el asignador de datos de DynamoDB.

```typescript
import { Module } from '@nestjs/common';
import { DynamoDbMapper } from './dynamodb-mapper.service';

@Module({
  providers: [DynamoDbMapper],
  exports: [DynamoDbMapper],
})
export class DynamoDbModule {}
```

Ahora que hemos creado el asignador de datos de DynamoDB, podemos usarlo para acceder a DynamoDB desde nuestra aplicación Nest.js.

## Uso de Nest.js con Google Cloud Firestore

Google Cloud Firestore es una base de datos sin servidor popular. Es una base de datos NoSQL rápida y escalable. Firestore es una excelente opción para aplicaciones sin servidor que necesitan una base de datos rápida y escalable.

Para usar Firestore con Nest.js, debemos instalar el paquete @nestjs/cloud-firestore. Este paquete proporciona un asignador de datos de Firestore para Nest.js.

```bash
$ npm install @nestjs/cloud-firestore
```

Una vez que el paquete está instalado, podemos crear un mapeador de datos de Firestore.

```typescript
import { Firestore } from '@nestjs/cloud-firestore';

@Injectable()
export class FirestoreMapper {
  constructor(private readonly firestore: Firestore) {}
}
```

El asignador de datos de Firestore proporciona un cliente de Firestore que podemos usar para acceder a Firestore.

Para usar el mapeador de datos de Firestore, necesitamos crear una base de datos de Firestore. Podemos hacer esto usando Google Cloud Console.

Una vez que se crea la base de datos de Firestore, debemos crear un módulo Nest.js que importe el asignador de datos de Firestore.

```typescript
import { Module } from '@nestjs/common';
import { FirestoreMapper } from './firestore-mapper.service';

@Module({
  providers: [FirestoreMapper],
  exports: [FirestoreMapper],
})
export class FirestoreModule {}
```

Ahora que hemos creado el mapeador de datos de Firestore, podemos usarlo para acceder a Firestore desde nuestra aplicación Nest.js.

## Implementación de Nest.js en AWS Lambda

AWS Lambda es una plataforma popular sin servidor. Es una excelente opción para aplicaciones sin servidor que necesitan escalar rápidamente.

Para implementar Nest.js en AWS Lambda, debemos instalar el paquete @nestjs/serverless. Este paquete proporciona un adaptador sin servidor Nest.js.

```bash
$ npm install @nestjs/serverless
```

Una vez que se instala el paquete, podemos crear un adaptador sin servidor Nest.js.

```typescript
import { ServerlessAdapter } from '@nestjs/serverless';

@Injectable()
export class ServerlessAdapter extends ServerlessAdapter {}
```

ServerlessAdapter proporciona un servidor Express.js que podemos usar para ejecutar nuestra aplicación Nest.js en AWS Lambda.

Para usar ServerlessAdapter, necesitamos crear una función de AWS Lambda. Podemos hacer esto usando la Consola de administración de AWS.

Una vez que se crea la función AWS Lambda, debemos crear un módulo Nest.js que importe el ServerlessAdapter.

```typescript
import { Module } from '@nestjs/common';
import { ServerlessAdapter } from './serverless-adapter.service';

@Module({
  providers: [ServerlessAdapter],
  exports: [ServerlessAdapter],
})
export class ServerlessModule {}
```

Ahora que hemos creado ServerlessAdapter, podemos usarlo para implementar nuestra aplicación Nest.js en AWS Lambda.