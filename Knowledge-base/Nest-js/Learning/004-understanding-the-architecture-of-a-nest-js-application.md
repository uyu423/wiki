---
title: 004: Nest.js 애플리케이션의 아키텍처 이해
description: 
published: true
date: 2023-02-14T01:56:43.346Z
tags: 
editor: markdown
dateCreated: 2023-02-14T01:56:36.152Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [004: Understanding the architecture of a Nest.js application***English** document is available*](/en/Knowledge-base/Nest-js/Learning/004-understanding-the-architecture-of-a-nest-js-application)
{.links-list}


# Nest.js 애플리케이션의 아키텍처 이해

Nest.js는 확장 가능한 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. 최신 JavaScript를 사용하고 TypeScript(JavaScript로 컴파일됨)로 구축되었으며 객체 지향 프로그래밍, 기능적 프로그래밍 및 반응형 프로그래밍의 요소를 결합합니다.

Nest.js 애플리케이션은 일련의 중첩 모듈로 구성됩니다. Nest.js 모듈은 Angular 모듈과 동일하며 관련 구성 요소, 서비스, 파이프 및 지시문을 함께 그룹화하는 데 사용됩니다.

Nest.js 모듈의 주요 목적은 단일 기능 또는 도메인에 대한 모든 관련 코드를 찾을 수 있는 단일 위치(또는 루트)를 제공하는 것입니다. 이를 통해 Nest.js 애플리케이션에 대해 쉽게 추론하고 유지 관리할 수 있습니다.

Nest.js 모듈은 루트 모듈과 0개 이상의 하위 모듈이 있는 계층 구조로 구성됩니다. 루트 모듈은 애플리케이션의 진입점이며 일반적으로 Nest.js 애플리케이션을 구성하는 데 사용됩니다. 하위 모듈은 기능 또는 도메인에 대한 관련 코드를 함께 그룹화하는 데 사용됩니다.

아래 그림은 Nest.js 애플리케이션의 일반적인 구조를 보여줍니다. src 디렉토리에는 애플리케이션의 소스 코드가 포함되어 있습니다. app.module.ts 파일은 루트 모듈이며 Nest.js 애플리케이션을 구성하는 데 사용됩니다. 하위 모듈은 기능 또는 도메인에 대한 관련 코드를 함께 그룹화하는 데 사용됩니다.

![그림 1. Nest.js 애플리케이션의 일반적인 구조](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/img/app-structure.png)

src/app.module.ts 파일은 루트 모듈이며 Nest.js 애플리케이션을 구성하는 데 사용됩니다. @Nestjs/common 모듈을 가져와서 CommonModule 클래스를 제공하는 데 사용합니다. CommonModule 클래스는 인젝터 서비스를 제공하는 데 사용됩니다. 인젝터 서비스는 종속성을 해결하는 데 사용됩니다.

@Nestjs/core 모듈을 가져와서 NestFactory 클래스를 제공하는 데 사용합니다. NestFactory 클래스는 Nest.js 애플리케이션 인스턴스를 만드는 데 사용됩니다.

AppModule 클래스를 가져와서 AppModule 클래스를 정의하는 데 사용합니다. AppModule 클래스는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

AppModule 클래스에는 @Module() 데코레이터가 주석으로 추가됩니다. @Module() 데코레이터는 Nest.js 모듈을 정의하는 데 사용됩니다.

AppModule 클래스를 가져와서 AppModule 클래스를 정의하는 데 사용합니다. AppModule 클래스는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

AppModule 클래스에는 @Module() 데코레이터가 주석으로 추가됩니다. @Module() 데코레이터는 Nest.js 모듈을 정의하는 데 사용됩니다.

AppModule 클래스에는 생성자와 configure() 메서드가 포함되어 있습니다. 생성자는 종속성을 주입하는 데 사용됩니다. configure() 메서드는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

src/app.controller.ts 파일은 AppController 클래스를 정의하는 데 사용됩니다. AppController 클래스는 HTTP 요청을 처리하는 데 사용됩니다.

AppController 클래스에는 @Controller() 데코레이터가 주석으로 추가됩니다. @Controller() 데코레이터는 Nest.js 컨트롤러를 정의하는 데 사용됩니다.

AppController 클래스에는 root() 메서드가 포함되어 있습니다. root() 메서드는 HTTP GET 요청을 처리하는 데 사용됩니다.

src/app.service.ts 파일은 AppService 클래스를 정의하는 데 사용됩니다. AppService 클래스는 컨트롤러에 데이터를 제공하는 데 사용됩니다.

AppService 클래스에는 @Injectable() 데코레이터가 주석으로 추가됩니다. @Injectable() 데코레이터는 Nest.js 서비스를 정의하는 데 사용됩니다.

AppService 클래스에는 getData() 메서드가 포함되어 있습니다. getData() 메서드는 컨트롤러에 대한 데이터를 반환하는 데 사용됩니다.

src/environments/environment.ts 파일은 환경 변수를 정의하는 데 사용됩니다. 환경 변수는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

환경 변수는 environment() 함수를 사용하여 AppModule 클래스에 주입됩니다.

environment() 함수는 환경 변수를 Nest.js 애플리케이션에 주입하는 데 사용됩니다.

environment() 함수는 개체를 인수로 사용합니다. 개체에는 환경 변수가 포함되어 있습니다.

environment() 함수는 Environment 객체를 반환합니다. 환경 개체에는 환경 변수가 포함되어 있습니다.

환경 객체는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

src/main.ts 파일은 Nest.js 애플리케이션의 진입점입니다. src/main.ts 파일은 Nest.js 애플리케이션의 인스턴스를 만드는 데 사용됩니다.

src/main.ts 파일은 AppModule 클래스를 가져옵니다. AppModule 클래스는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

src/main.ts 파일은 NestFactory 클래스를 사용하여 Nest.js 애플리케이션의 인스턴스를 생성합니다.

NestFactory 클래스는 @nestjs/core 모듈에서 가져옵니다. NestFactory 클래스는 Nest.js 애플리케이션 인스턴스를 만드는 데 사용됩니다.

NestFactory 클래스는 AppModule 클래스를 인수로 사용합니다. AppModule 클래스는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

NestFactory 클래스는 Nest.js 애플리케이션의 인스턴스를 반환합니다.

Nest.js 애플리케이션의 인스턴스는 Nest.js 애플리케이션을 시작하는 데 사용됩니다.

Nest.js 애플리케이션의 인스턴스는 start() 메서드를 사용하여 시작됩니다.

start() 메서드는 Nest.js 애플리케이션을 시작하는 데 사용됩니다.

start() 메서드는 포트 번호를 인수로 사용합니다. 포트 번호는 HTTP 요청을 수신하는 데 사용됩니다.

start() 메서드는 Promise를 반환합니다. Nest.js 애플리케이션이 시작되면 Promise가 해결됩니다.

src/index.ts 파일은 TypeScript 컴파일러의 진입점입니다. src/index.ts 파일은 TypeScript 코드를 컴파일하는 데 사용됩니다.

src/index.ts 파일은 AppModule 클래스를 가져옵니다. AppModule 클래스는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

src/index.ts 파일은 tsconfig.json 파일을 사용하여 TypeScript 컴파일러를 구성합니다.

tsconfig.json 파일은 TypeScript 컴파일러를 구성하는 데 사용됩니다.

tsconfig.json 파일에는 컴파일러 옵션이 포함되어 있습니다. 컴파일러 옵션은 TypeScript 컴파일러를 구성하는 데 사용됩니다.

tsconfig.json 파일은 TypeScript 코드를 JavaScript 코드로 컴파일하는 데 사용됩니다.

TypeScript 코드는 tsc 명령을 사용하여 JavaScript 코드로 컴파일됩니다.

tsc 명령은 TypeScript 코드를 JavaScript 코드로 컴파일하는 데 사용됩니다.

tsc 명령은 tsconfig.json 파일을 인수로 사용합니다. tsconfig.json 파일은 TypeScript 컴파일러를 구성하는 데 사용됩니다.

tsc 명령은 TypeScript 코드를 JavaScript 코드로 컴파일합니다.

컴파일된 JavaScript 코드는 dist 디렉토리에 배치됩니다.

dist 디렉토리에는 컴파일된 JavaScript 코드가 포함되어 있습니다.

dist 디렉토리는 TypeScript 컴파일러의 출력 디렉토리입니다.

Nest.js 애플리케이션은 node 명령을 사용하여 실행됩니다.

node 명령은 Nest.js 애플리케이션을 실행하는 데 사용됩니다.

node 명령은 컴파일된 JavaScript 코드를 인수로 사용합니다. 컴파일된 JavaScript 코드는 dist 디렉토리에 배치됩니다.

node 명령은 Nest.js 애플리케이션을 실행합니다.

Nest.js 애플리케이션은 Node.js 서버에서 실행됩니다.

Node.js 서버는 Nest.js 애플리케이션을 실행하는 데 사용됩니다.

Node.js 서버는 JavaScript 런타임입니다.

Node.js 서버는 JavaScript 코드를 실행하는 데 사용됩니다.

Nest.js 애플리케이션은 웹 브라우저를 사용하여 액세스합니다.

웹 브라우저는 Nest.js 애플리케이션에 액세스하는 데 사용됩니다.

웹 브라우저는 Nest.js 애플리케이션에 HTTP 요청을 보내는 데 사용됩니다.

Nest.js 애플리케이션은 http://localhost:3000에서 액세스됩니다.

# 추가 정보

Nest.js는 확장 가능한 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. 최신 JavaScript를 사용하고 TypeScript(JavaScript로 컴파일됨)로 구축되었으며 객체 지향 프로그래밍, 기능적 프로그래밍 및 반응형 프로그래밍의 요소를 결합합니다.

Nest.js 애플리케이션은 일련의 중첩 모듈로 구성됩니다. Nest.js 모듈은 Angular 모듈과 동일하며 관련 구성 요소, 서비스, 파이프 및 지시문을 함께 그룹화하는 데 사용됩니다.

Nest.js 모듈의 주요 목적은 단일 기능 또는 도메인에 대한 모든 관련 코드를 찾을 수 있는 단일 위치(또는 루트)를 제공하는 것입니다. 이를 통해 Nest.js 애플리케이션에 대해 쉽게 추론하고 유지 관리할 수 있습니다.

Nest.js 모듈은 루트 모듈과 0개 이상의 하위 모듈이 있는 계층 구조로 구성됩니다. 루트 모듈은 애플리케이션의 진입점이며 일반적으로 Nest.js 애플리케이션을 구성하는 데 사용됩니다. 하위 모듈은 기능 또는 도메인에 대한 관련 코드를 함께 그룹화하는 데 사용됩니다.

아래 그림은 Nest.js 애플리케이션의 일반적인 구조를 보여줍니다. src 디렉토리에는 애플리케이션의 소스 코드가 포함되어 있습니다. app.module.ts 파일은 루트 모듈이며 Nest.js 애플리케이션을 구성하는 데 사용됩니다. 하위 모듈은 기능 또는 도메인에 대한 관련 코드를 함께 그룹화하는 데 사용됩니다.

![그림 1. Nest.js 애플리케이션의 일반적인 구조](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/img/app-structure.png)

src/app.module.ts 파일은 루트 모듈이며 Nest.js 애플리케이션을 구성하는 데 사용됩니다. @Nestjs/common 모듈을 가져와서 CommonModule 클래스를 제공하는 데 사용합니다. CommonModule 클래스는 인젝터 서비스를 제공하는 데 사용됩니다. 인젝터 서비스는 종속성을 해결하는 데 사용됩니다.

@Nestjs/core 모듈을 가져와서 NestFactory 클래스를 제공하는 데 사용합니다. NestFactory 클래스는 Nest.js 애플리케이션 인스턴스를 만드는 데 사용됩니다.

AppModule 클래스를 가져와서 AppModule 클래스를 정의하는 데 사용합니다. AppModule 클래스는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

AppModule 클래스에는 @Module() 데코레이터가 주석으로 추가됩니다. @Module() 데코레이터는 Nest.js 모듈을 정의하는 데 사용됩니다.

AppModule 클래스를 가져와서 AppModule 클래스를 정의하는 데 사용합니다. AppModule 클래스는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

AppModule 클래스에는 @Module() 데코레이터가 주석으로 추가됩니다. @Module() 데코레이터는 Nest.js 모듈을 정의하는 데 사용됩니다.

AppModule 클래스에는 생성자와 configure() 메서드가 포함되어 있습니다. 생성자는 종속성을 주입하는 데 사용됩니다. configure() 메서드는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

src/app.controller.ts 파일은 AppController 클래스를 정의하는 데 사용됩니다. AppController 클래스는 HTTP 요청을 처리하는 데 사용됩니다.

AppController 클래스에는 @Controller() 데코레이터가 주석으로 추가됩니다. @Controller() 데코레이터는 Nest.js 컨트롤러를 정의하는 데 사용됩니다.

AppController 클래스에는 root() 메서드가 포함되어 있습니다. root() 메서드는 HTTP GET 요청을 처리하는 데 사용됩니다.

src/app.service.ts 파일은 AppService 클래스를 정의하는 데 사용됩니다. AppService 클래스는 컨트롤러에 데이터를 제공하는 데 사용됩니다.

AppService 클래스에는 @Injectable() 데코레이터가 주석으로 추가됩니다. @Injectable() 데코레이터는 Nest.js 서비스를 정의하는 데 사용됩니다.

AppService 클래스에는 getData() 메서드가 포함되어 있습니다. getData() 메서드는 컨트롤러에 대한 데이터를 반환하는 데 사용됩니다.

src/environments/environment.ts 파일은 환경 변수를 정의하는 데 사용됩니다. 환경 변수는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

환경 변수는 environment() 함수를 사용하여 AppModule 클래스에 주입됩니다.

environment() 함수는 환경 변수를 Nest.js 애플리케이션에 주입하는 데 사용됩니다.

environment() 함수는 개체를 인수로 사용합니다. 개체에는 환경 변수가 포함되어 있습니다.

environment() 함수는 Environment 객체를 반환합니다. 환경 개체에는 환경 변수가 포함되어 있습니다.

환경 객체는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

src/main.ts 파일은 Nest.js 애플리케이션의 진입점입니다. src/main.ts 파일은 Nest.js 애플리케이션의 인스턴스를 만드는 데 사용됩니다.

src/main.ts 파일은 AppModule 클래스를 가져옵니다. AppModule 클래스는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

src/main.ts 파일은 NestFactory 클래스를 사용하여 Nest.js 애플리케이션의 인스턴스를 생성합니다.

NestFactory 클래스는 @nestjs/core 모듈에서 가져옵니다. NestFactory 클래스는 Nest.js 애플리케이션 인스턴스를 만드는 데 사용됩니다.

NestFactory 클래스는 AppModule 클래스를 인수로 사용합니다. AppModule 클래스는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

NestFactory 클래스는 Nest.js 애플리케이션의 인스턴스를 반환합니다.

Nest.js 애플리케이션의 인스턴스는 Nest.js 애플리케이션을 시작하는 데 사용됩니다.

Nest.js 애플리케이션의 인스턴스는 start() 메서드를 사용하여 시작됩니다.

start() 메서드는 Nest.js 애플리케이션을 시작하는 데 사용됩니다.

start() 메서드는 포트 번호를 인수로 사용합니다. 포트 번호는 HTTP 요청을 수신하는 데 사용됩니다.

start() 메서드는 Promise를 반환합니다. Nest.js 애플리케이션이 시작되면 Promise가 해결됩니다.

src/index.ts 파일은 TypeScript 컴파일러의 진입점입니다. src/index.ts 파일은 TypeScript 코드를 컴파일하는 데 사용됩니다.

src/index.ts 파일은 AppModule 클래스를 가져옵니다. AppModule 클래스는 Nest.js 애플리케이션을 구성하는 데 사용됩니다.

src/index.ts 파일은 tsconfig.json 파일을 사용하여 TypeScript 컴파일러를 구성합니다.

tsconfig.json 파일은 TypeScript 컴파일러를 구성하는 데 사용됩니다.

tsconfig.json 파일에는 컴파일러 옵션이 포함되어 있습니다. 컴파일러 옵션은 TypeScript 컴파일러를 구성하는 데 사용됩니다.

tsconfig.json 파일은 TypeScript 코드를 JavaScript 코드로 컴파일하는 데 사용됩니다.

TypeScript 코드는 tsc 명령을 사용하여 JavaScript 코드로 컴파일됩니다.

tsc 명령은 TypeScript 코드를 JavaScript 코드로 컴파일하는 데 사용됩니다.

tsc 명령은 tsconfig.json 파일을 인수로 사용합니다. tsconfig.json 파일은 TypeScript 컴파일러를 구성하는 데 사용됩니다.

tsc 명령은 TypeScript 코드를 JavaScript 코드로 컴파일합니다.

컴파일된 JavaScript 코드는 dist 디렉토리에 배치됩니다.

dist 디렉토리에는 컴파일된 JavaScript 코드가 포함되어 있습니다.

dist 디렉토리는 TypeScript 컴파일러의 출력 디렉토리입니다.

Nest.js 애플리케이션은 node 명령을 사용하여 실행됩니다.

node 명령은 Nest.js 애플리케이션을 실행하는 데 사용됩니다.

node 명령은 컴파일된 JavaScript 코드를 인수로 사용합니다. 컴파일된 JavaScript 코드는 dist 디렉토리에 배치됩니다.

node 명령은 Nest.js 애플리케이션을 실행합니다.

Nest.js 애플리케이션은 Node.js 서버에서 실행됩니다.

Node.js 서버는 Nest.js 애플리케이션을 실행하는 데 사용됩니다.

Node.js 서버는 JavaScript 런타임입니다.

Node.js 서버는 JavaScript 코드를 실행하는 데 사용됩니다.

Nest.js 애플리케이션은 웹 브라우저를 사용하여 액세스합니다.

웹 브라우저는 Nest.js 애플리케이션에 액세스하는 데 사용됩니다.

웹 브라우저는 Nest.js 애플리케이션에 HTTP 요청을 보내는 데 사용됩니다.

Nest.js 애플리케이션은 http://localhost:3000에서 액세스됩니다.