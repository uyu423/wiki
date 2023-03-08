---
title: Creación de aplicaciones NoSQL con MongoDB
description: 
published: true
date: 2023-02-01T22:06:04.219Z
tags: 
editor: markdown
dateCreated: 2023-02-01T22:06:01.510Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Building NoSQL Applications with MongoDB***English** document is available*](/en/Knowledge-base/Backend/building-nosql-applications-with-mongodb)
{.links-list}


# Creación de aplicaciones NoSQL con MongoDB

## Introducción

MongoDB es un sistema de base de datos orientado a documentos de código abierto desarrollado y respaldado por 10gen. Es parte de la familia NoSQL de sistemas de bases de datos. Las bases de datos NoSQL se utilizan cada vez más para aplicaciones web, ya que pueden manejar un alto tráfico y volúmenes de datos.

MongoDB utiliza un formato de documento similar a JSON y tiene una función de búsqueda basada en índices. También tiene un rico lenguaje de consulta. Estas características hacen de MongoDB una opción atractiva para los desarrolladores que buscan crear aplicaciones NoSQL.

## Configurando MongoDB

En esta sección, cubriremos los aspectos básicos de la configuración de MongoDB. Instalaremos MongoDB en una máquina local y crearemos una base de datos simple.

### Instalación de MongoDB

MongoDB se puede descargar desde el sitio web de 10gen (http://www.10gen.com/). Hay versiones disponibles para Windows, OS X y Linux. Una vez descargado MongoDB, siga las instrucciones de su sistema operativo para instalarlo.

### Creación de una base de datos

Crearemos una base de datos simple para almacenar información sobre libros. Esta base de datos tendrá dos colecciones: una de libros y otra de autores.

Primero, necesitamos iniciar el servidor MongoDB. Para Windows, esto se puede hacer ejecutando el ejecutable `mongod`. Para OS X y Linux, MongoDB se puede iniciar ejecutando el comando `mongod` desde la terminal.

Una vez que el servidor MongoDB se está ejecutando, podemos conectarnos a él usando el cliente `mongo`. Esto nos dará un indicador `mongod>` donde podemos ingresar comandos.

Primero, necesitamos crear la colección `books`. Podemos hacer esto usando el método `db.createCollection()`:

    ```javascript
    db.createCollection("libros")
    ```

Luego podemos insertar algunos datos en la colección usando el método `db.books.insert()`. Insertaremos un documento por cada libro:

    ```javascript
    db.libros.insertar({
        "título": "Moby Dick",
        "autor": "Herman Melville",
        "año": 1851
    })

    db.libros.insertar({
        "title": "El guardián entre el centeno",
        "autor": "J.D. Salinger",
        "año": 1951
    })

    db.libros.insertar({
        "title": "Matar a un ruiseñor",
        "autor": "Harper Lee",
        "año": 1960
    })
    ```

Luego podemos crear la colección `autores` e insertar datos en ella usando los mismos métodos:

    ```javascript
    db.createCollection("autores")

    db.autores.insertar({
        "nombre": "Herman Melville",
        "nacido": 1819,
        "murió": 1891,
        "libros": ["Moby Dick"]
    })

    db.autores.insertar({
        "nombre": "J.D. Salinger",
        "nacido": 1919,
        "murió": 2010,
        "libros": ["El guardián entre el centeno"]
    })

    db.autores.insertar({
        "nombre": "Harper Lee",
        "nacido": 1926,
        "murió": 2016,
        "books": ["Matar a un ruiseñor"]
    })
    ```

Entonces podemos usar el método `db.collection.find()` para consultar los datos en las colecciones. Por ejemplo, para encontrar todos los libros escritos por J.D. Salinger, usaríamos la siguiente consulta:

    ```javascript
    db.books.find({"autor": "J.D. Salinger"})
    ```

## Creación de una aplicación NoSQL

En esta sección, construiremos una aplicación web simple que muestra información sobre libros. Usaremos la base de datos MongoDB que creamos en la sección anterior.

Construiremos la aplicación utilizando la plataforma Node.js. Node.js es una plataforma popular para crear aplicaciones web. Es liviano y tiene un gran ecosistema de módulos que se pueden usar para agregar funcionalidad a las aplicaciones.

Usaremos el marco de aplicación web Express.js. Express.js es una opción popular para crear aplicaciones web con Node.js. Es fácil de usar y tiene una gran cantidad de características.

Usaremos el motor de plantillas de Jade para generar el HTML de nuestras páginas web. Jade es un motor de plantillas popular que es fácil de usar y genera HTML limpio.

Usaremos el módulo Mongoose.js para interactuar con nuestra base de datos MongoDB. Mongoose.js es un módulo popular que facilita el trabajo con MongoDB desde Node.js.

### Instalando las dependencias

Primero, necesitamos instalar los módulos que usaremos. Podemos hacer esto usando el administrador de paquetes `npm`, que se incluye con Node.js. Instalaremos los módulos de forma global para poder usarlos desde la línea de comandos.

Desde la línea de comandos, podemos instalar los módulos que necesitemos usando los siguientes comandos:

    npm instalar -g express
    npm install -g jade
    npm install -g mangosta

### Creando la aplicación

Ahora crearemos los archivos para nuestra aplicación. Primero, crearemos un archivo llamado `app.js` en el directorio raíz de nuestra aplicación. Este archivo contendrá el código de nuestra aplicación web.

Comenzaremos requiriendo los módulos que instalamos y configurando la estructura básica de nuestra aplicación:

    ```javascript
    var express = require("expreso");
    var jade = require("jade");
    var mangosta = require("mangosta");

    var aplicación = express();

    app.set("ver motor", "jade");
    app.set("vistas", __dirname + "/vistas");

    app.use(express.static(__dirname + "/public"));
    ```

A continuación, definiremos nuestras rutas. Crearemos dos rutas: una para la página de inicio y otra para la página de detalles del libro.

Para la ruta de la página de inicio, consultaremos la colección `books` y generaremos una plantilla que muestre los resultados:

    ```javascript
    app.get("/", function(req, res) {
        db.books.find(function(err, libros) {
            si (err) {
                // manejar el error
            } más {
                res.render("index", { libros: libros });
            }
        });
    });
    ```

Para la página de detalles del libro, consultaremos las colecciones `books` y `authors` y generaremos una plantilla que muestre los resultados:

    ```javascript
    app.get("/libro/:id", function(req, res) {
        db.books.findById(req.params.id, function(err, libro) {
            si (err) {
                // manejar el error
            } más {
                db.authors.findById(libro.autor, función(err, autor) {
                    si (err) {
                        // manejar el error
                    } más {
                        res.render("libro", { libro: libro, autor: autor });
                    }
                });
            }
        });
    });
    ```

A continuación, definiremos nuestras plantillas. Crearemos dos plantillas: una para la página de inicio y otra para la página de detalles del libro.

Para la plantilla de la página de inicio, iteraremos sobre la matriz `books` y mostraremos información sobre cada libro:

    ```jade
    extiende el diseño

    bloquear contenido
        h1= título

        ul
            cada libro en libros
                li
                    a(href="/libro/# {libro._id}")= libro.título
    ```

Para la plantilla de página de detalles del libro, mostraremos información sobre el libro y el autor:

    ```jade
    extiende el diseño

    bloquear contenido
        h1= libro.título

        pag
            | Escrito por
            a(href="/autor/# {autor._id}")= autor.nombre

        p= libro.año
    ```

Luego crearemos un archivo llamado `layout.jade` en el directorio `views`. Este archivo contendrá la plantilla de diseño para nuestra aplicación:

    ```jade
    tipo de documento html
    html
        cabeza
            título = título
            enlace(rel='hoja de estilo', href='/hojas de estilo/estilo.css')
        cuerpo
            bloquear contenido
    ```

Luego crearemos un archivo llamado `style.css` en el directorio `public/stylesheets`. Este archivo contendrá el CSS para nuestra aplicación:

    ```css
    cuerpo {
        familia tipográfica: sans-serif;
    }

    h1 {
        peso de fuente: normal;
    }
    ```

Luego crearemos un archivo llamado `package.json` en el directorio raíz de nuestra aplicación. Este archivo contendrá las dependencias para nuestra aplicación:

    ```javascript
    {
        "nombre": "aplicación de libro",
        "versión": "0.0.1",
        "dependencias": {
            "expreso": "3.x",
            "jade": "1.x",
            "mangosta": "3.x"
        }
    }
    ```

Luego crearemos un archivo llamado `Procfile` en el directorio raíz de nuestra aplicación. Este archivo le dirá a Heroku cómo iniciar nuestra aplicación:

    ```
    web: aplicación de nodo.js
    ```

### Conexión a la base de datos

Ahora modificaremos nuestro archivo `app.js` para conectarnos a nuestra base de datos MongoDB. Usaremos el método `mongoose.connect()` para conectarnos a la base de datos. Guardaremos la conexión en una variable llamada `db` para que podamos usarla en nuestras rutas:

    ```javascript
    var db = mongoose.connect("mongodb://localhost/book-app");
    ```

A continuación, definiremos nuestros modelos. Crearemos dos modelos: uno para libros y otro para autores.

Para el modelo de libro, definiremos los campos que queremos almacenar en la base de datos:

    ```javascript
    var bookSchema = mangosta.Schema({
        título: Cadena,
        autor: mangosta.Schema.Types.ObjectId,
        año: Número
    });

    var Libro = mongoose.model("Libro", bookSchema);
    ```

Para el modelo autor, definiremos los campos que queremos almacenar en la base de datos:

    ```javascript
    var autorEsquema = mangosta.Esquema({
        nombre: cadena,
        nacido: Número,
        murió: Número,
        libros: [mongoose.Schema.Types.ObjectId]
    });

    var Autor = mongoose.model("Autor", authorSchema);
    ```

Luego modificaremos nuestras rutas para usar nuestros modelos.

Para la ruta de la página de inicio, consultaremos la colección `books` y generaremos una plantilla que muestre los resultados:

    ```javascript
    app.get("/", function(req, res) {
        Book.find(function(err, libros) {
            si (err) {
                // manejar el error
            } más {
                res.render("index", { libros: libros });
            }
        });
    });
    ```

Para la página de detalles del libro, consultaremos las colecciones `books` y `authors` y generaremos una plantilla que muestre los resultados:

    ```javascript
    app.get("/libro/:id", function(req, res) {
        Libro.findById(req.params.id, function(err, libro) {
            si (err) {
                // manejar el error
            } más {
                Autor.findById(libro.autor, función(err, autor) {
                    si (err) {
                        // manejar el error
                    } más {
                        res.render("libro", { libro: libro, autor: autor });
                    }
                });
            }
        });
    });
    ```

## Implementación de la aplicación

En esta sección, implementaremos nuestra aplicación en Heroku. Heroku es una popular plataforma como servicio (PaaS) que facilita la implementación y el escalado de aplicaciones web.

Primero necesitaremos crear una cuenta de Heroku (https://signup.heroku.com/). Una vez que haya creado su cuenta, deberá instalar Heroku Toolbelt (https://toolbelt.heroku.com/). Heroku Toolbelt es una interfaz de línea de comandos (CLI) que se puede usar para administrar las aplicaciones de Heroku.

Una vez que se haya instalado Heroku Toolbelt, puede iniciar sesión en su cuenta con el comando `heroku login`. Se le pedirá su dirección de correo electrónico y contraseña.

Luego podemos crear nuestra aplicación Heroku usando el comando `heroku create`. Esto creará una nueva aplicación y le dará un nombre único. Opcionalmente, podemos especificar un nombre para nuestra aplicación usando el indicador `--app`:

    heroku create --app mi-nombre-de-aplicación

Luego podemos implementar nuestra aplicación en Heroku usando el comando `git push heroku master`. Esto empujará nuestro código desde la rama `maestra` de nuestro repositorio Git al control remoto `heroku`:

    git empuje maestro heroku

Luego podemos abrir nuestra aplicación en un navegador web usando el comando `heroku open`. Esto abrirá la página de inicio de nuestra aplicación en una nueva pestaña:

    heroku abierto

## Conclusión

En este artículo, hemos cubierto los conceptos básicos de la creación de aplicaciones NoSQL con MongoDB. Hemos cubierto cómo instalar MongoDB, cómo crear una base de datos, cómo construir una aplicación NoSQL y cómo implementar la aplicación en Heroku.

Las bases de datos NoSQL son cada vez más populares para las aplicaciones web. MongoDB es una opción popular para aplicaciones NoSQL debido a su modelo de datos orientado a documentos, función de búsqueda basada en índices y lenguaje de consulta enriquecido.

Node.js es una plataforma popular para crear aplicaciones web. Es ligero y tiene un gran ecosistema de módulos. Express.js es un marco de aplicación web popular para Node.js. Jade es un motor de plantillas popular que es fácil de usar y genera HTML limpio. Mongoose.js es un módulo popular que facilita el trabajo con MongoDB desde Node.js.

Heroku es una popular plataforma como servicio (PaaS) que facilita la implementación y el escalado de aplicaciones web.