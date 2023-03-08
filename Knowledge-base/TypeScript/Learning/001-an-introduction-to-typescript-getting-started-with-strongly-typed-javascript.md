---
title: 001: TypeScript 소개: 강력한 형식의 JavaScript 시작하기
description: 
published: true
date: 2023-03-02T08:40:53.753Z
tags: 
editor: markdown
dateCreated: 2023-03-02T08:40:46.550Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [001: An Introduction to TypeScript: Getting Started with Strongly Typed JavaScript***English** document is available*](/en/Knowledge-base/TypeScript/Learning/001-an-introduction-to-typescript-getting-started-with-strongly-typed-javascript)
{.links-list}


소개

JavaScript 코드를 작성하고 코드를 실행하기 전에 몇 가지 오류를 포착하고 싶었던 적이 있습니까? JavaScript로 더 확장 가능하고 유지 관리 가능한 코드를 작성하고 싶습니까? 그렇다면 TypeScript가 원하는 솔루션일 수 있습니다. TypeScript는 선택적 정적 타이핑 및 기타 기능을 언어에 추가하는 JavaScript의 상위 집합입니다. 이 게시물에서는 TypeScript의 기본 사항과 시작 방법을 다룹니다.

타입스크립트란?

TypeScript는 Microsoft에서 개발하고 유지 관리하는 프로그래밍 언어입니다. JavaScript의 상위 집합입니다. 즉, 모든 유효한 JavaScript 코드는 유효한 TypeScript 코드이기도 합니다. TypeScript는 런타임 대신 컴파일 타임에 오류를 포착할 수 있는 선택적 정적 유형 지정을 JavaScript에 추가합니다. 또한 클래스, 인터페이스, 모듈 등과 같은 기능을 추가합니다.

TypeScript 시작하기

TypeScript를 시작하려면 TypeScript 컴파일러를 설치해야 합니다. Node.js용 패키지 관리자인 npm을 사용하여 이 작업을 수행할 수 있습니다. 터미널 또는 명령 프롬프트를 열고 다음 명령을 실행합니다.

```npm install -g typescript```

This command installs the TypeScript compiler globally on your machine. To check if the installation was successful, run the following command:

```tsc --버전```

이 명령은 TypeScript 컴파일러의 버전 번호를 출력해야 합니다.

TypeScript 파일 생성

TypeScript 파일을 생성하려면 `.ts` 확장자를 가진 파일을 생성해야 합니다. `app.ts`라는 파일을 만들고 다음 코드를 추가해 보겠습니다.

```
function greet(name: string) {
    console.log("Hello, " + name);
}

greet("TypeScript");
```

이 코드에서는 `name`이라는 문자열 매개변수를 사용하는 `greet`라는 함수를 정의합니다. 매개변수 이름 뒤의 `: 문자열` 구문은 매개변수가 `문자열` 유형임을 나타냅니다. 그런 다음 문자열 "TypeScript"로 `greet` 함수를 호출합니다.

TypeScript 파일 컴파일

`app.ts` 파일을 컴파일하려면 터미널 또는 명령 프롬프트에서 다음 명령을 실행하십시오.

```tsc app.ts```

This command compiles the TypeScript code into JavaScript code and creates a file called `app.js`. You can now run the `app.js` file using Node.js by executing the following command:

```노드 app.js```

이 명령은 터미널이나 명령 프롬프트에 "Hello, TypeScript"를 출력해야 합니다.

TypeScript 유형

TypeScript는 다음을 포함하여 JavaScript에 여러 유형을 추가합니다.

- `string`: 문자열 값을 나타냅니다.
- `숫자`: 숫자 값을 나타냅니다.
- `boolean`: 부울 값(참 또는 거짓)을 나타냅니다.
- `any`: 모든 유형을 나타냅니다(JavaScript의 동적 타이핑과 유사).
- `void`: 유형이 없음을 나타냅니다(일반적으로 값을 반환하지 않는 함수에 사용됨).
- `null` 및 `undefined`: 각각 null 및 정의되지 않은 값을 나타냅니다.
- `object`: 기본이 아닌 유형(예: 배열, 함수, 객체 등)을 나타냅니다.
- `배열`: 특정 유형의 값 배열을 나타냅니다.

TypeScript에서 이러한 유형을 사용하는 몇 가지 예를 살펴보겠습니다.

```
let name: string = "John";
let age: number = 30;
let isMarried: boolean = true;
let anything: any = "anything";
let nothing: void = undefined;
let nothing2: void = null;
let obj: object = { name: "John", age: 30 };
let nums: number[] = [1, 2, 3];
```

이 코드에서는 `string`, `number`, `boolean`, `any`, `void`, `object` 및 `array`를 포함하여 다양한 유형의 변수를 정의합니다.

TypeScript 인터페이스

TypeScript 인터페이스를 사용하면 객체의 구조를 정의할 수 있습니다. 'interface' 키워드 뒤에 인터페이스 이름과 있어야 하는 속성을 사용하여 인터페이스를 정의할 수 있습니다. 예를 살펴보겠습니다.

```
interface Person {
    name: string;
    age: number;
    isMarried?: boolean;
}

function greet(person: Person) {
    console.log("Hello, " + person.name);
}

let john: Person = { name: "John", age: 30 };
greet(john);
```

이 코드에서 `string` 유형의 `name`, `number` 유형의 `age` 및 `boolean` 유형의 `isMarried`(선택 사항)의 세 가지 속성이 있는 `Person`이라는 인터페이스를 정의합니다. 그런 다음 'Person' 유형의 매개변수를 사용하고 콘솔에 인사말을 기록하는 'greet'라는 함수를 정의합니다. `Person` 인터페이스와 일치하는 `john`이라는 객체를 만들고 `john` 객체로 `greet` 함수를 호출합니다.

TypeScript 클래스

TypeScript 클래스를 사용하면 개체에 대한 청사진을 정의할 수 있습니다. 'class' 키워드 다음에 클래스의 이름과 있어야 하는 속성 및 메서드를 사용하여 클래스를 정의할 수 있습니다. 예를 살펴보겠습니다.

```
class Person {
    name: string;
    age: number;
    isMarried?: boolean;

    constructor(name: string, age: number, isMarried?: boolean) {
        this.name = name;
        this.age = age;
        this.isMarried = isMarried;
    }

    greet() {
        console.log("Hello, " + this.name);
    }
}

let john: Person = new Person("John", 30);
john.greet();
```

이 코드에서는 `string` 유형의 `name`, `number` 유형의 `age` 및 `boolean` 유형의 `isMarried`(선택 사항)의 세 가지 속성이 있는 `Person`이라는 클래스를 정의합니다. 또한 세 개의 매개변수를 받아 클래스의 속성에 할당하는 생성자를 정의합니다. 콘솔에 인사말을 기록하는 'greet'라는 메서드를 정의합니다. `new` 키워드를 사용하여 `john`이라는 객체를 생성하고 그것에 `greet` 메서드를 호출합니다.

추가 정보

- TypeScript는 오픈 소스이며 Microsoft 및 커뮤니티에서 적극적으로 유지 관리합니다.
- TypeScript는 Visual Studio Code, WebStorm, Atom 등 다양한 IDE 및 편집기와 함께 사용할 수 있습니다.
- TypeScript는 프런트엔드 및 백엔드 코드와 Node.js 애플리케이션을 작성하는 데 사용할 수 있습니다.

결론

이 게시물에서는 TypeScript의 기본 사항과 시작 방법을 다뤘습니다. TypeScript 파일을 만들고 컴파일하고 실행하는 방법을 살펴보았습니다. 또한 TypeScript 유형, 인터페이스 및 클래스도 살펴보았습니다. TypeScript는 JavaScript에서 보다 확장 가능하고 유지 관리 가능한 코드를 작성하는 데 도움이 되는 강력한 도구입니다. TypeScript에 대해 자세히 알아보려면 아래에 나열된 공식 TypeScript 문서 및 기타 리소스를 확인하십시오.

외부 리소스

- 공식 TypeScript 문서: https://www.typescriptlang.org/docs/
- TypeScript 플레이그라운드: https://www.typescriptlang.org/play
- TypeScript 심층 분석: https://basarat.gitbook.io/typescript/
- TypeScript 핸드북: https://www.typescriptlang.org/docs/handbook/