---
title: 054: uso de Nest.js con aplicaciones web progresivas (PWA)
description: 
published: true
date: 2023-02-05T15:18:28.523Z
tags: 
editor: markdown
dateCreated: 2023-02-05T15:18:23.092Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [054: Using Nest.js with Progressive Web Apps (PWA)***English** document is available*](/en/Knowledge-base/Nest-js/Learning/054-using-nest-js-with-progressive-web-apps-pwa)
{.links-list}


# Uso de Nest.js con aplicaciones web progresivas (PWA)

En esta publicación, veremos cómo usar Nest.js con Progressive Web Apps (PWA).

Las aplicaciones web progresivas son aplicaciones web que utilizan tecnologías web modernas para proporcionar una experiencia de usuario similar a la de una aplicación móvil nativa.

Nest.js es un marco de Node.js que facilita la creación de aplicaciones escalables del lado del servidor.

## ¿Por qué usar Nest.js con aplicaciones web progresivas?

Existen algunas razones por las que es posible que desee utilizar Nest.js con Progressive Web Apps.

Primero, las aplicaciones de Nest.js son fáciles de escalar. Esto es importante para las aplicaciones web progresivas, que deben poder manejar una gran cantidad de usuarios.

En segundo lugar, las aplicaciones Nest.js son fáciles de desarrollar. Esto es importante porque las aplicaciones web progresivas deben poder desarrollarse de manera rápida y eficiente.

Tercero, Nest.js tiene un gran soporte para TypeScript. Esto es importante porque TypeScript es un superconjunto escrito de JavaScript que facilita el desarrollo de aplicaciones a gran escala.

En cuarto lugar, las aplicaciones de Nest.js son fáciles de probar. Esto es importante porque las aplicaciones web progresivas deben poder probarse de manera rápida y eficiente.

Finalmente, Nest.js tiene un gran soporte para estándares web. Esto es importante porque las aplicaciones web progresivas deben poder construirse utilizando estándares web.

## Empezando

Ahora que hemos visto algunas de las razones por las que podría querer usar Nest.js con Progressive Web Apps, veamos cómo empezar.

Primero, deberá instalar la CLI de Nest.js.

```
$ npm install -g @nestjs/cli
```

A continuación, deberá crear un nuevo proyecto Nest.js.

```
$ nest new my-project
```

Una vez que se haya creado el proyecto, deberá instalar las siguientes dependencias.

```
$ npm install --save @nestjs/pwa
$ npm install --save @angular/pwa
$ npm install --save workbox-build
```

Ahora que se han instalado las dependencias, deberá crear un archivo llamado `nest-cli.json` en la raíz de su proyecto. Este archivo contendrá la siguiente configuración.

```json
{
  "collection": "@nestjs/schematics",
  "sourceRoot": "src",
  "compilerOptions": {
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "target": "es5",
    "module": "commonjs",
    "lib": [
      "es2015",
      "dom"
    ]
  }
}
```

A continuación, deberá crear un archivo llamado `angular.json` en la raíz de su proyecto. Este archivo contendrá la siguiente configuración.

```json
{
  "$schema": "./node_modules/@angular/cli/lib/config/schema.json",
  "version": 1,
  "newProjectRoot": "projects",
  "projects": {
    "my-project": {
      "root": "",
      "sourceRoot": "src",
      "projectType": "application",
      "prefix": "app",
      "schematics": {},
      "architect": {
        "build": {
          "builder": "@angular-devkit/build-angular:browser",
          "options": {
            "outputPath": "dist/my-project",
            "index": "src/index.html",
            "main": "src/main.ts",
            "polyfills": "src/polyfills.ts",
            "tsConfig": "src/tsconfig.app.json",
            "assets": [
              "src/favicon.ico",
              "src/assets"
            ],
            "styles": [
              "src/styles.css"
            ],
            "scripts": []
          },
          "configurations": {
            "production": {
              "fileReplacements": [
                {
                  "replace": "src/environments/environment.ts",
                  "with": "src/environments/environment.prod.ts"
                }
              ],
              "optimization": true,
              "outputHashing": "all",
              "sourceMap": false,
              "extractCss": true,
              "namedChunks": false,
              "aot": true,
              "extractLicenses": true,
              "vendorChunk": false,
              "buildOptimizer": true,
              "budgets": [
                {
                  "type": "initial",
                  "maximumWarning": "2mb",
                  "maximumError": "5mb"
                },
                {
                  "type": "anyComponentStyle",
                  "maximumWarning": "6kb",
                  "maximumError": "10kb"
                }
              ]
            }
          }
        },
        "serve": {
          "builder": "@angular-devkit/build-angular:dev-server",
          "options": {
            "browserTarget": "my-project:build"
          },
          "configurations": {
            "production": {
              "browserTarget": "my-project:build:production"
            }
          }
        },
        "extract-i18n": {
          "builder": "@angular-devkit/build-angular:extract-i18n",
          "options": {
            "browserTarget": "my-project:build"
          }
        },
        "test": {
          "builder": "@angular-devkit/build-angular:karma",
          "options": {
            "main": "src/test.ts",
            "polyfills": "src/polyfills.ts",
            "tsConfig": "src/tsconfig.spec.json",
            "karmaConfig": "src/karma.conf.js",
            "styles": [
              "src/styles.css"
            ],
            "scripts": [],
            "assets": [
              "src/favicon.ico",
              "src/assets"
            ]
          }
        },
        "lint": {
          "builder": "@angular-devkit/build-angular:tslint",
          "options": {
            "tsConfig": [
              "src/tsconfig.app.json",
              "src/tsconfig.spec.json"
            ],
            "exclude": [
              "**/node_modules/**"
            ]
          }
        }
      }
    },
    "my-project-e2e": {
      "root": "e2e/",
      "projectType": "application",
      "architect": {
        "e2e": {
          "builder": "@angular-devkit/build-angular:protractor",
          "options": {
            "protractorConfig": "e2e/protractor.conf.js",
            "devServerTarget": "my-project:serve"
          },
          "configurations": {
            "production": {
              "protractorConfig": "e2e/protractor.prod.conf.js",
              "devServerTarget": "my-project:serve:production"
            }
          }
        },
        "lint": {
          "builder": "@angular-devkit/build-angular:tslint",
          "options": {
            "tsConfig": "e2e/tsconfig.e2e.json",
            "exclude": [
              "**/node_modules/**"
            ]
          }
        }
      }
    }
  },
  "defaultProject": "my-project"
}
```

A continuación, deberá crear un archivo llamado `polyfills.ts` en el directorio `src`. Este archivo contendrá el siguiente código.

```typescript
import 'core-js/es6';
import 'core-js/es7/reflect';
import 'zone.js/dist/zone';

if (process.env.ENV === 'production') {
  // Production
} else {
  // Development and test
  Error['stackTraceLimit'] = Infinity;
  require('zone.js/dist/long-stack-trace-zone');
}
```

A continuación, deberá crear un archivo llamado `main.ts` en el directorio `src`. Este archivo contendrá el siguiente código.

```typescript
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';
import { environment } from './environments/environment';

if (environment.production) {
  enableProdMode();
}

platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.log(err));
```

A continuación, deberá crear un archivo llamado `app.module.ts` en el directorio `src/app`. Este archivo contendrá el siguiente código.

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule, Injector } from '@angular/core';
import { createCustomElement } from '@angular/elements';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule
  ],
  entryComponents: [
    AppComponent
  ]
})
export class AppModule {
  constructor(private injector: Injector) {
    const el = createCustomElement(AppComponent, { injector: this.injector });
    customElements.define('my-app', el);
  }

  ngDoBootstrap() {}
}
```

A continuación, deberá crear un archivo llamado `app.component.ts` en el directorio `src/app`. Este archivo contendrá el siguiente código.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: [ './app.component.css' ]
})
export class AppComponent  {
  name = 'Angular';
}
```

A continuación, deberá crear un archivo llamado `app.component.html` en el directorio `src/app`. Este archivo contendrá el siguiente código.

```html
<h1>Hello {{ name }}!</h1>
```

A continuación, deberá crear un archivo llamado `app.component.css` en el directorio `src/app`. Este archivo contendrá el siguiente código.

```css
h1 {
  color: #369;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 250%;
}
```

Ahora que se ha configurado el proyecto, puede ejecutar el siguiente comando para iniciar el servidor de desarrollo.

```
$ nest start
```

## Construyendo la Aplicación

Ahora que se ha configurado el proyecto, puede ejecutar el siguiente comando para compilar la aplicación.

```
$ nest build
```

## Servir la aplicación

Ahora que se ha creado el proyecto, puede ejecutar el siguiente comando para servir la aplicación.

```
$ nest serve
```

## Prueba de la aplicación

Ahora que se ha servido el proyecto, puede ejecutar el siguiente comando para probar la aplicación.

```
$ nest test
```

## Conclusión

En esta publicación, hemos visto cómo usar Nest.js con Progressive Web Apps. Hemos visto cómo se puede usar Nest.js para crear fácilmente aplicaciones escalables del lado del servidor. También hemos visto cómo se puede usar Nest.js para desarrollar fácilmente aplicaciones web progresivas.