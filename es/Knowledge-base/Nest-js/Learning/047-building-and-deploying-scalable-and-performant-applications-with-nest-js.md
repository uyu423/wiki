---
title: 047: Creación e implementación de aplicaciones escalables y de alto rendimiento con Nest.js
description: 
published: true
date: 2023-02-15T17:32:54.227Z
tags: 
editor: markdown
dateCreated: 2023-02-15T17:32:52.152Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [047: Building and deploying scalable and performant applications with Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/047-building-and-deploying-scalable-and-performant-applications-with-nest-js)
{.links-list}


# nido.js

Nest.js es un marco para crear aplicaciones escalables y de alto rendimiento con Node.js. Está inspirado en Angular y proporciona un poderoso conjunto de herramientas para crear aplicaciones del lado del servidor. En esta publicación, veremos cómo comenzar con Nest.js y cómo crear e implementar una aplicación escalable y de alto rendimiento con él.

## Empezando

Para comenzar con Nest.js, deberá instalar la CLI de Nest.js. Puedes hacer esto con npm:

```
npm install -g @nestjs/cli
```

Una vez que haya instalado la CLI de Nest.js, puede crear un nuevo proyecto de Nest.js con el siguiente comando:

```
nest new my-project
```

Esto creará un nuevo directorio llamado ```my-project``` con la estructura básica del proyecto Nest.js dentro.

## estructura del proyecto

Un proyecto Nest.js tiene la siguiente estructura básica:

```
my-project
├── src
│   ├── app.controller.ts
│   ├── app.module.ts
│   ├── app.service.ts
│   ├── main.ts
│   └── ...
├── test
│   ├── app.controller.spec.ts
│   ├── app.service.spec.ts
│   └── ...
├── .gitignore
├── nest-cli.json
├── package-lock.json
└── package.json
```

El directorio ```src``` contiene el código fuente de su aplicación. El archivo ```app.controller.ts``` contiene el controlador para su aplicación. El archivo ```app.module.ts``` contiene la definición del módulo para su aplicación. El archivo ```app.service.ts``` contiene el servicio para su aplicación. El archivo ```main.ts``` es el punto de entrada para su aplicación.

El directorio ```test``` contiene las pruebas unitarias para su aplicación. El archivo ```app.controller.spec.ts``` contiene las pruebas unitarias para el controlador. El archivo ```app.service.spec.ts``` contiene las pruebas unitarias para el servicio.

El archivo ```.gitignore``` contiene los patrones de los archivos que Git debe ignorar.

El archivo ```nest-cli.json``` contiene la configuración para la CLI de Nest.js.

El archivo ```package-lock.json``` contiene las versiones de dependencia para su proyecto.

El archivo ```package.json``` contiene los metadatos de su proyecto.

## Escribir código

Ahora que tiene una comprensión básica de la estructura del proyecto, echemos un vistazo a cómo escribir código en Nest.js.

### Controladores

Los controladores son responsables de manejar las solicitudes HTTP entrantes y devolver las respuestas. En Nest.js, los controladores se definen usando el decorador ```@Controller()```.

Aquí hay un controlador de ejemplo que maneja solicitudes GET a la ruta ```/hello```:

```javascript
@Controller('hello')
export class HelloController {

  @Get()
  hello() {
    return 'Hello, world!';
  }

}
```

En este ejemplo, el decorador ```@Controller('hello')``` define el controlador con el nombre ```hello```. El decorador ```@Get()``` define un controlador para solicitudes GET. El método ```hello()``` es la función controladora que devuelve la cadena ```Hello, world!```.

### Servicios

Los servicios son singletons que se encargan de encapsular la lógica empresarial. En Nest.js, los servicios se definen mediante el decorador ```@Injectable()```.

Aquí hay un servicio de ejemplo que tiene un método para generar un saludo:

```javascript
@Injectable()
export class HelloService {

  generateGreeting(name: string) {
    return `Hello, ${name}!`;
  }

}
```

En este ejemplo, el decorador ```@Injectable()``` define el servicio como inyectable. El método ```generateGreeting()``` toma un parámetro ```name``` y devuelve una cadena de saludo.

### Módulos

Los módulos se utilizan para organizar la funcionalidad relacionada en Nest.js. En Nest.js, los módulos se definen usando el decorador ```@Module()```.

Aquí hay un módulo de ejemplo que define un controlador y un servicio:

```javascript
@Module({
  controllers: [HelloController],
  providers: [HelloService],
})
export class HelloModule {}
```

En este ejemplo, el decorador ```@Module()``` define el módulo con ```HelloController``` y ```HelloService```.

## Construcción e implementación

Ahora que ha visto cómo escribir código en Nest.js, echemos un vistazo a cómo crear e implementar una aplicación Nest.js.

### Edificio

Para crear una aplicación Nest.js, deberá usar la CLI de Nest.js. La CLI de Nest.js proporciona un comando ```build``` que se puede usar para crear una aplicación Nest.js.

Para crear una aplicación Nest.js, deberá ejecutar el siguiente comando:

```
nest build
```

Esto creará la aplicación Nest.js y enviará los archivos compilados al directorio ```dist```.

### Desplegando

Para implementar una aplicación Nest.js, deberá utilizar un proveedor de alojamiento de Node.js. Hay muchos proveedores de alojamiento de Node.js para elegir, pero recomendamos usar [Heroku](https://www.heroku.com/).

Heroku ofrece un nivel gratuito que puede usar para implementar su aplicación Nest.js. Para implementar su aplicación en Heroku, deberá crear un ```Procfile``` en la raíz de su proyecto. El ```Procfile``` se usa para decirle a Heroku cómo ejecutar su aplicación.

Aquí hay un ```Procfile``` de ejemplo para una aplicación Nest.js:

```
web: nest start
```

En este ejemplo, el tipo de proceso ```web``` se usa para decirle a Heroku que se trata de una aplicación web. El comando ```nest start``` se utiliza para iniciar la aplicación Nest.js.

Una vez que haya creado el ```Procfile```, puede implementar su aplicación Nest.js en Heroku con el siguiente comando:

```
git push heroku master
```

Esto enviará su código a Heroku y activará una nueva implementación.

## Conclusión

En esta publicación, analizamos cómo comenzar con Nest.js y cómo crear e implementar una aplicación escalable y de alto rendimiento con él. Nest.js es un marco poderoso para crear aplicaciones del lado del servidor y esperamos que esta publicación le haya brindado una buena introducción.