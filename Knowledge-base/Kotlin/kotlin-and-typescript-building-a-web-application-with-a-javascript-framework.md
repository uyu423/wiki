---
title: Kotlin 및 TypeScript: JavaScript 프레임워크로 웹 애플리케이션 구축
description: 
published: true
date: 2023-02-17T18:16:43.282Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:36:33.205Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kotlin and TypeScript: Building a Web Application with a JavaScript Framework***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-typescript-building-a-web-application-with-a-javascript-framework)
{.links-list}


Kotlin과 TypeScript는 웹 애플리케이션을 구축하는 데 함께 사용할 수 있는 널리 사용되는 두 가지 프로그래밍 언어입니다. 이 기사에서는 Kotlin 및 TypeScript를 사용하여 JavaScript 프레임워크로 웹 애플리케이션을 빌드하는 방법을 살펴보겠습니다.

먼저 Kotlin과 TypeScript를 함께 사용할 때의 몇 가지 이점을 살펴보겠습니다. Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 언어입니다. 안전성, 상호 운용성 및 도구 지원으로 유명합니다. TypeScript는 정적 타이핑 및 기타 기능을 추가하는 JavaScript의 상위 집합입니다. 도구 지원 및 확장 기능으로 유명합니다.

Kotlin과 TypeScript를 함께 사용하면 두 언어의 이점을 얻을 수 있습니다. Kotlin의 안전 및 도구 지원과 TypeScript의 확장 기능을 사용할 수 있습니다.

다음으로 Kotlin과 TypeScript를 사용하여 프로젝트를 설정하는 방법을 살펴보겠습니다. 간단한 "Hello, World!" 웹 애플리케이션.

먼저 프로젝트 디렉토리를 생성해야 합니다. 명령줄이나 IDE를 사용하여 이 작업을 수행할 수 있습니다.

다음으로 프로젝트 디렉토리에 "Hello.kt"라는 파일을 생성합니다. 파일에 다음 코드를 추가합니다.

```kotlin
fun main(args: Array<String>) {
    println("Hello, World!")
}
```

그런 다음 명령줄을 사용하여 Kotlin 코드를 컴파일할 수 있습니다.

```
kotlinc Hello.kt -d hello.js
```

이렇게 하면 프로젝트 디렉터리에 "hello.js"라는 파일이 생성됩니다.

이제 프로젝트 디렉토리에 "index.html"이라는 파일을 만들 수 있습니다. 파일에 다음 코드를 추가합니다.

```html
<!doctype html>
<html>

<head>
    <meta charset="utf-8">
    <title>Hello, World!</title>
</head>

<body>
    <script src="hello.js"></script>
</body>

</html>
```

마지막으로 브라우저에서 "index.html"을 열 수 있으며 "Hello, World!"가 표시되어야 합니다. 메시지.

Kotlin 및 TypeScript를 사용하여 프로젝트를 설정하는 방법을 살펴보았으므로 이제 JavaScript 프레임워크에서 Kotlin 및 TypeScript를 사용하는 방법을 살펴보겠습니다. 우리는 React JavaScript 프레임워크를 사용할 것입니다.

먼저 React와 React-DOM을 설치해야 합니다. 명령줄을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install react react-dom
```

다음으로 프로젝트 디렉터리에 "Hello.tsx"라는 파일을 만듭니다. 파일에 다음 코드를 추가합니다.

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

ReactDOM.render(
    <h1>Hello, World!</h1>,
    document.getElementById("root")
);
```

그런 다음 명령줄을 사용하여 TypeScript 코드를 컴파일합니다.

```
tsc --jsx react Hello.tsx
```

이렇게 하면 프로젝트 디렉터리에 "Hello.js"라는 파일이 생성됩니다.

마지막으로 React 코드를 포함하도록 "index.html" 파일을 업데이트해야 합니다. 파일에 다음 코드를 추가합니다.

```html
<!doctype html>
<html>

<head>
    <meta charset="utf-8">
    <title>Hello, World!</title>
</head>

<body>
    <div id="root"></div>
    <script src="hello.js"></script>
</body>

</html>
```

그런 다음 브라우저에서 "index.html"을 열면 "Hello, World!"가 표시됩니다. 메시지.

Kotlin과 TypeScript는 웹 애플리케이션을 구축하는 데 함께 사용할 수 있는 널리 사용되는 두 가지 프로그래밍 언어입니다. 이 기사에서는 Kotlin 및 TypeScript를 사용하여 JavaScript 프레임워크로 웹 애플리케이션을 빌드하는 방법을 살펴보았습니다.