---
title: 020: Uso de canalizaciones para la transformación de datos en Nest.js
description: 
published: true
date: 2023-02-09T15:17:23.593Z
tags: 
editor: markdown
dateCreated: 2023-02-09T15:17:21.912Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [020: Using pipes for data transformation in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/020-using-pipes-for-data-transformation-in-nest-js)
{.links-list}


# Usar tuberías para la transformación de datos en Nest.js

En Nest.js, las canalizaciones se utilizan para la transformación de datos. Las tuberías toman datos como entrada y devuelven los datos transformados como salida.

Las tuberías se pueden utilizar para una variedad de tareas, tales como:

- Validación
- Formateo
- Transformación

Las tuberías se pueden crear usando el decorador `@ Pipe`. El decorador `@ Pipe` toma el nombre de la tubería como argumento.

```javascript
@ Pipe({
  name: 'myPipe'
})
```

Las tuberías se pueden encadenar usando el método `.pipe()`. El método `.pipe()` toma el nombre de la tubería como argumento.

```javascript
.pipe(myPipe)
```

Las tuberías se pueden usar en los controladores y servicios de Nest.js. Para usar una tubería en un controlador, se puede usar el decorador `@ UsePipes`. El decorador `@ UsePipes` toma el nombre de la tubería como argumento.

```javascript
@ UsePipes(myPipe)
```

Para usar una tubería en un servicio, se puede usar el método `.usePipe()`. El método `.usePipe()` toma el nombre de la tubería como argumento.

```javascript
.usePipe(myPipe)
```

## Creando una tubería

Para crear una tubería, se puede usar el decorador `@ Pipe`. El decorador `@ Pipe` toma el nombre de la tubería como argumento.

```javascript
@ Pipe({
  name: 'myPipe'
})
```

Las tuberías deben tener un método `transform()`. El método `transform()` toma los datos a transformar como un argumento y devuelve los datos transformados.

```javascript
transform(data: any) {
  return data;
}
```

## Encadenamiento de tuberías

Las tuberías se pueden encadenar usando el método `.pipe()`. El método `.pipe()` toma el nombre de la tubería como argumento.

```javascript
.pipe(myPipe)
```

## Uso de tuberías en controladores

Las tuberías se pueden usar en los controladores y servicios de Nest.js. Para usar una tubería en un controlador, se puede usar el decorador `@ UsePipes`. El decorador `@ UsePipes` toma el nombre de la tubería como argumento.

```javascript
@ UsePipes(myPipe)
```

## Uso de tuberías en servicios

Para usar una tubería en un servicio, se puede usar el método `.usePipe()`. El método `.usePipe()` toma el nombre de la tubería como argumento.

```javascript
.usePipe(myPipe)
```

## Ejemplo

En este ejemplo, se creará una tubería que toma una cadena y la devuelve en todas las letras mayúsculas.

```javascript
@ Pipe({
  name: 'uppercasePipe'
})
export class UppercasePipe implements PipeTransform {
  transform(data: string) {
    return data.toUpperCase();
  }
}
```

Esta tubería se puede usar en un controlador así:

```javascript
@ Controller('/')
@ UsePipes(UppercasePipe)
export class MyController {
  @ Get('/')
  getData(@ Req() request: Request) {
    return {
      data: 'Hello, world!'
    };
  }
}
```

## Información adicional

- [Tuberías Nest.js](https://docs.nestjs.com/pipes)
- [Nest.js UsePipes](https://docs.nestjs.com/use-pipes)

## Advertencias

- Las tuberías se ejecutan en el orden en que se encadenan.

## Peligros

- Si una tubería arroja un error, la ejecución de la cadena de tuberías se detendrá.