---
title: How to Build a Real-Time Application with Firebase
description: 
published: true
date: 2023-02-01T13:23:48.148Z
tags: 
editor: markdown
dateCreated: 2023-02-01T13:23:44.584Z
---

- [Firebase로 실시간 애플리케이션을 구축하는 방법***Korean** version of this document is available*](/ko/Knowledge-base/Common/how-to-build-a-real-time-application-with-firebase)
{.links-list}
- [如何使用 Firebase 构建实时应用程序***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Common/how-to-build-a-real-time-application-with-firebase)
{.links-list}



# How to Build a Real-Time Application with Firebase

Firebase is a powerful platform for building real-time applications. It provides a rich set of features, including a NoSQL database, user authentication, static hosting, and more.

In this article, we'll show you how to build a real-time application with Firebase. We'll use the NoSQL database to store data, the user authentication to secure our app, and the static hosting to deploy our app.

## Setting up Firebase

The first thing you need to do is create a Firebase account and create a new project.

![Firebase Console](https://i.imgur.com/aVORi4k.png)

Once you've created your project, you'll be taken to the project dashboard. Here, you can find your project ID and project URL. You'll need these later.

![Firebase Project Dashboard](https://i.imgur.com/5bF9IyG.png)

## Creating a NoSQL Database

Firebase provides a powerful NoSQL database for storing data. To create a database, go to the Database tab in the Firebase console and click on the "Create database" button.

![Firebase Console](https://i.imgur.com/pZhCkYE.png)

You'll be asked to select a security rule for your database. For this example, we'll choose the "Lock mode" which will prevent anyone from accessing our database unless they're authenticated.

![Firebase Console](https://i.imgur.com/W0zJgwc.png)

Once you've created your database, you can start adding data to it. To do this, click on the "Add data" button.

![Firebase Console](https://i.imgur.com/V0CgqEH.png)

You can now add data to your database. For this example, we'll add a message.

![Firebase Console](https://i.imgur.com/TGiuk72.png)

## Authenticating Users

Firebase provides a powerful authentication system for securing your app. To set up authentication, go to the Auth tab in the Firebase console and click on the "Sign in method" tab.

![Firebase Console](https://i.imgur.com/3vHKTGi.png)

Click on the "Email/Password" sign-in method and enable it.

![Firebase Console](https://i.imgur.com/ZU6kCbJ.png)

Now that the sign-in method is enabled, you can create users. To do this, go to the "Users" tab and click on the "Add user" button.

![Firebase Console](https://i.imgur.com/XgbG0z7.png)

Enter the user's email and password and click on the "Add user" button.

![Firebase Console](https://i.imgur.com/V0CgqEH.png)

The user will now be able to sign in to your app.

## Deploying your app

Firebase provides a static hosting service for deploying your app. To set up hosting, go to the Hosting tab in the Firebase console and click on the "Get started" button.

![Firebase Console](https://i.imgur.com/7DpjkZI.png)

Firebase will now walk you through the process of setting up hosting. First, you'll need to install the Firebase CLI.

![Firebase Console](https://i.imgur.com/l0G9UO4.png)

Once the CLI is installed, you can deploy your app. To do this, run the following command from the root of your project directory.

```
firebase deploy
```

This will deploy your app to Firebase's servers.

## Conclusion

In this article, we've shown you how to build a real-time application with Firebase. We've used the NoSQL database to store data, the user authentication to secure our app, and the static hosting to deploy our app.