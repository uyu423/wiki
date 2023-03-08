---
title: 058: Implementing offline-first applications with Nest.js and Service Workers
description: 
published: true
date: 2023-02-15T21:33:03.589Z
tags: 
editor: markdown
dateCreated: 2023-02-15T21:33:00.826Z
---

- [058: Implementación de aplicaciones sin conexión primero con Nest.js y Service Workers***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/058-implementing-offline-first-applications-with-nest-js-and-service-workers)
{.links-list}
- [058：使用 Nest.js 和 Service Workers 实现离线优先应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/058-implementing-offline-first-applications-with-nest-js-and-service-workers)
{.links-list}
- [058: Nest.js 및 서비스 워커로 오프라인 우선 애플리케이션 구현***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/058-implementing-offline-first-applications-with-nest-js-and-service-workers)
{.links-list}


058: Implementing offline-first applications with Nest.js and Service Workers

Service workers are a powerful tool for making web applications work offline. With service workers, you can intercept network requests and serve cached responses, giving your users a better experience even when they're offline.

In this post, we'll show you how to use service workers to make a Nest.js application work offline. We'll start by creating a simple "hello world" Nest.js application. Then, we'll register a service worker and use it to cache our application's static assets. Finally, we'll use the service worker to serve a cached response when the user is offline.

Creating a Nest.js application

Let's start by creating a simple "hello world" Nest.js application. First, create a new file called app.js and add the following code:

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

This code creates a simple Express.js application that listens on port 3000 and responds with "Hello, world!" when you visit the root URL.

Next, install the Express.js dependency:

```
npm install --save express
```

Now, you can start the application by running the following command:

```
node app.js
```

You should see the following output:

```
Example app listening on port 3000!
```

You can now visit http://localhost:3000 in your web browser and you should see the "Hello, world!" message.

Registering a service worker

Now that we have a basic Nest.js application up and running, let's register a service worker. Service workers are registered in the main JavaScript file of your web application. In our case, that's the app.js file.

Add the following code to the bottom of the app.js file:

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

This code checks to see if service workers are supported by the browser. If they are, it registers the service worker file (sw.js). If service workers are not supported, it prints an error message to the console.

Next, create a new file called sw.js in the root directory of your project. This is the service worker file. Add the following code to the sw.js file:

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

This code sets up three event listeners: 'install', 'activate', and 'fetch'. The 'install' event is fired when the service worker is first installed. The 'activate' event is fired when the service worker is activated. The 'fetch' event is fired every time a network request is made.

We'll add code to each of these event listeners in the next section.

Caching static assets

Now that we have a service worker registered, let's use it to cache our application's static assets. Static assets are files that don't change often, such as images, CSS files, and JavaScript files.

First, let's add some code to the 'install' event listener. This code will cache the static assets when the service worker is installed:

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

This code opens a cache called 'static-cache' and adds the files listed to the cache. The 'waitUntil' method tells the browser to keep the service worker alive until the caching is complete.

Next, let's add some code to the 'activate' event listener. This code will delete any old caches that are not needed:

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

This code gets a list of all the caches, filters out the caches that start with 'static-' but are not 'static-cache', and deletes them.

Finally, let's add some code to the 'fetch' event listener. This code will serve the cached response if it exists, or else it will fetch the response from the network:

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

This code checks the 'static-cache' for a matching request. If it finds a match, it returns the cached response. If it doesn't find a match, it fetches the response from the network.

Testing the service worker

Now that we've added code to our service worker, let's test it to make sure it's working.

First, stop the Nest.js server if it's running. Then, run the following command to start the server in production mode:

```
NODE_ENV=production node app.js
```

This command sets the NODE_ENV environment variable to 'production' and starts the server.

Next, open http://localhost:3000 in your web browser and open the developer tools. Click on the 'Application' tab and you should see the 'Service Workers' section. You should see that your service worker is registered and is 'active'.

Now, make a change to the 'fetch' event listener in the sw.js file. For example, you could change the 'static-cache' to 'my-cache'. Then, save the file and refresh the page. You should see that the service worker is 'updated' and is 'waiting to activate'.

To test that the service worker is working, open the 'Network' tab in the developer tools and make sure that the 'Disable cache' checkbox is checked. Then, refresh the page. You should see that the service worker is serving the cached response.

If you make a change to the 'fetch' event listener in the sw.js file, you'll need to unregister the service worker and register it again. To do this, open the 'Application' tab in the developer tools and click on the 'Unregister' button. Then, refresh the page and you should see that the service worker is registered again.

Conclusion

In this post, we've shown you how to use service workers to make a Nest.js application work offline. We've started by creating a simple "hello world" Nest.js application. Then, we've registered a service worker and used it to cache our application's static assets. Finally, we've used the service worker to serve a cached response when the user is offline.