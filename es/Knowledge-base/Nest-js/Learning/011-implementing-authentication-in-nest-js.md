---
title: 011: Implementando autenticación en Nest.js
description: 
published: true
date: 2023-02-14T21:32:53.955Z
tags: 
editor: markdown
dateCreated: 2023-02-14T21:32:46.277Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [011: Implementing authentication in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/011-implementing-authentication-in-nest-js)
{.links-list}


# Implementando autenticación en Nest.js

Nest.js es un marco para crear aplicaciones Node.js. Utiliza TypeScript y está influenciado por Angular. Nest.js proporciona una forma de estructurar el código que es fácil de usar y mantener.

La autenticación es un proceso de verificación de la identidad de un usuario. Nest.js proporciona una forma de implementar la autenticación en las aplicaciones. En esta publicación, aprenderemos cómo implementar la autenticación en una aplicación Nest.js.

## ¿Qué es la autenticación?

La autenticación es el proceso de verificar la identidad de un usuario. Se utiliza para proteger los recursos del acceso no autorizado. La autenticación generalmente se realiza solicitando al usuario que proporcione un nombre de usuario y una contraseña. Luego, el nombre de usuario y la contraseña se verifican con una base de datos de usuarios autorizados.

## ¿Qué es Nest.js?

Nest.js es un marco para crear aplicaciones Node.js. Utiliza TypeScript y está influenciado por Angular. Nest.js proporciona una forma de estructurar el código que es fácil de usar y mantener.

## ¿Cuáles son los beneficios de usar Nest.js?

Hay muchos beneficios de usar Nest.js, algunos de los cuales son:

- Nest.js proporciona una forma de estructurar el código que es fácil de usar y mantener.
- Nest.js es fácil de aprender y usar.
- Nest.js se basa en TypeScript, que es un superconjunto de JavaScript. Esto significa que el código de Nest.js es más fácil de leer y comprender.
- Nest.js está influenciado por Angular. Esto significa que el código de Nest.js es fácil de leer y comprender para aquellos que están familiarizados con Angular.

## ¿Qué es TypeScript?

TypeScript es un superconjunto de JavaScript. Esto significa que el código TypeScript es más fácil de leer y comprender. TypeScript también se escribe, lo que significa que puede detectar errores en tiempo de compilación. Esto hace que el código TypeScript sea más confiable.

## ¿Cuál es la diferencia entre JavaScript y TypeScript?

La diferencia entre JavaScript y TypeScript es que TypeScript se escribe y JavaScript no. Esto significa que TypeScript puede detectar errores en tiempo de compilación. Esto hace que el código TypeScript sea más confiable.

## ¿Cuál es la diferencia entre Node.js y Nest.js?

La diferencia entre Node.js y Nest.js es que Nest.js está construido sobre Node.js. Nest.js proporciona una forma de estructurar el código que es fácil de usar y mantener.

## ¿Cómo instalo Nest.js?

Nest.js se puede instalar usando el Administrador de paquetes de Node.js (npm). Para instalar Nest.js, abra una terminal y ejecute el siguiente comando:

```
npm install -g @nestjs/cli
```

## ¿Cómo creo un proyecto Nest.js?

Para crear un proyecto Nest.js, abra una terminal y ejecute el siguiente comando:

```
nest new project-name
```

Reemplace project-name con el nombre de su proyecto. Esto creará un nuevo proyecto Nest.js con el nombre project-name.

## ¿Cómo ejecuto un proyecto Nest.js?

Para ejecutar un proyecto Nest.js, abra una terminal y navegue hasta el directorio del proyecto. Luego, ejecuta el siguiente comando:

```
nest start
```

Esto iniciará el servidor Nest.js. Se podrá acceder al servidor en http://localhost:3000.

## ¿Cuáles son los pasos para implementar la autenticación en Nest.js?

Hay muchas formas de implementar la autenticación en Nest.js. En esta publicación, usaremos la biblioteca Passport.js para implementar la autenticación. Passport.js es una biblioteca de autenticación popular para Node.js.

Los pasos para implementar la autenticación en Nest.js son:

1. Instale la biblioteca Passport.js.
2. Configure Passport.js.
3. Cree una página de inicio de sesión.
4. Cree una página de cierre de sesión.
5. Proteja los recursos con autenticación.

## Paso 1: Instale la biblioteca Passport.js

El primer paso es instalar la biblioteca Passport.js. Passport.js es una biblioteca de autenticación popular para Node.js. Para instalar la biblioteca Passport.js, abra una terminal y ejecute el siguiente comando:

```
npm install passport
```

## Paso 2: Configurar Passport.js

El siguiente paso es configurar Passport.js. Passport.js necesita saber cómo verificar la identidad de un usuario. Esto se hace proporcionando una estrategia. Hay muchas estrategias que se pueden usar con Passport.js. En esta publicación, utilizaremos LocalStrategy.

LocalStrategy es una estrategia que utiliza un nombre de usuario y una contraseña para verificar la identidad de un usuario. Para usar LocalStrategy, debemos proporcionar una función de devolución de llamada. Esta función de devolución de llamada se llamará cuando Passport.js necesite verificar la identidad de un usuario.

La función de devolución de llamada de LocalStrategy tiene la siguiente firma:

```
function(username, password, done) {

}
```

Los argumentos de nombre de usuario y contraseña son el nombre de usuario y la contraseña que ha proporcionado el usuario. La devolución de llamada realizada es una función que se utiliza para devolver el resultado de la verificación. La devolución de llamada realizada tiene la siguiente firma:

```
function(error, user, info) {

}
```

Si la verificación fue exitosa, el argumento de usuario contendrá el objeto de usuario. Si la verificación no tuvo éxito, los argumentos de error e información contendrán información sobre el error.

Para configurar LocalStrategy, necesitamos crear un archivo llamado pasaporte.js en el directorio raíz del proyecto. El archivo pasaporte.js debería tener este aspecto:

```javascript
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;

passport.use(new LocalStrategy(
  function(username, password, done) {
    //Verify the username and password here
  }
));
```

Reemplace el comentario //Verifique el nombre de usuario y la contraseña aquí con el código para verificar el nombre de usuario y la contraseña.

## Paso 3: Cree una página de inicio de sesión

El siguiente paso es crear una página de inicio de sesión. La página de inicio de sesión será una página HTML que contiene un formulario. El formulario tendrá campos para el nombre de usuario y la contraseña. El formulario se enviará a la ruta /login.

Para crear la página de inicio de sesión, cree un archivo llamado login.html en el directorio raíz del proyecto. El archivo login.html debería verse así:

```html
<html>
<body>
  <form action="/login" method="post">
    <label>Username:</label>
    <input type="text" name="username">
    <label>Password:</label>
    <input type="password" name="password">
    <input type="submit" value="Login">
  </form>
</body>
</html>
```

## Paso 4: Crear una página de cierre de sesión

El siguiente paso es crear una página de cierre de sesión. La página de cierre de sesión será una página HTML que contiene un formulario. El formulario tendrá un campo para el nombre de usuario. El formulario se enviará a la ruta /logout.

Para crear la página de cierre de sesión, cree un archivo llamado logout.html en el directorio raíz del proyecto. El archivo logout.html debería verse así:

```html
<html>
<body>
  <form action="/logout" method="post">
    <label>Username:</label>
    <input type="text" name="username">
    <input type="submit" value="Logout">
  </form>
</body>
</html>
```

## Paso 5: proteger los recursos con autenticación

El paso final es proteger los recursos con autenticación. Para hacer esto, necesitamos crear una función de middleware que verifique si el usuario está autenticado. Si el usuario no está autenticado, la función de middleware redirigirá al usuario a la página de inicio de sesión.

Para crear la función de middleware, cree un archivo llamado auth.js en el directorio raíz del proyecto. El archivo auth.js debería verse así:

```javascript
const passport = require('passport');

function isAuthenticated(req, res, next) {
  if (req.isAuthenticated()) {
    return next();
  }
  res.redirect('/login');
}

module.exports = {
  isAuthenticated: isAuthenticated
};
```

La función isAuthenticated() es la función de middleware. La función comprueba si el usuario está autenticado. Si el usuario no está autenticado, la función lo redirige a la página de inicio de sesión.

La función de middleware se puede utilizar para proteger cualquier ruta. Por ejemplo, para proteger la ruta /admin, podemos usar el siguiente código:

```javascript
app.get('/admin', auth.isAuthenticated, (req, res) => {
  // The authenticated user can access this route
});
```

## Conclusión

En esta publicación, aprendimos cómo implementar la autenticación en una aplicación Nest.js. Instalamos la biblioteca Passport.js y la configuramos para usar LocalStrategy. También creamos una página de inicio de sesión y una página de cierre de sesión. Finalmente, protegemos los recursos con autenticación.