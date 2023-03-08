---
title: How to Build a Progressive Web App (PWA) with Angular
description: 
published: true
date: 2023-02-06T07:55:38.041Z
tags: 
editor: markdown
dateCreated: 2023-02-06T07:55:32.542Z
---

- [Cómo construir una aplicación web progresiva (PWA) con Angular***Spanish** document is available*](/es/Knowledge-base/Common/how-to-build-a-progressive-web-app-pwa-with-angular)
{.links-list}
- [如何使用 Angular 构建渐进式 Web 应用程序 (PWA)***Chinese Simplified** document is available*](/zh/Knowledge-base/Common/how-to-build-a-progressive-web-app-pwa-with-angular)
{.links-list}
- [Angular로 프로그레시브 웹 앱(PWA)을 구축하는 방법***Korean** document is available*](/ko/Knowledge-base/Common/how-to-build-a-progressive-web-app-pwa-with-angular)
{.links-list}


# How to Build a Progressive Web App (PWA) with Angular

## What is a PWA?

A Progressive Web App (PWA) is a web application that uses modern web technologies to deliver an app-like experience to users. PWAs are responsive and fast, and can be installed on the user's home screen.

## Why build a PWA?

PWAs offer many benefits over traditional web apps, including improved performance, offline capability, and app-like features.

## How to build a PWA with Angular

Angular is a popular framework for building PWAs. In this article, we'll show you how to create a PWA with Angular.

### 1. Create a new Angular project

First, you'll need to create a new Angular project. You can do this using the Angular CLI.

Run the following command to create a new Angular project:

```
ng new my-pwa
```

This will create a new folder called `my-pwa` with your Angular project.

### 2. Add PWA features

Next, you'll need to add PWA features to your Angular project. You can do this using the @angular/pwa package.

First, install the @angular/pwa package:

```
npm install @angular/pwa --save
```

Next, add the PWA manifest to your `index.html` file:

```html
<link rel="manifest" href="/manifest.json">
```

Finally, generate a service worker file:

```
ng generate service-worker
```

This will create a file called `ngsw-worker.js` in your `src/` folder.

### 3. Test your PWA

Now that you've added PWA features to your Angular project, you can test your PWA.

To test your PWA, you'll need to run a local server. The Angular CLI includes a development server, so you can use that.

Run the following command to start the development server:

```
ng serve
```

Now, open your browser and go to http://localhost:4200/. You should see your Angular app running.

To test the PWA features, you'll need to install the [Lighthouse](https://developers.google.com/web/tools/lighthouse/) extension for Chrome.

Once you've installed Lighthouse, open the extension and click the "Generate report" button.

Lighthouse will analyze your app and provide a report. The report will tell you whether your app passes the PWA checklist.

If your app doesn't pass the checklist, try adding more PWA features. For example, you can add [push notifications](https://developers.google.com/web/fundamentals/getting-started/codelabs/push-notifications/) or [background sync](https://developers.google.com/web/fundamentals/getting-started/primers/background-sync).

## Conclusion

In this article, we've shown you how to build a Progressive Web App with Angular. PWAs offer many benefits over traditional web apps, including improved performance, offline capability, and app-like features. With Angular, it's easy to add PWA features to your web app.