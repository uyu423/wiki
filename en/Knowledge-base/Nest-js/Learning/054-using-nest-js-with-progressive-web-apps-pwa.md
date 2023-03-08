---
title: 054: Using Nest.js with Progressive Web Apps (PWA)
description: 
published: true
date: 2023-02-05T15:18:24.783Z
tags: 
editor: markdown
dateCreated: 2023-02-05T15:18:23.094Z
---

- [054: uso de Nest.js con aplicaciones web progresivas (PWA)***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/054-using-nest-js-with-progressive-web-apps-pwa)
{.links-list}
- [054：将 Nest.js 与渐进式 Web 应用程序 (PWA) 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/054-using-nest-js-with-progressive-web-apps-pwa)
{.links-list}
- [054: PWA(프로그레시브 웹 앱)에서 Nest.js 사용***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/054-using-nest-js-with-progressive-web-apps-pwa)
{.links-list}


# Using Nest.js with Progressive Web Apps (PWA)

In this post, we'll be looking at how to use Nest.js with Progressive Web Apps (PWA).

Progressive Web Apps are web applications that make use of modern web technologies to provide a user experience similar to that of a native mobile app.

Nest.js is a Node.js framework that makes it easy to create scalable, server-side applications.

## Why Use Nest.js with Progressive Web Apps?

There are a few reasons why you might want to use Nest.js with Progressive Web Apps.

First, Nest.js applications are easy to scale. This is important for Progressive Web Apps, which need to be able to handle a large number of users.

Second, Nest.js applications are easy to develop. This is important because Progressive Web Apps need to be able to be developed quickly and efficiently.

Third, Nest.js has great support for TypeScript. This is important because TypeScript is a typed superset of JavaScript that makes it easier to develop large-scale applications.

Fourth, Nest.js applications are easy to test. This is important because Progressive Web Apps need to be able to be tested quickly and efficiently.

Finally, Nest.js has great support for web standards. This is important because Progressive Web Apps need to be able to be built using web standards.

## Getting Started

Now that we've seen some of the reasons why you might want to use Nest.js with Progressive Web Apps, let's look at how to get started.

First, you'll need to install the Nest.js CLI.

```
$ npm install -g @nestjs/cli
```

Next, you'll need to create a new Nest.js project.

```
$ nest new my-project
```

Once the project has been created, you'll need to install the following dependencies.

```
$ npm install --save @nestjs/pwa
$ npm install --save @angular/pwa
$ npm install --save workbox-build
```

Now that the dependencies have been installed, you'll need to create a file called `nest-cli.json` in the root of your project. This file will contain the following configuration.

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

Next, you'll need to create a file called `angular.json` in the root of your project. This file will contain the following configuration.

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

Next, you'll need to create a file called `polyfills.ts` in the `src` directory. This file will contain the following code.

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

Next, you'll need to create a file called `main.ts` in the `src` directory. This file will contain the following code.

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

Next, you'll need to create a file called `app.module.ts` in the `src/app` directory. This file will contain the following code.

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

Next, you'll need to create a file called `app.component.ts` in the `src/app` directory. This file will contain the following code.

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

Next, you'll need to create a file called `app.component.html` in the `src/app` directory. This file will contain the following code.

```html
<h1>Hello {{ name }}!</h1>
```

Next, you'll need to create a file called `app.component.css` in the `src/app` directory. This file will contain the following code.

```css
h1 {
  color: #369;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 250%;
}
```

Now that the project has been set up, you can run the following command to start the development server.

```
$ nest start
```

## Building the Application

Now that the project has been set up, you can run the following command to build the application.

```
$ nest build
```

## Serving the Application

Now that the project has been built, you can run the following command to serve the application.

```
$ nest serve
```

## Testing the Application

Now that the project has been served, you can run the following command to test the application.

```
$ nest test
```

## Conclusion

In this post, we've seen how to use Nest.js with Progressive Web Apps. We've seen how Nest.js can be used to easily create scalable, server-side applications. We've also seen how Nest.js can be used to easily develop Progressive Web Apps.