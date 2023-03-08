---
title: 043: Uso de Nest.js con Docker
description: 
published: true
date: 2023-02-15T14:32:51.851Z
tags: 
editor: markdown
dateCreated: 2023-02-15T14:32:50.209Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [043: Using Nest.js with Docker***English** document is available*](/en/Knowledge-base/Nest-js/Learning/043-using-nest-js-with-docker)
{.links-list}


# Uso de Nest.js con Docker

Docker es una gran herramienta para desarrollar e implementar aplicaciones web. Le permite empaquetar su aplicación en un entorno autónomo que es fácil de implementar y administrar.

Nest.js es un marco para crear aplicaciones del lado del servidor Node.js eficientes y escalables. Utiliza JavaScript moderno, está construido con TypeScript (que trae verificación de tipo estático a JavaScript) y combina elementos de programación orientada a objetos y programación funcional.

En esta publicación, aprenderemos a usar Nest.js con Docker. Comenzaremos creando una aplicación Nest.js simple y luego la colocaremos en un contenedor usando Docker. También aprenderemos a usar Docker Compose para administrar las dependencias de nuestra aplicación.

## Creación de una aplicación Nest.js

Comencemos por crear una aplicación Nest.js simple. Llamaremos a nuestra aplicación "lista de tareas pendientes".

Primero, necesitamos instalar la CLI de Nest.js. Podemos hacer esto usando npm:

```
npm install -g @nestjs/cli
```

Una vez instalada la CLI de Nest.js, podemos crear nuestra aplicación usando el siguiente comando:

```
nest new todo-list
```

Esto creará un nuevo directorio llamado "lista de tareas pendientes" y generará el andamiaje básico para nuestra aplicación Nest.js.

A continuación, necesitamos instalar las dependencias para nuestra aplicación. Podemos hacer esto usando npm:

```
cd todo-list
npm install
```

Ahora que las dependencias de nuestra aplicación están instaladas, podemos iniciar la aplicación usando el siguiente comando:

```
npm start
```

Esto iniciará la aplicación en el puerto 3000. Podemos ver la aplicación en nuestro navegador navegando a http://localhost:3000.

## Poner en contenedores nuestra aplicación

Ahora que tenemos una aplicación Nest.js básica en funcionamiento, vamos a contenerla usando Docker.

Primero, necesitamos crear un archivo llamado "Dockerfile" en el directorio raíz de nuestra aplicación. Este archivo contendrá las instrucciones para construir nuestra imagen de Docker.

Nuestro Dockerfile comenzará con la siguiente línea:

```
FROM node:10-alpine
```

Esta línea especifica que queremos usar la imagen Alpine de Node.js 10 como imagen base para nuestra imagen de Docker. Alpine es una distribución ligera de Linux que es perfecta para usar como imagen base para nuestra aplicación.

A continuación, debemos copiar los archivos de nuestra aplicación en la imagen. Podemos hacer esto usando el comando COPY:

```
COPY . .
```

Esto copiará todos los archivos del directorio actual en la imagen.

Ahora que nuestros archivos están copiados, necesitamos instalar las dependencias de nuestra aplicación. Podemos hacer esto usando el comando npm:

```
RUN npm install
```

Finalmente, debemos especificar el comando que se utilizará para iniciar nuestra aplicación. Podemos hacer esto usando el comando CMD:

```
CMD ["npm", "start"]
```

Esto iniciará nuestra aplicación cuando se inicie el contenedor.

Nuestro Dockerfile ahora está completo. Podemos construir nuestra imagen de Docker usando el siguiente comando:

```
docker build -t todo-list .
```

Esto creará una imagen llamada "lista de tareas pendientes" siguiendo las instrucciones de nuestro Dockerfile.

Una vez construida nuestra imagen, podemos ejecutarla usando el siguiente comando:

```
docker run -d -p 3000:3000 todo-list
```

Esto iniciará un contenedor basado en nuestra imagen de "lista de tareas pendientes" y asignará el puerto 3000 en el contenedor al puerto 3000 en nuestra máquina host.

Ahora podemos ver nuestra aplicación en nuestro navegador navegando a http://localhost:3000.

## Usando Docker Compose

Docker Compose es una herramienta para definir y ejecutar aplicaciones Docker de varios contenedores. Le permite especificar las dependencias de su aplicación en un solo archivo y luego iniciar todos los contenedores con un solo comando.

Vamos a crear un archivo "docker-compose.yml" en el directorio raíz de nuestra aplicación. Este archivo contendrá las instrucciones para ejecutar nuestra aplicación usando Docker Compose.

Nuestro archivo docker-compose.yml comenzará con la siguiente línea:

```
version: '3'
```

Esta línea especifica que estamos usando la versión 3 del formato de archivo Docker Compose.

A continuación, debemos especificar los servicios de los que depende nuestra aplicación. Podemos hacer esto usando la tecla "servicios":

```
services:
  todo-list:
    image: todo-list
    ports:
      - "3000:3000"
```

Esto define un servicio llamado "lista de tareas pendientes" que usa la imagen de la "lista de tareas pendientes" y asigna el puerto 3000 en el contenedor al puerto 3000 en nuestra máquina host.

Ahora que nuestro archivo docker-compose.yml está completo, podemos iniciar nuestra aplicación usando el siguiente comando:

```
docker-compose up
```

Esto iniciará todos los contenedores definidos en nuestro archivo docker-compose.yml.

Ahora podemos ver nuestra aplicación en nuestro navegador navegando a http://localhost:3000.

## Conclusión

En esta publicación, aprendimos a usar Nest.js con Docker. Comenzamos creando una aplicación Nest.js simple y luego la colocamos en un contenedor usando Docker. También aprendimos a usar Docker Compose para administrar las dependencias de nuestra aplicación.