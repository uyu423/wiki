---
title: 054：将 Nest.js 与渐进式 Web 应用程序 (PWA) 结合使用
description: 
published: true
date: 2023-02-05T15:18:28.523Z
tags: 
editor: markdown
dateCreated: 2023-02-05T15:18:23.085Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [054: Using Nest.js with Progressive Web Apps (PWA)***English** document is available*](/en/Knowledge-base/Nest-js/Learning/054-using-nest-js-with-progressive-web-apps-pwa)
{.links-list}


# 将 Nest.js 与渐进式 Web 应用程序 (PWA) 结合使用

在这篇文章中，我们将研究如何将 Nest.js 与渐进式 Web 应用程序 (PWA) 结合使用。

渐进式 Web 应用程序是利用现代 Web 技术提供类似于本机移动应用程序的用户体验的 Web 应用程序。

Nest.js 是一个 Node.js 框架，可以轻松创建可扩展的服务器端应用程序。

## 为什么将 Nest.js 与渐进式 Web 应用程序一起使用？

您可能希望将 Nest.js 与 Progressive Web Apps 一起使用的原因有几个。

首先，Nest.js 应用程序易于扩展。这对于需要能够处理大量用户的 Progressive Web Apps 来说很重要。

其次，Nest.js 应用程序易于开发。这很重要，因为渐进式 Web 应用程序需要能够快速高效地开发。

第三，Nest.js 对 TypeScript 有很好的支持。这很重要，因为 TypeScript 是 JavaScript 的类型化超集，可以更轻松地开发大型应用程序。

第四，Nest.js 应用程序易于测试。这很重要，因为渐进式 Web 应用程序需要能够快速有效地进行测试。

最后，Nest.js 对网络标准有很好的支持。这很重要，因为渐进式 Web 应用程序需要能够使用 Web 标准构建。

## 入门

现在我们已经了解了您可能希望将 Nest.js 与渐进式 Web 应用程序一起使用的一些原因，让我们看看如何开始。

首先，您需要安装 Nest.js CLI。

```
$ npm install -g @nestjs/cli
```

接下来，您需要创建一个新的 Nest.js 项目。

```
$ nest new my-project
```

创建项目后，您需要安装以下依赖项。

```
$ npm install --save @nestjs/pwa
$ npm install --save @angular/pwa
$ npm install --save workbox-build
```

现在已经安装了依赖项，您需要在项目的根目录中创建一个名为“nest-cli.json”的文件。该文件将包含以下配置。

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

接下来，您需要在项目的根目录中创建一个名为“angular.json”的文件。该文件将包含以下配置。

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

接下来，您需要在 `src` 目录中创建一个名为 `polyfills.ts` 的文件。该文件将包含以下代码。

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

接下来，您需要在 `src` 目录中创建一个名为 `main.ts` 的文件。该文件将包含以下代码。

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

接下来，您需要在 `src/app` 目录中创建一个名为 `app.module.ts` 的文件。该文件将包含以下代码。

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

接下来，您需要在 `src/app` 目录中创建一个名为 `app.component.ts` 的文件。该文件将包含以下代码。

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

接下来，您需要在 `src/app` 目录中创建一个名为 `app.component.html` 的文件。该文件将包含以下代码。

```html
<h1>Hello {{ name }}!</h1>
```

接下来，您需要在 `src/app` 目录中创建一个名为 `app.component.css` 的文件。该文件将包含以下代码。

```css
h1 {
  color: #369;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 250%;
}
```

现在项目已经建立，您可以运行以下命令来启动开发服务器。

```
$ nest start
```

## 构建应用程序

现在项目已经设置好，您可以运行以下命令来构建应用程序。

```
$ nest build
```

## 服务应用程序

现在已经构建了项目，您可以运行以下命令来为应用程序提供服务。

```
$ nest serve
```

## 测试应用程序

现在项目已经服务，您可以运行以下命令来测试应用程序。

```
$ nest test
```

## 结论

在这篇文章中，我们了解了如何将 Nest.js 与渐进式 Web 应用程序结合使用。我们已经了解了如何使用 Nest.js 轻松创建可扩展的服务器端应用程序。我们还了解了如何使用 Nest.js 轻松开发渐进式 Web 应用程序。