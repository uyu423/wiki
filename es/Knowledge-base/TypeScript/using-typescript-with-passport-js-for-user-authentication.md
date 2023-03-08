---
title: Uso de TypeScript con Passport.js para la autenticación de usuarios
description: 
published: true
date: 2023-02-10T16:17:46.980Z
tags: 
editor: markdown
dateCreated: 2023-02-10T16:17:45.298Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Using TypeScript with Passport.js for User Authentication***English** document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-passport-js-for-user-authentication)
{.links-list}


# Uso de TypeScript con Passport.js para la autenticación de usuarios

Passport.js es un middleware de autenticación flexible para Node.js. Se puede usar para autenticar a los usuarios mediante una variedad de estrategias, incluido el nombre de usuario y la contraseña, Facebook, Twitter y más.

TypeScript es un superconjunto de JavaScript que agrega verificación de tipo estático y otras características. TypeScript se usa ampliamente en aplicaciones grandes y su compatibilidad con módulos, clases e interfaces lo convierte en una buena opción para trabajar con Passport.js.

En este artículo, veremos cómo usar TypeScript con Passport.js para crear un sistema de autenticación de usuarios. Comenzaremos configurando un proyecto con TypeScript y Express.js. Luego, instalaremos Passport.js y lo configuraremos para usarlo con TypeScript. Finalmente, agregaremos algo de código TypeScript para implementar una estrategia simple de autenticación de nombre de usuario y contraseña.

## Configuración de un proyecto TypeScript

Para comenzar, necesitamos crear un nuevo proyecto de TypeScript. Usaremos el marco web [Express.js](https://expressjs.com/) y la plantilla de proyecto [TypeScript Node Starter](https://github.com/Microsoft/TypeScript-Node-Starter).

Primero, instale el compilador TypeScript y el marco Express.js. También necesitaremos algunos otros módulos:

```
npm install -g typescript
npm install express
npm install @types/express -D
```

A continuación, cree un nuevo proyecto utilizando la plantilla TypeScript Node Starter:

```
npx tsc --init
```

Esto creará un archivo `tsconfig.json` en su proyecto. Abra este archivo y agregue la siguiente configuración:

```json
{
    "compilerOptions": {
        "target": "es6",
        "module": "commonjs",
        "outDir": "dist",
        "strict": true
    }
}
```

Esta configuración compilará nuestro código TypeScript en ES6 JavaScript, que es compatible con Express.js. El código compilado se enviará al directorio `dist`.

## Instalación de Passport.js

Ahora que tenemos un proyecto configurado, podemos instalar Passport.js. Ejecute el siguiente comando:

```
npm install passport
```

Esto instalará el módulo Passport.js y lo agregará al archivo `package.json`.

## Configuración de Passport.js

Passport.js utiliza un enfoque modular, con diferentes "estrategias" para autenticar a los usuarios. Hay estrategias para autenticarse con un nombre de usuario y contraseña, con Facebook, con Twitter y más. En este artículo, nos centraremos en la estrategia de autenticación de nombre de usuario y contraseña.

Para usar una estrategia Passport.js, necesitamos instalar el módulo correspondiente. Para la estrategia de nombre de usuario y contraseña, usaremos el módulo [passport-local](https://github.com/jaredhanson/passport-local). Ejecute el siguiente comando para instalarlo:

```
npm install passport-local
```

Una vez que el módulo está instalado, debemos configurar Passport.js para usarlo. Haremos esto en el archivo `app.ts`. Primero, necesitamos importar el módulo `passport-local`:

```javascript
import passportLocal from "passport-local";
```

A continuación, debemos configurar Passport.js para usar la estrategia `passport-local`. Haremos esto en la función `configurePassport`:

```javascript
function configurePassport(passport: passport.Passport) {
    passport.use(new passportLocal.Strategy());
}
```

Esto configura Passport.js para usar la estrategia `passport-local`. La estrategia `passport-local` autentica a los usuarios mediante un nombre de usuario y una contraseña.

## Implementando la Autenticación

Ahora que tenemos Passport.js configurado, podemos comenzar a implementar la autenticación. Haremos esto en el archivo `app.ts`.

Primero, necesitamos importar el módulo `passport-local`:

```javascript
import passportLocal from "passport-local";
```

A continuación, debemos configurar Passport.js para usar la estrategia `passport-local`. Haremos esto en la función `configurePassport`:

```javascript
function configurePassport(passport: passport.Passport) {
    passport.use(new passportLocal.Strategy());
}
```

Esto configura Passport.js para usar la estrategia `passport-local`. La estrategia `passport-local` autentica a los usuarios mediante un nombre de usuario y una contraseña.

Una vez que tenemos configurado Passport.js, podemos escribir el código para autenticar a un usuario. Haremos esto en la función `login`:

```javascript
async function login(req: express.Request, res: express.Response) {
    passport.authenticate("local", (err, user, info) => {
        if (err) {
            // Handle errors
        }

        if (!user) {
            // Redirect to login page
        }

        // Login successful, redirect to home page
    })(req, res);
}
```

Este código autentica a un usuario usando la estrategia `passport-local`. Si la autenticación es exitosa, el usuario será redirigido a la página de inicio. De lo contrario, serán redirigidos a la página de inicio de sesión.

## Recursos externos

- [Documentación de Passport.js] (http://passportjs.org/docs)
- [Documentación local de pasaporte] (https://github.com/jaredhanson/passport-local)
- [Documentación TypeScript](https://www.typescriptlang.org/docs/handbook/basic-types.html)