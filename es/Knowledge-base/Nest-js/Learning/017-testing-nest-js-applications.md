---
title: 017: Prueba de aplicaciones Nest.js
description: 
published: true
date: 2023-02-10T19:55:52.670Z
tags: 
editor: markdown
dateCreated: 2023-02-10T19:55:50.996Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [017: Testing Nest.js applications***English** document is available*](/en/Knowledge-base/Nest-js/Learning/017-testing-nest-js-applications)
{.links-list}


## Introducción

En esta publicación, veremos cómo probar las aplicaciones Nest.js. Nest.js es un marco de Node.js para crear aplicaciones del lado del servidor.

Las aplicaciones de Nest.js son fáciles de probar, ya que están construidas con componentes modulares y comprobables. En esta publicación, repasaremos algunas de las diferentes formas de probar las aplicaciones de Nest.js.

## Examen de la unidad

La prueba unitaria es un tipo de prueba donde se prueban unidades individuales de código. En Nest.js, las unidades de código suelen ser métodos en servicios o controladores.

Para realizar una prueba unitaria de una aplicación Nest.js, necesitamos:

1. Importar el módulo que queremos probar
2. Crea una instancia de la clase que queremos probar
3. Llame al método que queremos probar y afirme que se devuelve el resultado esperado

Veamos un ejemplo. Supongamos que tenemos un servicio Nest.js simple que suma dos números. El código para este servicio se vería así:

```javascript
export class CalculatorService {
  public add(a: number, b: number): number {
    return a + b;
  }
}
```

Podemos probar la unidad de este servicio haciendo lo siguiente:

```javascript
import { Test, TestingModule } from '@nestjs/testing';
import { CalculatorService } from './calculator.service';

describe('CalculatorService', () => {
  let service: CalculatorService;
  
  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      providers: [CalculatorService],
    }).compile();
    
    service = module.get<CalculatorService>(CalculatorService);
  });
  
  it('should add two numbers together', () => {
    const result = service.add(1, 2);
    
    expect(result).toEqual(3);
  });
});
```

En el código anterior, nosotros:

1. Importado el módulo que queremos probar
2. Creó una instancia de la clase que queremos probar
3. Llamado al método que queremos probar y afirmado que se devuelve el resultado esperado

Este es un ejemplo simple, pero muestra cómo podemos realizar una prueba unitaria de una aplicación Nest.js.

## Pruebas de integración

La prueba de integración es un tipo de prueba en la que se prueban juntas diferentes unidades de código. En Nest.js, las unidades de código suelen ser servicios o controladores.

Para probar la integración de una aplicación Nest.js, necesitamos:

1. Importar el módulo que queremos probar
2. Crea una instancia de la clase que queremos probar
3. Llame a los métodos que queremos probar y afirme que se devuelve el resultado esperado

Veamos un ejemplo. Supongamos que tenemos un servicio Nest.js simple que suma dos números y un controlador que llama a este servicio. El código para estos se vería así:

```javascript
// calculator.service.ts
export class CalculatorService {
  public add(a: number, b: number): number {
    return a + b;
  }
}
```

```javascript
// calculator.controller.ts
import { Controller, Get, Query } from '@nestjs/common';
import { CalculatorService } from './calculator.service';

@Controller('calculator')
export class CalculatorController {
  constructor(private readonly calculatorService: CalculatorService) {}
  
  @Get()
  public add(@Query('a') a: number, @Query('b') b: number): number {
    return this.calculatorService.add(a, b);
  }
}
```

Podemos probar la integración de este controlador haciendo lo siguiente:

```javascript
import { Test, TestingModule } from '@nestjs/testing';
import { CalculatorController } from './calculator.controller';
import { CalculatorService } from './calculator.service';

describe('CalculatorController', () => {
  let controller: CalculatorController;
  
  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      controllers: [CalculatorController],
      providers: [CalculatorService],
    }).compile();
    
    controller = module.get<CalculatorController>(CalculatorController);
  });
  
  it('should add two numbers together', () => {
    const result = controller.add(1, 2);
    
    expect(result).toEqual(3);
  });
});
```

En el código anterior, nosotros:

1. Importado el módulo que queremos probar
2. Creó una instancia de la clase que queremos probar
3. Llamamos a los métodos que queremos probar y afirmamos que se devuelve el resultado esperado

Este es un ejemplo simple, pero muestra cómo podemos probar la integración de una aplicación Nest.js.

## Pruebas de extremo a extremo

La prueba de extremo a extremo es un tipo de prueba en la que se prueba toda la aplicación de principio a fin. En Nest.js, esto significa probar la aplicación desde la solicitud http hasta la respuesta.

Para probar una aplicación Nest.js de extremo a extremo, necesitamos:

1. Importar el módulo que queremos probar
2. Crea una instancia de la clase que queremos probar
3. Llame a los métodos que queremos probar y afirme que se devuelve el resultado esperado

Veamos un ejemplo. Supongamos que tenemos una aplicación Nest.js simple que tiene un controlador que devuelve una lista de usuarios. El código para este controlador se vería así:

```javascript
import { Controller, Get } from '@nestjs/common';
import { User } from './user.entity';
import { UserService } from './user.service';

@Controller('users')
export class UserController {
  constructor(private readonly userService: UserService) {}
  
  @Get()
  public findAll(): User[] {
    return this.userService.findAll();
  }
}
```

Podemos probar este controlador de extremo a extremo haciendo lo siguiente:

```javascript
import { Test, TestingModule } from '@nestjs/testing';
import { UserController } from './user.controller';
import { UserService } from './user.service';

describe('UserController', () => {
  let controller: UserController;
  
  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      controllers: [UserController],
      providers: [UserService],
    }).compile();
    
    controller = module.get<UserController>(UserController);
  });
  
  it('should return a list of users', () => {
    const result = controller.findAll();
    
    expect(result).toEqual([{ id: 1, name: 'John Doe' }, { id: 2, name: 'Jane Doe' }]);
  });
});
```

En el código anterior, nosotros:

1. Importado el módulo que queremos probar
2. Creó una instancia de la clase que queremos probar
3. Llamamos a los métodos que queremos probar y afirmamos que se devuelve el resultado esperado

Este es un ejemplo simple, pero muestra cómo podemos probar una aplicación Nest.js de extremo a extremo.

## Conclusión

En esta publicación, analizamos cómo probar las aplicaciones Nest.js. Las aplicaciones de Nest.js son fáciles de probar, ya que están construidas con componentes modulares y comprobables.

Hemos analizado tres tipos diferentes de pruebas: pruebas unitarias, pruebas de integración y pruebas de extremo a extremo. Cada tipo de prueba tiene sus propias ventajas y desventajas, por lo que es importante elegir el tipo de prueba adecuado para sus necesidades.

Si recién está comenzando con las pruebas, las pruebas unitarias son un buen lugar para comenzar. Una vez que se sienta más cómodo con las pruebas, puede pasar a la integración y las pruebas de un extremo a otro.