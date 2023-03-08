---
title: 020: Using pipes for data transformation in Nest.js
description: 
published: true
date: 2023-02-09T15:17:28.103Z
tags: 
editor: markdown
dateCreated: 2023-02-09T15:17:21.916Z
---

- [020: Uso de canalizaciones para la transformación de datos en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/020-using-pipes-for-data-transformation-in-nest-js)
{.links-list}
- [020: 在 Nest.js 中使用管道进行数据转换***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/020-using-pipes-for-data-transformation-in-nest-js)
{.links-list}
- [020: Nest.js에서 데이터 변환을 위한 파이프 사용***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/020-using-pipes-for-data-transformation-in-nest-js)
{.links-list}


# Using pipes for data transformation in Nest.js

In Nest.js, pipes are used for data transformation. Pipes take in data as an input and return the transformed data as an output.

Pipes can be used for a variety of tasks such as:

- Validation
- Formatting
- Transformation

Pipes can be created using the `@ Pipe` decorator. The `@ Pipe` decorator takes in the name of the pipe as an argument.

```javascript
@ Pipe({
  name: 'myPipe'
})
```

Pipes can be chained together using the `.pipe()` method. The `.pipe()` method takes in the name of the pipe as an argument.

```javascript
.pipe(myPipe)
```

Pipes can be used in Nest.js controllers and services. To use a pipe in a controller, the `@ UsePipes` decorator can be used. The `@ UsePipes` decorator takes in the name of the pipe as an argument.

```javascript
@ UsePipes(myPipe)
```

To use a pipe in a service, the `.usePipe()` method can be used. The `.usePipe()` method takes in the name of the pipe as an argument.

```javascript
.usePipe(myPipe)
```

## Creating a pipe

To create a pipe, the `@ Pipe` decorator can be used. The `@ Pipe` decorator takes in the name of the pipe as an argument.

```javascript
@ Pipe({
  name: 'myPipe'
})
```

Pipes must have a `transform()` method. The `transform()` method takes in the data to be transformed as an argument and returns the transformed data.

```javascript
transform(data: any) {
  return data;
}
```

## Chaining pipes

Pipes can be chained together using the `.pipe()` method. The `.pipe()` method takes in the name of the pipe as an argument.

```javascript
.pipe(myPipe)
```

## Using pipes in controllers

Pipes can be used in Nest.js controllers and services. To use a pipe in a controller, the `@ UsePipes` decorator can be used. The `@ UsePipes` decorator takes in the name of the pipe as an argument.

```javascript
@ UsePipes(myPipe)
```

## Using pipes in services

To use a pipe in a service, the `.usePipe()` method can be used. The `.usePipe()` method takes in the name of the pipe as an argument.

```javascript
.usePipe(myPipe)
```

## Example

In this example, a pipe will be created that takes in a string and returns the string in all uppercase letters.

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

This pipe can be used in a controller like so:

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

## Additional Information

- [Nest.js Pipes](https://docs.nestjs.com/pipes)
- [Nest.js UsePipes](https://docs.nestjs.com/use-pipes)

## Warnings

- Pipes are executed in the order in which they are chained.

## Dangers

- If a pipe throws an error, the execution of the pipe chain will stop.