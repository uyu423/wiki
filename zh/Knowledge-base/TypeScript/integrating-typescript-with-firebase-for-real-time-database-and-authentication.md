---
title: 将 TypeScript 与 Firebase 集成以实现实时数据库和身份验证
description: 
published: true
date: 2023-02-17T18:14:36.938Z
tags: 
editor: markdown
dateCreated: 2023-01-30T21:37:39.148Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Integrating TypeScript with Firebase for Real-Time Database and Authentication***English** version of this document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-firebase-for-real-time-database-and-authentication)
{.links-list}

    
    虽然本文的结构有多种可能性，但以下部分旨在作为指南：

# 介绍

TypeScript 是一种功能强大的编程语言，使开发人员能够编写既可维护又防错的代码。 Firebase 是一种流行的移动和 Web 应用程序开发平台，可提供实时数据库和身份验证服务。在本文中，我们将向您展示如何将 TypeScript 与 Firebase 集成以创建实时数据库和身份验证系统。

# 什么是打字稿？

TypeScript 是 JavaScript 的超集，它使开发人员能够编写既可维护又防错的代码。 TypeScript 被编译成 JavaScript，可以很容易地与现有的 JavaScript 代码集成。 TypeScript 通过在编译期间检查类型错误来为您的代码添加额外的安全层。这可以防止将错误引入您的代码库，并使重构和调试代码变得更加容易。

# 什么是 Firebase？

Firebase 是一种流行的移动和 Web 应用程序开发平台，可提供实时数据库和身份验证服务。 Firebase 易于使用，并为小型项目提供免费套餐。 Firebase 的实时数据库允许您跨设备实时同步数据，从而轻松构建响应式应用程序。 Firebase 的身份验证服务可以轻松地向您的应用程序添加登录和注册功能。

# 如何将 TypeScript 与 Firebase 集成

在本节中，我们将向您展示如何将 TypeScript 与 Firebase 集成以创建实时数据库和身份验证系统。

## 设置 Firebase

在开始使用 Firebase 之前，我们需要创建一个 Firebase 项目。前往 [Firebase 控制台](https://console.firebase.google.com/)，然后点击“创建项目”按钮。

输入项目名称并单击“创建项目”按钮。

创建项目后，单击“将 Firebase 添加到您的网络应用程序”按钮。

这将打开一个模式，其中包含您的 Firebase 项目的配置信息。我们稍后会需要这些信息，因此请将其复制到您的剪贴板或文本编辑器中。

## 安装 Firebase SDK

接下来，我们需要安装 Firebase SDK。我们可以使用 npm 来完成此操作。在您的终端中运行以下命令以安装 Firebase SDK：

```
npm install firebase --save
```

## 配置打字稿

TypeScript 使用 tsconfig.json 文件来配置编译器。 tsconfig.json 文件应位于项目目录的根目录中。

将以下内容添加到您的 tsconfig.json 文件中：

```json
{
    "compilerOptions": {
        "target": "es5",
        "module": "commonjs",
        "sourceMap": true
    }
}
```

在 compilerOptions 部分，我们指定我们希望 TypeScript 编译器以 es5 JavaScript 为目标，并且我们希望使用 commonjs 模块格式。我们还启用了源映射，这在调试我们的 TypeScript 代码时会很有帮助。

## 初始化 Firebase

现在我们已经安装了 Firebase SDK 并配置了 TypeScript 项目，我们可以在 TypeScript 代码中初始化 Firebase。

将以下代码添加到 src/index.ts 文件中：

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

将 firebaseConfig 对象中的占位符值替换为您的 Firebase 项目中的值。

## 创建实时数据库

Firebase 的实时数据库使您能够跨设备实时同步数据。这使得构建响应式应用程序变得容易。

要创建实时数据库，我们首先需要创建对数据库的引用。我们可以使用 firebase.database() 方法来做到这一点。

将以下代码添加到 src/index.ts 文件中：

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

接下来，我们需要创建一个我们想要跨设备同步的数据对象。我们将向我们的数据对象添加一个消息属性并将其值设置为“Hello, world!”。

将以下代码添加到 src/index.ts 文件中：

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

现在，我们需要将我们的数据对象添加到数据库中。我们可以使用 set() 方法来做到这一点。

将以下代码添加到 src/index.ts 文件中：

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

现在，我们的数据持久化在实时数据库中。我们可以通过导航到“数据”选项卡在 Firebase 控制台中查看我们的数据。

要从数据库中读取数据，我们可以使用 on() 方法。 on() 方法将事件类型和回调函数作为参数。事件类型可以是“value”、“child_added”、“child_changed”、“child_removed”或“child_moved”。只要触发事件类型，就会调用回调函数。

将以下代码添加到 src/index.ts 文件中：

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

现在，每次我们的数据更新时，都会调用回调函数并将数据记录到控制台。

## 添加身份验证

Firebase 的身份验证服务可以轻松地向您的应用程序添加登录和注册功能。 Firebase 支持多种流行的身份提供商，包括 Google、Facebook 和 Twitter。在本节中，我们将向您展示如何将 Google 登录添加到您的 TypeScript 应用程序。

首先，我们需要在我们的 Firebase 项目中启用 Google 登录提供程序。为此，请转到 Firebase 控制台并单击“登录方法”选项卡。

接下来，单击“Google”登录提供程序并启用它。

现在，我们需要配置 TypeScript 项目以使用 Google 登录提供程序。我们可以通过将提供者 ID 传递给 firebase.auth.GoogleAuthProvider() 方法来做到这一点。

将以下代码添加到 src/index.ts 文件中：

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

现在我们已经配置了登录提供程序，我们可以将登录按钮添加到我们的 HTML 文件中。

将以下代码添加到 src/index.html 文件中：

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

接下来，我们需要为登录按钮添加一个事件监听器。单击该按钮后，我们将使用我们的 Google 帐户登录。

将以下代码添加到 src/index.ts 文件中：

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

现在，当您点击登录按钮时，系统会提示您使用您的 Google 帐户登录。

登录后，您可以使用 firebase.auth().currentUser 属性访问用户信息。

将以下代码添加到 src/index.ts 文件中：

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

现在，当您使用 Google 帐户登录时，您的姓名将被记录到控制台。

## 注销

在本节中，我们将向您展示如何向您的应用程序添加注销按钮。

首先，我们需要在 HTML 文件中添加一个退出按钮。

将以下代码添加到 src/index.html 文件中：

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

接下来，我们需要为注销按钮添加一个事件监听器。单击该按钮后，我们将退出我们的 Google 帐户。

将以下代码添加到 src/index.ts 文件中：

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

现在，当您点击退出按钮时，您将退出您的 Google 帐户。

# 结论

在本文中，我们向您展示了如何将 TypeScript 与 Firebase 集成以创建实时数据库和身份验证系统。我们希望您发现这篇文章有所帮助。如果您有任何疑问，请随时在下方发表评论。