---
title: 057：将 Nest.js 与服务工作者一起使用
description: 
published: true
date: 2023-02-15T20:32:42.846Z
tags: 
editor: markdown
dateCreated: 2023-02-15T20:32:35.147Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [057: Using Nest.js with Service Workers***English** document is available*](/en/Knowledge-base/Nest-js/Learning/057-using-nest-js-with-service-workers)
{.links-list}


# 将 Nest.js 与服务工作者一起使用

Service Workers 是一个强大的工具，可以极大地提高 Web 应用程序的性能。然而，它们附带了一些警告，即使是经验丰富的开发人员也会被绊倒。在这篇文章中，我们将看看如何将 Nest.js 与 Service Worker 一起使用来避免其中的一些陷阱。

## 什么是 Service Worker？

Service Worker 是一个在您的网络浏览器后台运行并拦截网络请求的脚本。这允许他们做一些事情，比如缓存资源以供离线使用或根据网络条件提供不同的内容。

## 什么是 Nest.js？

Nest.js 是一个使用 JavaScript 构建服务器端应用程序的框架。它建立在 Express Web 框架之上，并使用 TypeScript 提供类型安全。

## 将 Nest.js 与服务工作者一起使用

将 Nest.js 与服务工作者一起使用是一个两步过程。首先，您需要使用 Nest.js 注册 Service Worker 脚本。这可以在 `app.module.ts` 文件中完成：

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { ServiceWorkerModule } from '@nestjs/service-worker';

@Module({
  imports: [
    ServiceWorkerModule.register('/ngsw-worker.js'),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

第二步是在项目的根目录中创建 ngsw-worker.js 文件。该文件包含 Service Worker 代码，将由 Nest.js 提供服务。

```javascript
// This is the code for the Service Worker

self.addEventListener('fetch', event => {
  // This is where you can handle network requests
  // and serve different content based on the network conditions
});
```

现在您对如何将 Nest.js 与 Service Workers 结合使用有了基本的了解，让我们来看看它们可以提供的一些好处。

## Service Worker 的好处

Service Workers 可以为您的 Web 应用程序提供许多好处，包括离线支持、后台数据同步和推送通知。

### 离线支持

Service Workers 最常见的用例之一是为 Web 应用程序提供离线支持。这可以通过在 Service Worker 的“fetch”事件处理程序中缓存资源来实现。

```javascript
// This is the code for the Service Worker

self.addEventListener('fetch', event => {
  // Try to fetch the resource from the network first
  event.respondWith(
    fetch(event.request).catch(() => {
      // If the network request fails, try to get the resource from the cache
      return caches.match(event.request);
    })
  );
});
```

### 后台数据同步

Service Workers 的另一个常见用例是执行后台数据同步。这对于使用来自远程服务器的数据更新本地数据库之类的事情很有用。

```javascript
// This is the code for the Service Worker

self.addEventListener('sync', event => {
  // This is where you can perform background data synchronization
});
```

### 推送通知

Service Worker 也可用于向用户发送推送通知。这对于警报或更新之类的事情很有用。

```javascript
// This is the code for the Service Worker

self.addEventListener('push', event => {
  // This is where you can send push notifications to users
});
```

## Service Worker 的陷阱

尽管有很多好处，但 Service Workers 也有一些警告，即使是经验丰富的开发人员也会被绊倒。

### 安全

Service Workers 最大的担忧之一是安全性。由于 Service Worker 可以访问网络请求，因此可以使用它们来执行中间人攻击。

为了降低这种风险，重要的是只从可信来源注册服务工作者。对于 Nest.js，这意味着只注册由 Nest.js 提供服务的服务工作者。

### 缓存

Service Worker 的另一个潜在缺陷是缓存。使用 Service Worker 缓存资源时，设置正确的缓存标头很重要。否则，资源可能无法正确缓存，或者缓存时间过长。

```javascript
// This is the code for the Service Worker

self.addEventListener('fetch', event => {
  // Try to fetch the resource from the network first
  event.respondWith(
    fetch(event.request).then(response => {
      // If the network request succeeds, cache the response
      return caches.open(CACHE_NAME).then(cache => {
        cache.put(event.request, response.clone());
        return response;
      });
    }).catch(() => {
      // If the network request fails, try to get the resource from the cache
      return caches.match(event.request);
    })
  );
});
```

## 结论

在这篇文章中，我们了解了如何将 Nest.js 与 Service Workers 结合使用。我们还看到了 Service Workers 可以提供的一些好处，以及您需要注意的一些陷阱。

如果您有兴趣了解有关 Service Worker 的更多信息，我建议您查看以下资源：

- [服务工作者：简介](https://developers.google.com/web/fundamentals/primers/service-workers)
- [使用服务工作者](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers)
- [Service Worker 生命周期](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers# the_serviceworker_lifecycle)