---
title: 058: Implementación de aplicaciones sin conexión primero con Nest.js y Service Workers
description: 
published: true
date: 2023-02-15T21:33:09.079Z
tags: 
editor: markdown
dateCreated: 2023-02-15T21:33:00.821Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [058: Implementing offline-first applications with Nest.js and Service Workers***English** document is available*](/en/Knowledge-base/Nest-js/Learning/058-implementing-offline-first-applications-with-nest-js-and-service-workers)
{.links-list}


058: Implementación de aplicaciones sin conexión primero con Nest.js y Service Workers

Los trabajadores de servicio son una herramienta poderosa para hacer que las aplicaciones web funcionen sin conexión. Con los trabajadores de servicio, puede interceptar solicitudes de red y entregar respuestas almacenadas en caché, brindando a sus usuarios una mejor experiencia incluso cuando están desconectados.

En esta publicación, le mostraremos cómo usar trabajadores de servicio para hacer que una aplicación Nest.js funcione sin conexión. Comenzaremos creando una aplicación Nest.js "hola mundo" simple. Luego, registraremos un trabajador de servicio y lo usaremos para almacenar en caché los activos estáticos de nuestra aplicación. Finalmente, usaremos el trabajador de servicio para entregar una respuesta almacenada en caché cuando el usuario esté desconectado.

Creación de una aplicación Nest.js

Comencemos por crear una aplicación Nest.js "hola mundo" simple. Primero, cree un nuevo archivo llamado app.js y agregue el siguiente código:

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

Este código crea una aplicación Express.js simple que escucha en el puerto 3000 y responde "¡Hola, mundo!" cuando visita la URL raíz.

A continuación, instale la dependencia de Express.js:

```
npm install --save express
```

Ahora, puede iniciar la aplicación ejecutando el siguiente comando:

```
node app.js
```

Debería ver el siguiente resultado:

```
Example app listening on port 3000!
```

Ahora puede visitar http://localhost:3000 en su navegador web y debería ver el mensaje "¡Hola, mundo!" mensaje.

Registro de un trabajador de servicio

Ahora que tenemos una aplicación Nest.js básica en funcionamiento, registremos un trabajador de servicio. Los trabajadores del servicio están registrados en el archivo JavaScript principal de su aplicación web. En nuestro caso, ese es el archivo app.js.

Agrega el siguiente código al final del archivo app.js:

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

Este código verifica si el navegador admite trabajadores de servicios. Si lo son, registra el archivo del trabajador del servicio (sw.js). Si los trabajadores de servicio no son compatibles, imprime un mensaje de error en la consola.

Luego, cree un nuevo archivo llamado sw.js en el directorio raíz de su proyecto. Este es el archivo del trabajador del servicio. Agregue el siguiente código al archivo sw.js:

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

Este código configura tres detectores de eventos: 'instalar', 'activar' y 'buscar'. El evento 'instalar' se activa cuando se instala por primera vez el trabajador de servicio. El evento 'activar' se activa cuando se activa el trabajador del servicio. El evento 'buscar' se activa cada vez que se realiza una solicitud de red.

Agregaremos código a cada uno de estos detectores de eventos en la siguiente sección.

Almacenamiento en caché de activos estáticos

Ahora que tenemos un trabajador de servicio registrado, usémoslo para almacenar en caché los activos estáticos de nuestra aplicación. Los activos estáticos son archivos que no cambian con frecuencia, como imágenes, archivos CSS y archivos JavaScript.

Primero, agreguemos algo de código al detector de eventos 'instalar'. Este código almacenará en caché los activos estáticos cuando se instale el trabajador de servicio:

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

Este código abre un caché llamado 'static-cache' y agrega los archivos enumerados al caché. El método 'waitUntil' le dice al navegador que mantenga vivo al trabajador del servicio hasta que se complete el almacenamiento en caché.

A continuación, agreguemos algo de código al detector de eventos 'activar'. Este código eliminará todos los cachés antiguos que no sean necesarios:

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

Este código obtiene una lista de todos los cachés, filtra los cachés que comienzan con 'static-' pero no son 'static-cache' y los elimina.

Finalmente, agreguemos algo de código al detector de eventos 'fetch'. Este código servirá la respuesta almacenada en caché si existe, o de lo contrario obtendrá la respuesta de la red:

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

Este código comprueba la 'caché estática' en busca de una solicitud coincidente. Si encuentra una coincidencia, devuelve la respuesta almacenada en caché. Si no encuentra una coincidencia, obtiene la respuesta de la red.

Probando al trabajador de servicio

Ahora que hemos agregado código a nuestro trabajador de servicio, probémoslo para asegurarnos de que funciona.

Primero, detenga el servidor Nest.js si se está ejecutando. Luego, ejecute el siguiente comando para iniciar el servidor en modo de producción:

```
NODE_ENV=production node app.js
```

Este comando establece la variable de entorno NODE_ENV en 'producción' e inicia el servidor.

A continuación, abra http://localhost:3000 en su navegador web y abra las herramientas de desarrollo. Haga clic en la pestaña 'Aplicación' y debería ver la sección 'Trabajadores de servicio'. Debería ver que su trabajador de servicio está registrado y está 'activo'.

Ahora, realice un cambio en el detector de eventos 'fetch' en el archivo sw.js. Por ejemplo, podría cambiar 'static-cache' a 'my-cache'. Luego, guarde el archivo y actualice la página. Debería ver que el trabajador del servicio está 'actualizado' y está 'esperando para activarse'.

Para probar que el trabajador del servicio está funcionando, abra la pestaña 'Red' en las herramientas de desarrollo y asegúrese de que la casilla de verificación 'Deshabilitar caché' esté marcada. Luego, actualice la página. Debería ver que el trabajador del servicio está entregando la respuesta almacenada en caché.

Si realiza un cambio en el detector de eventos 'fetch' en el archivo sw.js, deberá anular el registro del trabajador del servicio y volver a registrarlo. Para hacer esto, abra la pestaña 'Aplicación' en las herramientas para desarrolladores y haga clic en el botón 'Cancelar registro'. Luego, actualice la página y debería ver que el trabajador del servicio está registrado nuevamente.

Conclusión

En esta publicación, le mostramos cómo usar trabajadores de servicio para hacer que una aplicación Nest.js funcione sin conexión. Comenzamos creando una aplicación Nest.js simple "hola mundo". Luego, registramos un trabajador de servicio y lo usamos para almacenar en caché los activos estáticos de nuestra aplicación. Finalmente, usamos el trabajador de servicio para entregar una respuesta en caché cuando el usuario está desconectado.