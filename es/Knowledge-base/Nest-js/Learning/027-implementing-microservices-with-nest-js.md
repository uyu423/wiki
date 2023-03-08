---
title: 027: Implementando microservicios con Nest.js
description: 
published: true
date: 2023-02-15T07:32:35.248Z
tags: 
editor: markdown
dateCreated: 2023-02-15T07:32:27.449Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [027: Implementing microservices with Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/027-implementing-microservices-with-nest-js)
{.links-list}


# Implementando microservicios con Nest.js

Los microservicios son un estilo arquitectónico popular para crear aplicaciones en la nube que son escalables y resistentes. Nest.js es un marco de Node.js para crear aplicaciones del lado del servidor eficientes, escalables y de nivel empresarial.

En esta publicación, aprenderemos cómo implementar microservicios con Nest.js. Comenzaremos analizando qué son los microservicios y por qué son útiles. Luego veremos cómo crear un microservicio simple usando Nest.js. Finalmente, aprenderemos cómo implementar nuestro microservicio en una plataforma en la nube.

## ¿Qué son los microservicios?

Los microservicios son un estilo de arquitectura de software en el que las aplicaciones se crean como un conjunto de pequeños servicios independientes. Cada servicio tiene una única responsabilidad y se puede implementar y escalar de forma independiente.

Los microservicios tienen una serie de beneficios sobre las arquitecturas monolíticas tradicionales. Son más fáciles de desarrollar, implementar y escalar. También son más resistentes, ya que una falla en un servicio no afecta a los otros servicios.

## Creando un microservicio con Nest.js

Ahora que hemos visto qué son los microservicios, aprendamos cómo crear un microservicio simple usando Nest.js.

Nest.js es un marco de Node.js para crear aplicaciones del lado del servidor eficientes, escalables y de nivel empresarial. Utiliza TypeScript, que es un superconjunto de JavaScript que proporciona verificación de tipos estáticos y otros beneficios.

Para crear un microservicio Nest.js, usaremos la CLI de Nest. Nest CLI es una interfaz de línea de comandos que facilita la creación, el desarrollo y la prueba de aplicaciones Nest.js.

Primero, crearemos un nuevo directorio para nuestro microservicio:

```
mkdir my-microservice
```

A continuación, inicializaremos un nuevo proyecto Nest.js en nuestro directorio:

```
nest init
```

Esto creará un archivo llamado `package.json` en nuestro directorio. Este archivo contiene información sobre nuestro proyecto, incluidas las dependencias que necesitaremos instalar.

A continuación, instalaremos las dependencias para nuestro proyecto:

```
npm install
```

Ahora que nuestro proyecto está configurado, podemos comenzar a codificar nuestro microservicio. Comenzaremos creando un archivo llamado `src/app.controller.ts`:

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller()
export class AppController {
  @Get()
  root(): string {
    return 'Hello World!';
  }
}
```

Este archivo contiene un controlador llamado `AppController`. Este controlador contiene un único método, `root()`, que devuelve la cadena `'Hello World!'`.

A continuación, crearemos un archivo llamado `src/app.module.ts`:

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';

@Module({
  controllers: [AppController],
})
export class AppModule {}
```

Este archivo contiene un módulo llamado `AppModule`. Este módulo contiene nuestro `AppController`.

Finalmente, crearemos un archivo llamado `src/main.ts`:

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

Este archivo contiene el código que iniciará nuestro microservicio. Primero, creamos una nueva `NestFactory`, que es una fábrica para crear aplicaciones Nest.js. Luego pasamos nuestro `AppModule` a `NestFactory`. Finalmente, llamamos al método `listen()` para iniciar el microservicio en el puerto `3000`.

Ahora que nuestro microservicio está completo, podemos iniciarlo ejecutando el siguiente comando:

```
npm start
```

Luego podemos acceder a nuestro microservicio en http://localhost:3000.

## Desplegando un microservicio

Ahora que hemos visto cómo crear un microservicio con Nest.js, aprendamos cómo implementarlo.

Hay muchas formas diferentes de implementar un microservicio. En esta publicación, aprenderemos cómo implementar nuestro microservicio en una plataforma en la nube usando Docker.

Docker es una herramienta que facilita el empaquetado, la implementación y la ejecución de aplicaciones en un contenedor. Un contenedor es un entorno autónomo que incluye todo lo que necesita una aplicación para ejecutarse, como el código, el tiempo de ejecución, las herramientas del sistema y las bibliotecas.

Para implementar nuestro microservicio en una plataforma en la nube usando Docker, primero debemos crear un `Dockerfile`:

```
FROM node:10.16.0-alpine

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

Este `Dockerfile` contiene las instrucciones para construir nuestra imagen de Docker. Primero, especificamos la imagen del `nodo` que queremos usar. A continuación, creamos un directorio de trabajo para nuestra aplicación. Luego, copiamos el archivo `package.json` a nuestro directorio de trabajo. Usamos este archivo para instalar las dependencias de nuestra aplicación.

Luego, copiamos el resto del código de nuestra aplicación a nuestro directorio de trabajo. Finalmente, exponemos el puerto `3000` y especificamos el comando que debe ejecutarse cuando se inicia nuestro contenedor.

Ahora que tenemos nuestro `Dockerfile`, podemos construir nuestra imagen de Docker:

```
docker build -t my-microservice .
```

Este comando creará una imagen Docker con la etiqueta `my-microservice`. Luego podemos ejecutar nuestra imagen de Docker:

```
docker run -d -p 3000:3000 my-microservice
```

Este comando iniciará un contenedor desde nuestra imagen `my-microservice`. El indicador `-d` especifica que el contenedor debe ejecutarse en modo separado. Esto significa que el contenedor se ejecutará en segundo plano. El indicador `-p` especifica que el puerto `3000` en nuestro host debe asignarse al puerto `3000` en el contenedor.

Luego podemos acceder a nuestro microservicio en http://localhost:3000.

## Conclusión

En esta publicación, hemos aprendido cómo implementar microservicios con Nest.js. Hemos visto cómo crear un microservicio simple y cómo implementarlo en una plataforma en la nube usando Docker.