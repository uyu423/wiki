---
title: Integrating TypeScript with Firebase for Real-Time Database and Authentication
description: 
published: true
date: 2023-02-17T18:14:28.066Z
tags: 
editor: markdown
dateCreated: 2023-01-30T21:37:39.137Z
---

- [실시간 데이터베이스 및 인증을 위해 TypeScript를 Firebase와 통합***Korean** version of this document is available*](/ko/Knowledge-base/TypeScript/integrating-typescript-with-firebase-for-real-time-database-and-authentication)
{.links-list}
- [リアルタイム データベースと認証のために TypeScript を Firebase と統合する***Japanese** version of this document is available*](/ja/Knowledge-base/TypeScript/integrating-typescript-with-firebase-for-real-time-database-and-authentication)
{.links-list}
- [将 TypeScript 与 Firebase 集成以实现实时数据库和身份验证***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/TypeScript/integrating-typescript-with-firebase-for-real-time-database-and-authentication)
{.links-list}

    
    While there are many possibilities for how to structure this article, the following sections are meant to serve as a guide:

# Introduction

TypeScript is a powerful programming language that enables developers to write code that is both maintainable and error-proof. Firebase is a popular mobile and web application development platform that provides a real-time database and authentication services. In this article, we will show you how to integrate TypeScript with Firebase to create a real-time database and authentication system.

# What is TypeScript?

TypeScript is a superset of JavaScript that enables developers to write code that is both maintainable and error-proof. TypeScript is compiled to JavaScript, making it easy to integrate with existing JavaScript code. TypeScript adds an extra layer of safety to your code by checking for type errors during compilation. This prevents errors from being introduced into your codebase and makes it easier to refactor and debug your code.

# What is Firebase?

Firebase is a popular mobile and web application development platform that provides a real-time database and authentication services. Firebase is easy to use and offers a free tier for small projects. Firebase's real-time database allows you to sync data across devices in real-time, making it easy to build responsive applications. Firebase's authentication services make it easy to add sign-in and sign-up functionality to your application.

# How to Integrate TypeScript with Firebase

In this section, we will show you how to integrate TypeScript with Firebase to create a real-time database and authentication system.

## Setting up Firebase

Before we can start using Firebase, we need to create a Firebase project. Head over to the [Firebase console](https://console.firebase.google.com/) and click the "Create a Project" button.

Enter a project name and click the "Create Project" button.

Once your project is created, click on the "Add Firebase to your web app" button.

This will open a modal with your Firebase project's configuration information. We will need this information later, so copy it to your clipboard or a text editor.

## Installing the Firebase SDK

Next, we need to install the Firebase SDK. We can do this using npm.Run the following command in your terminal to install the Firebase SDK:

```
npm install firebase --save
```

## Configuring TypeScript

TypeScript uses the tsconfig.json file to configure the compiler. The tsconfig.json file should be located in the root of your project directory.

Add the following contents to your tsconfig.json file:

```json
{
    "compilerOptions": {
        "target": "es5",
        "module": "commonjs",
        "sourceMap": true
    }
}
```

In the compilerOptions section, we've specified that we want the TypeScript compiler to target es5 JavaScript and that we want to use the commonjs module format. We've also enabled source maps, which will be helpful when debugging our TypeScript code.

## Initializing Firebase

Now that we have the Firebase SDK installed and our TypeScript project configured, we can initialize Firebase in our TypeScript code.

Add the following code to the src/index.ts file:

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

Replace the placeholder values in the firebaseConfig object with the values from your Firebase project.

## Creating a Real-Time Database

Firebase's real-time database enables you to sync data across devices in real-time. This makes it easy to build responsive applications.

To create a real-time database, we first need to create a reference to the database. We can do this using the firebase.database() method.

Add the following code to the src/index.ts file:

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

Next, we need to create a data object that we want to sync across devices. We'll add a message property to our data object and set its value to "Hello, world!".

Add the following code to the src/index.ts file:

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

Now, we need to add our data object to the database. We can do this using the set() method.

Add the following code to the src/index.ts file:

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

Now, our data is persisted in the real-time database. We can view our data in the Firebase console by navigating to the "Data" tab.

To read our data from the database, we can use the on() method. The on() method takes a event type and a callback function as arguments. The event type can be "value", "child_added", "child_changed", "child_removed", or "child_moved". The callback function is invoked whenever the event type is triggered.

Add the following code to the src/index.ts file:

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

Now, every time our data is updated, the callback function will be invoked and the data will be logged to the console.

## Adding Authentication

Firebase's authentication services make it easy to add sign-in and sign-up functionality to your application. Firebase supports several popular identity providers, including Google, Facebook, and Twitter. In this section, we will show you how to add Google sign-in to your TypeScript application.

First, we need to enable the Google sign-in provider in our Firebase project. To do this, head over to the Firebase console and click on the "Sign-in method" tab.

Next, click on the "Google" sign-in provider and enable it.

Now, we need to configure our TypeScript project to use the Google sign-in provider. We can do this by passing the provider ID to the firebase.auth.GoogleAuthProvider() method.

Add the following code to the src/index.ts file:

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

Now that we have our sign-in provider configured, we can add a sign-in button to our HTML file.

Add the following code to the src/index.html file:

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

Next, we need to add an event listener to the sign-in button. When the button is clicked, we will sign in with our Google account.

Add the following code to the src/index.ts file:

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

Now, when you click the sign-in button, you will be prompted to sign in with your Google account.

Once you've signed in, you can access the user's information using the firebase.auth().currentUser property.

Add the following code to the src/index.ts file:

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

Now, when you sign in with your Google account, your name will be logged to the console.

## Logging Out

In this section, we will show you how to add a sign-out button to your application.

First, we need to add a sign-out button to our HTML file.

Add the following code to the src/index.html file:

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

Next, we need to add an event listener to the sign-out button. When the button is clicked, we will sign out of our Google account.

Add the following code to the src/index.ts file:

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

Now, when you click the sign-out button, you will be signed out of your Google account.

# Conclusion

In this article, we showed you how to integrate TypeScript with Firebase to create a real-time database and authentication system. We hope you found this article helpful. If you have any questions, feel free to leave a comment below.