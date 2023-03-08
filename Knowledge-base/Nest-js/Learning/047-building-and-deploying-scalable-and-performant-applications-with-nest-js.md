---
title: 047: Nest.js로 확장 가능하고 성능이 뛰어난 애플리케이션 구축 및 배포
description: 
published: true
date: 2023-02-15T17:32:53.836Z
tags: 
editor: markdown
dateCreated: 2023-02-15T17:32:52.143Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [047: Building and deploying scalable and performant applications with Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/047-building-and-deploying-scalable-and-performant-applications-with-nest-js)
{.links-list}


# Nest.js

Nest.js는 Node.js로 확장 가능하고 성능이 뛰어난 애플리케이션을 구축하기 위한 프레임워크입니다. Angular에서 영감을 얻었으며 서버 측 애플리케이션을 만들기 위한 강력한 도구 세트를 제공합니다. 이 게시물에서는 Nest.js를 시작하는 방법과 확장 가능하고 성능이 뛰어난 애플리케이션을 빌드하고 배포하는 방법을 살펴보겠습니다.

## 시작하기

Nest.js를 시작하려면 Nest.js CLI를 설치해야 합니다. npm으로 이 작업을 수행할 수 있습니다.

```
npm install -g @nestjs/cli
```

Nest.js CLI가 설치되면 다음 명령을 사용하여 새 Nest.js 프로젝트를 만들 수 있습니다.

```
nest new my-project
```

이렇게 하면 내부에 기본 Nest.js 프로젝트 구조가 있는 ```my-project```라는 새 디렉토리가 생성됩니다.

## 프로젝트 구조

Nest.js 프로젝트의 기본 구조는 다음과 같습니다.

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

```javascript
@Controller('hello')
export class HelloController {

  @Get()
  hello() {
    return 'Hello, world!';
  }

}
```test``` 디렉토리에는 애플리케이션에 대한 단위 테스트가 포함되어 있습니다. ```app.controller.spec.ts``` 파일에는 컨트롤러에 대한 단위 테스트가 포함되어 있습니다. ```app.service.spec.ts``` 파일에는 서비스에 대한 단위 테스트가 포함되어 있습니다.

```javascript
@Injectable()
export class HelloService {

  generateGreeting(name: string) {
    return `Hello, ${name}!`;
  }

}
```nest-cli.json``` 파일에는 Nest.js CLI에 대한 구성이 포함되어 있습니다.

```javascript
@Module({
  controllers: [HelloController],
  providers: [HelloService],
})
export class HelloModule {}
```package.json``` 파일에는 프로젝트의 메타데이터가 포함되어 있습니다.

## 코드 작성

이제 프로젝트 구조에 대한 기본적인 이해를 마쳤으니 Nest.js에서 코드를 작성하는 방법을 살펴보겠습니다.

### 컨트롤러

컨트롤러는 들어오는 HTTP 요청을 처리하고 응답을 반환하는 역할을 합니다. Nest.js에서 컨트롤러는 ```@Controller()``` 데코레이터를 사용하여 정의됩니다.

다음은 ```/hello``` 경로에 대한 GET 요청을 처리하는 예제 컨트롤러입니다.

```
nest build
```

이 예제에서 ```@Controller('hello')``` 데코레이터는 ```hello```라는 이름으로 컨트롤러를 정의합니다. ```@Get()``` 데코레이터는 GET 요청에 대한 핸들러를 정의합니다. ```hello()``` 메서드는 ```Hello, world!``` 문자열을 반환하는 핸들러 함수입니다.

### 서비스

서비스는 비즈니스 로직 캡슐화를 담당하는 싱글톤입니다. Nest.js에서 서비스는 ```@Injectable()``` 데코레이터를 사용하여 정의됩니다.

인사말을 생성하는 방법이 있는 예제 서비스는 다음과 같습니다.

```
web: nest start
```

이 예에서 ```@Injectable()``` 데코레이터는 서비스를 주입 가능한 것으로 정의합니다. ```generateGreeting()``` 메서드는 ```name``` 매개변수를 사용하고 인사말 문자열을 반환합니다.

### 모듈

모듈은 Nest.js에서 관련 기능을 구성하는 데 사용됩니다. Nest.js에서 모듈은 ```@Module()``` 데코레이터를 사용하여 정의됩니다.

다음은 컨트롤러와 서비스를 정의하는 예제 모듈입니다.

```
git push heroku master
```

이 예제에서 ```@Module()``` 데코레이터는 ```HelloController``` 및 ```HelloService```로 모듈을 정의합니다.

## 구축 및 배포

이제 Nest.js에서 코드를 작성하는 방법을 살펴보았으므로 Nest.js 애플리케이션을 빌드하고 배포하는 방법을 살펴보겠습니다.

### 건물

Nest.js 애플리케이션을 빌드하려면 Nest.js CLI를 사용해야 합니다. Nest.js CLI는 Nest.js 애플리케이션을 빌드하는 데 사용할 수 있는 ```build``` 명령을 제공합니다.

Nest.js 애플리케이션을 빌드하려면 다음 명령을 실행해야 합니다.

```
둥지 짓기
```

그러면 Nest.js 애플리케이션이 빌드되고 컴파일된 파일이 ```dist``` 디렉토리에 출력됩니다.

### 배포 중

Nest.js 애플리케이션을 배포하려면 Node.js 호스팅 공급자를 사용해야 합니다. 선택할 수 있는 Node.js 호스팅 공급자가 많이 있지만 [Heroku](https://www.heroku.com/)를 사용하는 것이 좋습니다.

Heroku는 Nest.js 애플리케이션을 배포하는 데 사용할 수 있는 무료 등급을 제공합니다. 애플리케이션을 Heroku에 배포하려면 프로젝트 루트에 ```Procfile```을 생성해야 합니다. ```Procfile```은 Heroku에게 애플리케이션 실행 방법을 알려주는 데 사용됩니다.

다음은 Nest.js 애플리케이션의 ```Procfile``` 예시입니다.

```
웹: 둥지 시작
```

이 예에서 ```web``` 프로세스 유형은 Heroku에게 이것이 웹 애플리케이션임을 알리는 데 사용됩니다. ```nest start``` 명령은 Nest.js 애플리케이션을 시작하는 데 사용됩니다.

```Procfile```을 생성했으면 다음 명령을 사용하여 Nest.js 애플리케이션을 Heroku에 배포할 수 있습니다.

```
git push 헤로쿠 마스터
```

이렇게 하면 코드가 Heroku로 푸시되고 새 배포가 트리거됩니다.

## 결론

이 게시물에서는 Nest.js를 시작하는 방법과 이를 사용하여 확장 가능하고 성능이 뛰어난 애플리케이션을 빌드하고 배포하는 방법을 살펴보았습니다. Nest.js는 서버 측 애플리케이션을 구축하기 위한 강력한 프레임워크이며 이 게시물이 이에 대한 좋은 소개가 되었기를 바랍니다.