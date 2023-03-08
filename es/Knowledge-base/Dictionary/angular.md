---
title: Angular
description: 
published: true
date: 2023-02-10T11:17:58.802Z
tags: 
editor: markdown
dateCreated: 2023-02-10T11:17:56.954Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Angular***English** document is available*](/en/Knowledge-base/Dictionary/angular)
{.links-list}


# Angular

## Descripción general
Angular es un marco de aplicación web de código abierto creado y mantenido por Google. Se utiliza para desarrollar aplicaciones web de una sola página y aplicaciones móviles. Está escrito en TypeScript y se basa en el patrón de diseño Modelo-Vista-Controlador (MVC).

## Descripción
Angular es un marco para desarrollar aplicaciones web y se basa en el patrón de diseño Modelo-Vista-Controlador (MVC). Está escrito en TypeScript y es mantenido por Google. Está diseñado para ser utilizado para desarrollar aplicaciones de una sola página, así como aplicaciones móviles.

Angular se compone de varios componentes, incluidos Angular CLI (Command Line Interface), Angular Compiler y Angular Core. La CLI de Angular se usa para crear y administrar proyectos de Angular, mientras que el Compilador de Angular se usa para compilar código TypeScript. Angular Core es el marco principal que contiene los componentes y servicios principales que se utilizan para crear aplicaciones.

Angular también incluye otras bibliotecas y herramientas, como Angular Router, que se usa para administrar el enrutamiento en las aplicaciones, y la biblioteca Angular Forms, que se usa para crear y administrar formularios.

## Características
Angular incluye varias funciones que lo convierten en una opción atractiva para el desarrollo de aplicaciones web y móviles. Estas características incluyen:

- Compatibilidad con TypeScript: Angular está escrito en TypeScript, que es un superconjunto de JavaScript. Esto permite a los desarrolladores utilizar las funciones más recientes del lenguaje, sin dejar de tener acceso a las funciones de JavaScript.

- Arquitectura basada en componentes: Angular utiliza una arquitectura basada en componentes, lo que permite a los desarrolladores crear componentes modulares y reutilizables. Esto facilita el mantenimiento y la escalabilidad de las aplicaciones.

- Modularización: Angular permite a los desarrolladores modularizar su código, lo que facilita la administración y el mantenimiento de las aplicaciones.

- Programación reactiva: Angular utiliza un modelo de programación reactiva, que permite a los desarrolladores crear aplicaciones que responden mejor a las entradas del usuario.

- Herramientas: Angular incluye varias herramientas que facilitan el desarrollo de aplicaciones, como Angular CLI, que se usa para crear y administrar proyectos, y Angular Compiler, que se usa para compilar código TypeScript.

## Ejemplo
El siguiente es un ejemplo de una aplicación Angular que muestra una lista de usuarios. La aplicación usa Angular CLI para crear el proyecto, Angular Router para administrar el enrutamiento y la biblioteca Angular Forms para crear y administrar formularios.

```
import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';
import { FormGroup, FormControl, Validators } from '@angular/forms';

@Component({
  selector: 'app-user-list',
  templateUrl: './user-list.component.html',
  styleUrls: ['./user-list.component.css']
})
export class UserListComponent implements OnInit {
  users: any[];
  userForm: FormGroup;

  constructor(private router: Router) { }

  ngOnInit() {
    this.userForm = new FormGroup({
      name: new FormControl('', Validators.required),
      email: new FormControl('', [Validators.required, Validators.email])
    });
  }

  onSubmit() {
    this.users.push(this.userForm.value);
    this.router.navigate(['/users']);
  }

}
```

## Pros y contras
Angular tiene varias ventajas y desventajas que deben tenerse en cuenta al elegir un marco.

**Pros:**

- Fácil de usar: Angular es relativamente fácil de usar y tiene una gran comunidad de desarrolladores que pueden brindar soporte y recursos.

- Modularización: Angular permite a los desarrolladores modularizar su código, lo que facilita el mantenimiento y la escala de las aplicaciones.

- Programación reactiva: Angular utiliza un modelo de programación reactiva, que permite a los desarrolladores crear aplicaciones que responden mejor a las entradas del usuario.

**Contras:**

- Curva de aprendizaje pronunciada: Angular tiene una curva de aprendizaje pronunciada y puede tomar algún tiempo dominar el marco.

- Complejidad: Angular puede ser bastante complejo y puede ser difícil depurar y solucionar problemas de aplicaciones.

- Rendimiento: las aplicaciones angulares pueden ser más lentas que las aplicaciones creadas con otros marcos, debido a la complejidad del marco.

## Tecnología relacionada
Angular está relacionado con varias otras tecnologías, como TypeScript, React y Vue.js. TypeScript es el lenguaje en el que está escrito Angular, y es un superconjunto de JavaScript. React y Vue.js son marcos JavaScript populares para crear aplicaciones web.

## Digresión
Angular es un marco de código abierto y muchas empresas y organizaciones lo utilizan para desarrollar aplicaciones web y móviles. Es una opción atractiva para los desarrolladores debido a su facilidad de uso y su compatibilidad con TypeScript y otras tecnologías.

## Otros
Angular ha crecido en popularidad desde su lanzamiento inicial en 2010, y ahora es uno de los marcos de aplicaciones web más populares. Es utilizado por muchas empresas, incluidas Google, Microsoft y Apple.