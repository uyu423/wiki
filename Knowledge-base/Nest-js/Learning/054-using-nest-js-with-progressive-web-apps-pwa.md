---
title: 054: PWA(프로그레시브 웹 앱)에서 Nest.js 사용
description: 
published: true
date: 2023-02-05T15:18:28.523Z
tags: 
editor: markdown
dateCreated: 2023-02-05T15:18:23.091Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [054: Using Nest.js with Progressive Web Apps (PWA)***English** document is available*](/en/Knowledge-base/Nest-js/Learning/054-using-nest-js-with-progressive-web-apps-pwa)
{.links-list}


# 프로그레시브 웹 앱(PWA)과 함께 Nest.js 사용

이 게시물에서는 PWA(Progressive Web App)와 함께 Nest.js를 사용하는 방법을 살펴보겠습니다.

프로그레시브 웹 앱은 최신 웹 기술을 활용하여 기본 모바일 앱과 유사한 사용자 경험을 제공하는 웹 애플리케이션입니다.

Nest.js는 확장 가능한 서버측 애플리케이션을 쉽게 만들 수 있는 Node.js 프레임워크입니다.

## 프로그레시브 웹 앱과 함께 Nest.js를 사용하는 이유는 무엇인가요?

프로그레시브 웹 앱과 함께 Nest.js를 사용하려는 몇 가지 이유가 있습니다.

첫째, Nest.js 애플리케이션은 확장하기 쉽습니다. 이것은 많은 수의 사용자를 처리할 수 있어야 하는 프로그레시브 웹 앱에 중요합니다.

둘째, Nest.js 애플리케이션은 개발하기 쉽습니다. 프로그레시브 웹 앱은 빠르고 효율적으로 개발할 수 있어야 하기 때문에 이는 중요합니다.

셋째, Nest.js는 TypeScript를 크게 지원합니다. TypeScript는 대규모 애플리케이션을 더 쉽게 개발할 수 있게 해주는 JavaScript의 형식화된 상위 집합이기 때문에 이는 중요합니다.

넷째, Nest.js 애플리케이션은 테스트하기 쉽습니다. 프로그레시브 웹 앱은 빠르고 효율적으로 테스트할 수 있어야 하므로 이는 중요합니다.

마지막으로 Nest.js는 웹 표준을 훌륭하게 지원합니다. 프로그레시브 웹 앱은 웹 표준을 사용하여 구축할 수 있어야 하기 때문에 이는 중요합니다.

## 시작하기

이제 Progressive Web Apps와 함께 Nest.js를 사용하려는 몇 가지 이유를 살펴보았으므로 시작하는 방법을 살펴보겠습니다.

먼저 Nest.js CLI를 설치해야 합니다.

```
$ npm install -g @nestjs/cli
```

다음으로 새 Nest.js 프로젝트를 만들어야 합니다.

```
$ nest new my-project
```

프로젝트가 생성되면 다음 종속 항목을 설치해야 합니다.

```
$ npm install --save @nestjs/pwa
$ npm install --save @angular/pwa
$ npm install --save workbox-build
```

이제 종속성이 설치되었으므로 프로젝트의 루트에 `nest-cli.json`이라는 파일을 만들어야 합니다. 이 파일에는 다음 구성이 포함됩니다.

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

다음으로 프로젝트의 루트에 `angular.json`이라는 파일을 만들어야 합니다. 이 파일에는 다음 구성이 포함됩니다.

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

다음으로 `src` 디렉토리에 `polyfills.ts`라는 파일을 만들어야 합니다. 이 파일에는 다음 코드가 포함됩니다.

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

다음으로 `src` 디렉토리에 `main.ts`라는 파일을 만들어야 합니다. 이 파일에는 다음 코드가 포함됩니다.

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

다음으로 `src/app` 디렉토리에 `app.module.ts`라는 파일을 만들어야 합니다. 이 파일에는 다음 코드가 포함됩니다.

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

다음으로 `src/app` 디렉토리에 `app.component.ts`라는 파일을 만들어야 합니다. 이 파일에는 다음 코드가 포함됩니다.

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

다음으로 `src/app` 디렉토리에 `app.component.html`이라는 파일을 만들어야 합니다. 이 파일에는 다음 코드가 포함됩니다.

```html
<h1>Hello {{ name }}!</h1>
```

다음으로 `src/app` 디렉토리에 `app.component.css`라는 파일을 만들어야 합니다. 이 파일에는 다음 코드가 포함됩니다.

```css
h1 {
  color: #369;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 250%;
}
```

이제 프로젝트가 설정되었으므로 다음 명령을 실행하여 개발 서버를 시작할 수 있습니다.

```
$ nest start
```

## 애플리케이션 구축

이제 프로젝트가 설정되었으므로 다음 명령을 실행하여 애플리케이션을 빌드할 수 있습니다.

```
$ nest build
```

## 애플리케이션 제공

이제 프로젝트가 빌드되었으므로 다음 명령을 실행하여 애플리케이션을 제공할 수 있습니다.

```
$ nest serve
```

## 애플리케이션 테스트

이제 프로젝트가 제공되었으므로 다음 명령을 실행하여 애플리케이션을 테스트할 수 있습니다.

```
$ nest test
```

## 결론

이 게시물에서는 Progressive Web Apps와 함께 Nest.js를 사용하는 방법을 살펴보았습니다. Nest.js를 사용하여 확장 가능한 서버 측 애플리케이션을 쉽게 만드는 방법을 살펴보았습니다. 또한 Nest.js를 사용하여 프로그레시브 웹 앱을 쉽게 개발하는 방법도 살펴보았습니다.