---
title: 실시간 데이터베이스 및 인증을 위해 TypeScript를 Firebase와 통합
description: 
published: true
date: 2023-02-17T18:14:30.607Z
tags: 
editor: markdown
dateCreated: 2023-01-30T21:37:39.138Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Integrating TypeScript with Firebase for Real-Time Database and Authentication***English** version of this document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-firebase-for-real-time-database-and-authentication)
{.links-list}

    
    이 문서를 구성하는 방법에 대한 많은 가능성이 있지만 다음 섹션은 가이드 역할을 합니다.

# 소개

TypeScript는 개발자가 유지 관리가 가능하고 오류가 없는 코드를 작성할 수 있게 해주는 강력한 프로그래밍 언어입니다. Firebase는 실시간 데이터베이스 및 인증 서비스를 제공하는 인기 있는 모바일 및 웹 애플리케이션 개발 플랫폼입니다. 이 기사에서는 TypeScript를 Firebase와 통합하여 실시간 데이터베이스 및 인증 시스템을 만드는 방법을 보여줍니다.

# 타입스크립트란?

TypeScript는 개발자가 유지 관리가 가능하고 오류가 없는 코드를 작성할 수 있도록 하는 JavaScript의 상위 집합입니다. TypeScript는 JavaScript로 컴파일되어 기존 JavaScript 코드와 쉽게 통합할 수 있습니다. TypeScript는 컴파일 중에 유형 오류를 확인하여 코드에 추가적인 보안 계층을 추가합니다. 이렇게 하면 코드베이스에 오류가 도입되는 것을 방지하고 코드 리팩터링 및 디버그가 더 쉬워집니다.

# 파이어베이스란?

Firebase는 실시간 데이터베이스 및 인증 서비스를 제공하는 인기 있는 모바일 및 웹 애플리케이션 개발 플랫폼입니다. Firebase는 사용하기 쉽고 소규모 프로젝트를 위한 무료 등급을 제공합니다. Firebase의 실시간 데이터베이스를 사용하면 여러 기기에서 실시간으로 데이터를 동기화할 수 있으므로 반응형 애플리케이션을 쉽게 구축할 수 있습니다. Firebase의 인증 서비스를 사용하면 애플리케이션에 로그인 및 가입 기능을 쉽게 추가할 수 있습니다.

# TypeScript와 Firebase를 통합하는 방법

이 섹션에서는 TypeScript를 Firebase와 통합하여 실시간 데이터베이스 및 인증 시스템을 만드는 방법을 보여줍니다.

## Firebase 설정

Firebase를 사용하기 전에 Firebase 프로젝트를 생성해야 합니다. [Firebase 콘솔](https://console.firebase.google.com/)로 이동하여 '프로젝트 만들기' 버튼을 클릭합니다.

프로젝트 이름을 입력하고 "프로젝트 생성" 버튼을 클릭합니다.

프로젝트가 생성되면 "웹 앱에 Firebase 추가" 버튼을 클릭합니다.

그러면 Firebase 프로젝트의 구성 정보가 포함된 모달이 열립니다. 나중에 이 정보가 필요하므로 클립보드나 텍스트 편집기에 복사하십시오.

## Firebase SDK 설치

다음으로 Firebase SDK를 설치해야 합니다. npm을 사용하여 이 작업을 수행할 수 있습니다. 터미널에서 다음 명령을 실행하여 Firebase SDK를 설치합니다.

```
npm install firebase --save
```

## TypeScript 구성

TypeScript는 tsconfig.json 파일을 사용하여 컴파일러를 구성합니다. tsconfig.json 파일은 프로젝트 디렉터리의 루트에 있어야 합니다.

tsconfig.json 파일에 다음 콘텐츠를 추가합니다.

```json
{
    "compilerOptions": {
        "target": "es5",
        "module": "commonjs",
        "sourceMap": true
    }
}
```

compilerOptions 섹션에서 TypeScript 컴파일러가 es5 JavaScript를 대상으로 하고 commonjs 모듈 형식을 사용하도록 지정했습니다. TypeScript 코드를 디버깅할 때 도움이 될 소스 맵도 활성화했습니다.

## Firebase 초기화

이제 Firebase SDK를 설치하고 TypeScript 프로젝트를 구성했으므로 TypeScript 코드에서 Firebase를 초기화할 수 있습니다.

src/index.ts 파일에 다음 코드를 추가합니다.

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp(firebaseConfig);
```

firebaseConfig 개체의 자리 표시자 값을 Firebase 프로젝트의 값으로 바꿉니다.

## 실시간 데이터베이스 생성

Firebase의 실시간 데이터베이스를 사용하면 여러 기기에서 실시간으로 데이터를 동기화할 수 있습니다. 이를 통해 반응형 애플리케이션을 쉽게 구축할 수 있습니다.

실시간 데이터베이스를 생성하려면 먼저 데이터베이스에 대한 참조를 생성해야 합니다. firebase.database() 메서드를 사용하여 이 작업을 수행할 수 있습니다.

src/index.ts 파일에 다음 코드를 추가합니다.

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp(firebaseConfig);

const database = firebase.database();
```

다음으로 장치 간에 동기화할 데이터 개체를 만들어야 합니다. 데이터 개체에 message 속성을 추가하고 해당 값을 "Hello, world!"로 설정합니다.

src/index.ts 파일에 다음 코드를 추가합니다.

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp(firebaseConfig);

const database = firebase.database();

const data = {
    message: "Hello, world!"
};
```

이제 데이터 개체를 데이터베이스에 추가해야 합니다. set() 메서드를 사용하여 이 작업을 수행할 수 있습니다.

src/index.ts 파일에 다음 코드를 추가합니다.

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp(firebaseConfig);

const database = firebase.database();

const data = {
    message: "Hello, world!"
};

database.ref().set(data);
```

이제 데이터는 실시간 데이터베이스에 유지됩니다. "데이터" 탭으로 이동하여 Firebase 콘솔에서 데이터를 볼 수 있습니다.

데이터베이스에서 데이터를 읽으려면 on() 메서드를 사용할 수 있습니다. on() 메서드는 이벤트 유형과 콜백 함수를 인수로 사용합니다. 이벤트 유형은 "value", "child_added", "child_changed", "child_removed" 또는 "child_moved"일 수 있습니다. 콜백 함수는 이벤트 유형이 트리거될 때마다 호출됩니다.

src/index.ts 파일에 다음 코드를 추가합니다.

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp(firebaseConfig);

const database = firebase.database();

const data = {
    message: "Hello, world!"
};

database.ref().set(data);

database.ref().on("value", (snapshot) => {
    console.log(snapshot.val());
});
```

이제 데이터가 업데이트될 때마다 콜백 함수가 호출되고 데이터가 콘솔에 기록됩니다.

## 인증 추가

Firebase의 인증 서비스를 사용하면 애플리케이션에 로그인 및 가입 기능을 쉽게 추가할 수 있습니다. Firebase는 Google, Facebook, Twitter를 비롯한 여러 유명 ID 공급업체를 지원합니다. 이 섹션에서는 TypeScript 애플리케이션에 Google 로그인을 추가하는 방법을 보여줍니다.

먼저 Firebase 프로젝트에서 Google 로그인 공급자를 활성화해야 합니다. 이렇게 하려면 Firebase 콘솔로 이동하여 '로그인 방법' 탭을 클릭합니다.

그런 다음 "Google" 로그인 공급자를 클릭하고 사용하도록 설정합니다.

이제 Google 로그인 공급자를 사용하도록 TypeScript 프로젝트를 구성해야 합니다. 제공업체 ID를 firebase.auth.GoogleAuthProvider() 메서드에 전달하면 됩니다.

src/index.ts 파일에 다음 코드를 추가합니다.

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp(firebaseConfig);

const auth = firebase.auth();

const provider = new firebase.auth.GoogleAuthProvider();
```

이제 로그인 공급자를 구성했으므로 HTML 파일에 로그인 버튼을 추가할 수 있습니다.

src/index.html 파일에 다음 코드를 추가합니다.

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>TypeScript with Firebase</title>
</head>

<body>
    <button id="sign-in">Sign in with Google</button>
</body>

</html>
```

다음으로 로그인 버튼에 이벤트 리스너를 추가해야 합니다. 버튼을 클릭하면 Google 계정으로 로그인됩니다.

src/index.ts 파일에 다음 코드를 추가합니다.

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp(firebaseConfig);

const auth = firebase.auth();

const provider = new firebase.auth.GoogleAuthProvider();

const signInButton = document.getElementById("sign-in");

signInButton.addEventListener("click", () => {
    auth.signInWithPopup(provider);
});
```

이제 로그인 버튼을 클릭하면 Google 계정으로 로그인하라는 메시지가 표시됩니다.

로그인하면 firebase.auth().currentUser 속성을 사용하여 사용자 정보에 액세스할 수 있습니다.

src/index.ts 파일에 다음 코드를 추가합니다.

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp(firebaseConfig);

const auth = firebase.auth();

const provider = new firebase.auth.GoogleAuthProvider();

const signInButton = document.getElementById("sign-in");

signInButton.addEventListener("click", () => {
    auth.signInWithPopup(provider);
});

auth.onAuthStateChanged((user) => {
    if (user) {
        console.log(user.displayName);
    }
});
```

이제 Google 계정으로 로그인하면 이름이 콘솔에 기록됩니다.

## 로그 아웃하다

이 섹션에서는 애플리케이션에 로그아웃 버튼을 추가하는 방법을 보여줍니다.

먼저 HTML 파일에 로그아웃 버튼을 추가해야 합니다.

src/index.html 파일에 다음 코드를 추가합니다.

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>TypeScript with Firebase</title>
</head>

<body>
    <button id="sign-in">Sign in with Google</button>
    <button id="sign-out">Sign out</button>
</body>

</html>
```

다음으로 로그아웃 버튼에 이벤트 리스너를 추가해야 합니다. 버튼을 클릭하면 Google 계정에서 로그아웃됩니다.

src/index.ts 파일에 다음 코드를 추가합니다.

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp(firebaseConfig);

const auth = firebase.auth();

const provider = new firebase.auth.GoogleAuthProvider();

const signInButton = document.getElementById("sign-in");

signInButton.addEventListener("click", () => {
    auth.signInWithPopup(provider);
});

const signOutButton = document.getElementById("sign-out");

signOutButton.addEventListener("click", () => {
    auth.signOut();
});

auth.onAuthStateChanged((user) => {
    if (user) {
        console.log(user.displayName);
    }
});
```

이제 로그아웃 버튼을 클릭하면 Google 계정에서 로그아웃됩니다.

# 결론

이 기사에서는 TypeScript를 Firebase와 통합하여 실시간 데이터베이스 및 인증 시스템을 만드는 방법을 설명했습니다. 이 기사가 도움이 되었기를 바랍니다. 질문이 있으시면 아래에 의견을 남겨주십시오.