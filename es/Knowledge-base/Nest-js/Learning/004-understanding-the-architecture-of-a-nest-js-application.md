---
title: 004: Comprender la arquitectura de una aplicación Nest.js
description: 
published: true
date: 2023-02-14T01:56:43.346Z
tags: 
editor: markdown
dateCreated: 2023-02-14T01:56:36.156Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [004: Understanding the architecture of a Nest.js application***English** document is available*](/en/Knowledge-base/Nest-js/Learning/004-understanding-the-architecture-of-a-nest-js-application)
{.links-list}


# Comprender la arquitectura de una aplicación Nest.js

Nest.js es un marco de Node.js para crear aplicaciones escalables del lado del servidor. Utiliza JavaScript moderno, está construido con TypeScript (que se compila en JavaScript) y combina elementos de programación orientada a objetos, programación funcional y programación reactiva.

Las aplicaciones Nest.js están organizadas en un conjunto de módulos anidados. Los módulos de Nest.js son equivalentes a los módulos de Angular y se utilizan para agrupar componentes, servicios, canalizaciones y directivas relacionados.

El objetivo principal de un módulo Nest.js es proporcionar un lugar único (o raíz) donde se pueda encontrar todo el código relacionado para una función o dominio único. Esto facilita el razonamiento y el mantenimiento de las aplicaciones Nest.js.

Los módulos de Nest.js están organizados en una estructura jerárquica con un módulo raíz y cero o más módulos secundarios. El módulo raíz es el punto de entrada de la aplicación y normalmente se usa para configurar la aplicación Nest.js. Los módulos secundarios se utilizan para agrupar código relacionado para una característica o dominio.

La siguiente figura muestra la estructura típica de una aplicación Nest.js. El directorio src contiene el código fuente de la aplicación. El archivo app.module.ts es el módulo raíz y se usa para configurar la aplicación Nest.js. Los módulos secundarios se utilizan para agrupar código relacionado para una característica o dominio.

![Figura 1. La estructura típica de una aplicación Nest.js](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/img/app-structure.png)

El archivo src/app.module.ts es el módulo raíz y se usa para configurar la aplicación Nest.js. El módulo @Nestjs/common se importa y se usa para proporcionar la clase CommonModule. La clase CommonModule se utiliza para proporcionar el servicio de inyector. El servicio del inyector se utiliza para resolver dependencias.

El módulo @Nestjs/core se importa y se utiliza para proporcionar la clase NestFactory. La clase NestFactory se usa para crear una instancia de aplicación Nest.js.

La clase AppModule se importa y se usa para definir la clase AppModule. La clase AppModule se usa para configurar la aplicación Nest.js.

La clase AppModule se anota con el decorador @Module(). El decorador @Module() se usa para definir un módulo Nest.js.

La clase AppModule se importa y se usa para definir la clase AppModule. La clase AppModule se usa para configurar la aplicación Nest.js.

La clase AppModule se anota con el decorador @Module(). El decorador @Module() se usa para definir un módulo Nest.js.

La clase AppModule contiene un constructor y un método configure(). El constructor se utiliza para inyectar las dependencias. El método configure() se usa para configurar la aplicación Nest.js.

El archivo src/app.controller.ts se usa para definir la clase AppController. La clase AppController se usa para manejar solicitudes HTTP.

La clase AppController se anota con el decorador @Controller(). El decorador @Controller() se usa para definir un controlador Nest.js.

La clase AppController contiene un método root(). El método root() se usa para manejar solicitudes HTTP GET.

El archivo src/app.service.ts se usa para definir la clase AppService. La clase AppService se usa para proporcionar los datos para el controlador.

La clase AppService se anota con el decorador @Injectable(). El decorador @Injectable() se usa para definir un servicio Nest.js.

La clase AppService contiene un método getData(). El método getData() se usa para devolver los datos para el controlador.

El archivo src/environments/environment.ts se utiliza para definir las variables de entorno. Las variables de entorno se utilizan para configurar la aplicación Nest.js.

Las variables de entorno se inyectan en la clase AppModule mediante la función environment().

La función environment() se utiliza para inyectar las variables de entorno en la aplicación Nest.js.

La función environment() toma un objeto como argumento. El objeto contiene las variables de entorno.

La función Environment() devuelve un objeto Environment. El objeto Environment contiene las variables de entorno.

El objeto Environment se usa para configurar la aplicación Nest.js.

El archivo src/main.ts es el punto de entrada para la aplicación Nest.js. El archivo src/main.ts se usa para crear una instancia de la aplicación Nest.js.

El archivo src/main.ts importa la clase AppModule. La clase AppModule se usa para configurar la aplicación Nest.js.

El archivo src/main.ts usa la clase NestFactory para crear una instancia de la aplicación Nest.js.

La clase NestFactory se importa desde el módulo @nestjs/core. La clase NestFactory se usa para crear una instancia de aplicación Nest.js.

La clase NestFactory toma la clase AppModule como argumento. La clase AppModule se usa para configurar la aplicación Nest.js.

La clase NestFactory devuelve una instancia de la aplicación Nest.js.

La instancia de la aplicación Nest.js se usa para iniciar la aplicación Nest.js.

La instancia de la aplicación Nest.js se inicia con el método start().

El método start() se usa para iniciar la aplicación Nest.js.

El método start() toma un número de puerto como argumento. El número de puerto se utiliza para escuchar solicitudes HTTP.

El método start() devuelve una Promesa. La Promesa se resuelve cuando se inicia la aplicación Nest.js.

El archivo src/index.ts es el punto de entrada para el compilador de TypeScript. El archivo src/index.ts se usa para compilar el código TypeScript.

El archivo src/index.ts importa la clase AppModule. La clase AppModule se usa para configurar la aplicación Nest.js.

El archivo src/index.ts usa el archivo tsconfig.json para configurar el compilador de TypeScript.

El archivo tsconfig.json se usa para configurar el compilador de TypeScript.

El archivo tsconfig.json contiene las opciones del compilador. Las opciones del compilador se utilizan para configurar el compilador de TypeScript.

El archivo tsconfig.json se usa para compilar el código TypeScript en código JavaScript.

El código TypeScript se compila en código JavaScript usando el comando tsc.

El comando tsc se usa para compilar el código TypeScript en código JavaScript.

El comando tsc toma el archivo tsconfig.json como argumento. El archivo tsconfig.json se usa para configurar el compilador de TypeScript.

El comando tsc compila el código TypeScript en código JavaScript.

El código JavaScript compilado se coloca en el directorio dist.

El directorio dist contiene el código JavaScript compilado.

El directorio dist es el directorio de salida para el compilador de TypeScript.

La aplicación Nest.js se ejecuta con el comando de nodo.

El comando de nodo se usa para ejecutar la aplicación Nest.js.

El comando de nodo toma el código JavaScript compilado como argumento. El código JavaScript compilado se coloca en el directorio dist.

El comando de nodo ejecuta la aplicación Nest.js.

La aplicación Nest.js se ejecuta en un servidor Node.js.

El servidor Node.js se utiliza para ejecutar la aplicación Nest.js.

El servidor Node.js es un tiempo de ejecución de JavaScript.

El servidor Node.js se utiliza para ejecutar código JavaScript.

Se accede a la aplicación Nest.js mediante un navegador web.

El navegador web se utiliza para acceder a la aplicación Nest.js.

El navegador web se utiliza para enviar solicitudes HTTP a la aplicación Nest.js.

Se accede a la aplicación Nest.js en http://localhost:3000.

# Información adicional

Nest.js es un marco de Node.js para crear aplicaciones escalables del lado del servidor. Utiliza JavaScript moderno, está construido con TypeScript (que se compila en JavaScript) y combina elementos de programación orientada a objetos, programación funcional y programación reactiva.

Las aplicaciones Nest.js están organizadas en un conjunto de módulos anidados. Los módulos de Nest.js son equivalentes a los módulos de Angular y se utilizan para agrupar componentes, servicios, canalizaciones y directivas relacionados.

El objetivo principal de un módulo Nest.js es proporcionar un lugar único (o raíz) donde se pueda encontrar todo el código relacionado para una función o dominio único. Esto facilita el razonamiento y el mantenimiento de las aplicaciones Nest.js.

Los módulos de Nest.js están organizados en una estructura jerárquica con un módulo raíz y cero o más módulos secundarios. El módulo raíz es el punto de entrada de la aplicación y normalmente se usa para configurar la aplicación Nest.js. Los módulos secundarios se utilizan para agrupar código relacionado para una característica o dominio.

La siguiente figura muestra la estructura típica de una aplicación Nest.js. El directorio src contiene el código fuente de la aplicación. El archivo app.module.ts es el módulo raíz y se usa para configurar la aplicación Nest.js. Los módulos secundarios se utilizan para agrupar código relacionado para una característica o dominio.

![Figura 1. La estructura típica de una aplicación Nest.js](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/img/app-structure.png)

El archivo src/app.module.ts es el módulo raíz y se usa para configurar la aplicación Nest.js. El módulo @Nestjs/common se importa y se usa para proporcionar la clase CommonModule. La clase CommonModule se utiliza para proporcionar el servicio de inyector. El servicio del inyector se utiliza para resolver dependencias.

El módulo @Nestjs/core se importa y se utiliza para proporcionar la clase NestFactory. La clase NestFactory se usa para crear una instancia de aplicación Nest.js.

La clase AppModule se importa y se usa para definir la clase AppModule. La clase AppModule se usa para configurar la aplicación Nest.js.

La clase AppModule se anota con el decorador @Module(). El decorador @Module() se usa para definir un módulo Nest.js.

La clase AppModule se importa y se usa para definir la clase AppModule. La clase AppModule se usa para configurar la aplicación Nest.js.

La clase AppModule se anota con el decorador @Module(). El decorador @Module() se usa para definir un módulo Nest.js.

La clase AppModule contiene un constructor y un método configure(). El constructor se utiliza para inyectar las dependencias. El método configure() se usa para configurar la aplicación Nest.js.

El archivo src/app.controller.ts se usa para definir la clase AppController. La clase AppController se usa para manejar solicitudes HTTP.

La clase AppController se anota con el decorador @Controller(). El decorador @Controller() se usa para definir un controlador Nest.js.

La clase AppController contiene un método root(). El método root() se usa para manejar solicitudes HTTP GET.

El archivo src/app.service.ts se usa para definir la clase AppService. La clase AppService se usa para proporcionar los datos para el controlador.

La clase AppService se anota con el decorador @Injectable(). El decorador @Injectable() se usa para definir un servicio Nest.js.

La clase AppService contiene un método getData(). El método getData() se usa para devolver los datos para el controlador.

El archivo src/environments/environment.ts se utiliza para definir las variables de entorno. Las variables de entorno se utilizan para configurar la aplicación Nest.js.

Las variables de entorno se inyectan en la clase AppModule mediante la función environment().

La función environment() se utiliza para inyectar las variables de entorno en la aplicación Nest.js.

La función environment() toma un objeto como argumento. El objeto contiene las variables de entorno.

La función Environment() devuelve un objeto Environment. El objeto Environment contiene las variables de entorno.

El objeto Environment se usa para configurar la aplicación Nest.js.

El archivo src/main.ts es el punto de entrada para la aplicación Nest.js. El archivo src/main.ts se usa para crear una instancia de la aplicación Nest.js.

El archivo src/main.ts importa la clase AppModule. La clase AppModule se usa para configurar la aplicación Nest.js.

El archivo src/main.ts usa la clase NestFactory para crear una instancia de la aplicación Nest.js.

La clase NestFactory se importa desde el módulo @nestjs/core. La clase NestFactory se usa para crear una instancia de aplicación Nest.js.

La clase NestFactory toma la clase AppModule como argumento. La clase AppModule se usa para configurar la aplicación Nest.js.

La clase NestFactory devuelve una instancia de la aplicación Nest.js.

La instancia de la aplicación Nest.js se utiliza para iniciar la aplicación Nest.js.

La instancia de la aplicación Nest.js se inicia con el método start().

El método start() se usa para iniciar la aplicación Nest.js.

El método start() toma un número de puerto como argumento. El número de puerto se utiliza para escuchar solicitudes HTTP.

El método start() devuelve una Promesa. La Promesa se resuelve cuando se inicia la aplicación Nest.js.

El archivo src/index.ts es el punto de entrada para el compilador de TypeScript. El archivo src/index.ts se usa para compilar el código TypeScript.

El archivo src/index.ts importa la clase AppModule. La clase AppModule se usa para configurar la aplicación Nest.js.

El archivo src/index.ts usa el archivo tsconfig.json para configurar el compilador de TypeScript.

El archivo tsconfig.json se usa para configurar el compilador de TypeScript.

El archivo tsconfig.json contiene las opciones del compilador. Las opciones del compilador se utilizan para configurar el compilador de TypeScript.

El archivo tsconfig.json se usa para compilar el código TypeScript en código JavaScript.

El código TypeScript se compila en código JavaScript usando el comando tsc.

El comando tsc se usa para compilar el código TypeScript en código JavaScript.

El comando tsc toma el archivo tsconfig.json como argumento. El archivo tsconfig.json se usa para configurar el compilador de TypeScript.

El comando tsc compila el código TypeScript en código JavaScript.

El código JavaScript compilado se coloca en el directorio dist.

El directorio dist contiene el código JavaScript compilado.

El directorio dist es el directorio de salida para el compilador de TypeScript.

La aplicación Nest.js se ejecuta con el comando de nodo.

El comando de nodo se usa para ejecutar la aplicación Nest.js.

El comando de nodo toma el código JavaScript compilado como argumento. El código JavaScript compilado se coloca en el directorio dist.

El comando de nodo ejecuta la aplicación Nest.js.

La aplicación Nest.js se ejecuta en un servidor Node.js.

El servidor Node.js se utiliza para ejecutar la aplicación Nest.js.

El servidor Node.js es un tiempo de ejecución de JavaScript.

El servidor Node.js se utiliza para ejecutar código JavaScript.

Se accede a la aplicación Nest.js mediante un navegador web.

El navegador web se utiliza para acceder a la aplicación Nest.js.

El navegador web se utiliza para enviar solicitudes HTTP a la aplicación Nest.js.

Se accede a la aplicación Nest.js en http://localhost:3000.