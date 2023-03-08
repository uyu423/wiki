---
title: 058：使用 Nest.js 和 Service Workers 实现离线优先应用程序
description: 
published: true
date: 2023-02-15T21:33:09.079Z
tags: 
editor: markdown
dateCreated: 2023-02-15T21:33:00.817Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [058: Implementing offline-first applications with Nest.js and Service Workers***English** document is available*](/en/Knowledge-base/Nest-js/Learning/058-implementing-offline-first-applications-with-nest-js-and-service-workers)
{.links-list}


058：使用 Nest.js 和 Service Workers 实现离线优先应用程序

Service Worker 是让 Web 应用程序离线工作的强大工具。使用服务工作者，您可以拦截网络请求并提供缓存的响应，即使用户处于离线状态也能为他们提供更好的体验。

在这篇文章中，我们将向您展示如何使用 Service Worker 使 Nest.js 应用程序离线工作。我们将从创建一个简单的“hello world”Nest.js 应用程序开始。然后，我们将注册一个 service worker 并使用它来缓存我们应用程序的静态资产。最后，我们将使用 service worker 在用户离线时提供缓存响应。

创建 Nest.js 应用程序

让我们从创建一个简单的“hello world”Nest.js 应用程序开始。首先，创建一个名为 app.js 的新文件并添加以下代码：

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello, world!');
});

app.listen(3000, () => {
  console.log('Example app listening on port 3000!');
});
```

此代码创建了一个简单的 Express.js 应用程序，该应用程序侦听端口 3000 并以“Hello, world!”响应。当您访问根 URL 时。

接下来，安装 Express.js 依赖项：

```
npm install --save express
```

现在，您可以通过运行以下命令来启动应用程序：

```
node app.js
```

您应该看到以下输出：

```
Example app listening on port 3000!
```

您现在可以在 Web 浏览器中访问 http://localhost:3000，您应该会看到“Hello, world!”。信息。

注册服务人员

现在我们已经启动并运行了一个基本的 Nest.js 应用程序，让我们注册一个 service worker。 Service Worker 在 Web 应用程序的主 JavaScript 文件中注册。在我们的例子中，这是 app.js 文件。

将以下代码添加到 app.js 文件的底部：

```javascript
if ('serviceWorker' in navigator) {
  navigator.serviceWorker
    .register('/sw.js')
    .then(function() {
      console.log('Service worker registered!');
    })
    .catch(function(err) {
      console.log('Service worker registration failed: ', err);
    });
} else {
  console.log('Service workers are not supported.');
}
```

此代码检查浏览器是否支持服务工作者。如果是，它会注册服务工作者文件 (sw.js)。如果不支持服务工作者，它会向控制台打印一条错误消息。

接下来，在项目的根目录中创建一个名为 sw.js 的新文件。这是服务工作者文件。将以下代码添加到 sw.js 文件中：

```javascript
self.addEventListener('install', function(event) {
  // Perform install steps
});

self.addEventListener('activate', function(event) {
  // Perform activate steps
});

self.addEventListener('fetch', function(event) {
  // Perform fetch steps
});
```

此代码设置了三个事件侦听器：'install'、'activate' 和'fetch'。首次安装 Service Worker 时会触发 'install' 事件。当 service worker 被激活时，'activate' 事件被触发。每次发出网络请求时都会触发“获取”事件。

我们将在下一节中为每个事件侦听器添加代码。

缓存静态资产

现在我们已经注册了一个服务工作者，让我们用它来缓存我们应用程序的静态资产。静态资产是不经常更改的文件，例如图像、CSS 文件和 JavaScript 文件。

首先，让我们向“安装”事件侦听器添加一些代码。此代码将在安装 service worker 时缓存静态资产：

```javascript
self.addEventListener('install', function(event) {
  event.waitUntil(
    caches.open('static-cache').then(function(cache) {
      return cache.addAll([
        '/',
        '/app.js',
        '/styles.css',
        '/images/logo.png'
      ]);
    })
  );
});
```

此代码打开名为“static-cache”的缓存并将列出的文件添加到缓存中。 'waitUntil' 方法告诉浏览器让 service worker 保持活动状态，直到缓存完成。

接下来，让我们向“激活”事件侦听器添加一些代码。此代码将删除任何不需要的旧缓存：

```javascript
self.addEventListener('activate', function(event) {
  event.waitUntil(
    caches.keys().then(function(cacheNames) {
      return Promise.all(
        cacheNames.filter(function(cacheName) {
          return cacheName.startsWith('static-') && cacheName != 'static-cache';
        }).map(function(cacheName) {
          return caches.delete(cacheName);
        })
      );
    })
  );
});
```

此代码获取所有缓存的列表，过滤掉以'static-'开头但不是'static-cache'的缓存，并将其删除。

最后，让我们向“获取”事件侦听器添加一些代码。此代码将提供缓存的响应（如果存在），否则它将从网络获取响应：

```javascript
self.addEventListener('fetch', function(event) {
  event.respondWith(
    caches.match(event.request).then(function(response) {
      if (response) {
        return response;
      }
      return fetch(event.request);
    })
  );
});
```

此代码检查匹配请求的“静态缓存”。如果找到匹配项，它会返回缓存的响应。如果找不到匹配项，它会从网络中获取响应。

测试服务工作者

现在我们已经将代码添加到我们的 service worker，让我们测试它以确保它正常工作。

首先，如果 Nest.js 服务器正在运行，请将其停止。然后，运行以下命令以生产模式启动服务器：

```
NODE_ENV=production node app.js
```

此命令将 NODE_ENV 环境变量设置为“production”并启动服务器。

接下来，在 Web 浏览器中打开 http://localhost:3000 并打开开发人员工具。单击“应用程序”选项卡，您应该会看到“Service Workers”部分。您应该看到您的 service worker 已注册并且处于“活动”状态。

现在，更改 sw.js 文件中的“获取”事件侦听器。例如，您可以将“静态缓存”更改为“我的缓存”。然后，保存文件并刷新页面。您应该看到服务工作线程已“更新”并且正在“等待激活”。

要测试 service worker 是否正常工作，请打开开发人员工具中的“网络”选项卡，并确保选中“禁用缓存”复选框。然后，刷新页面。您应该看到 service worker 正在为缓存的响应提供服务。

如果您对 sw.js 文件中的“获取”事件侦听器进行了更改，则需要注销服务工作者并重新注册。为此，请打开开发人员工具中的“应用程序”选项卡，然后单击“注销”按钮。然后，刷新页面，你应该会看到 service worker 再次注册了。

结论

在这篇文章中，我们向您展示了如何使用 Service Worker 使 Nest.js 应用程序离线工作。我们从创建一个简单的“hello world”Nest.js 应用程序开始。然后，我们注册了一个 service worker 并用它来缓存我们应用程序的静态资产。最后，我们使用 service worker 在用户离线时提供缓存响应。