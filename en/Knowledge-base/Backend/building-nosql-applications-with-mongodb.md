---
title: Building NoSQL Applications with MongoDB
description: 
published: true
date: 2023-02-01T22:06:06.743Z
tags: 
editor: markdown
dateCreated: 2023-02-01T22:06:01.512Z
---

- [Creación de aplicaciones NoSQL con MongoDB***Spanish** document is available*](/es/Knowledge-base/Backend/building-nosql-applications-with-mongodb)
{.links-list}
- [使用 MongoDB 构建 NoSQL 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Backend/building-nosql-applications-with-mongodb)
{.links-list}
- [MongoDB로 NoSQL 애플리케이션 구축***Korean** document is available*](/ko/Knowledge-base/Backend/building-nosql-applications-with-mongodb)
{.links-list}


# Building NoSQL Applications with MongoDB

## Introduction

MongoDB is an open source document-oriented database system developed and supported by 10gen. It is part of the NoSQL family of database systems. NoSQL databases are increasingly being used for web applications as they can handle high traffic and data volumes.

MongoDB uses a JSON-like document format and has an index-based search feature. It also has a rich query language. These features make MongoDB an attractive option for developers looking to build NoSQL applications.

## Setting up MongoDB

In this section, we will cover the basics of setting up MongoDB. We will install MongoDB on a local machine and create a simple database.

### Installing MongoDB

MongoDB can be downloaded from the 10gen website (http://www.10gen.com/). There are versions available for Windows, OS X, and Linux. Once MongoDB has been downloaded, follow the instructions for your operating system to install it.

### Creating a Database

We will create a simple database to store information about books. This database will have two collections: one for books and one for authors.

First, we need to start the MongoDB server. For Windows, this can be done by running the `mongod` executable. For OS X and Linux, MongoDB can be started by running the `mongod` command from the terminal.

Once the MongoDB server is running, we can connect to it using the `mongo` client. This will give us a `mongod>` prompt where we can enter commands.

First, we need to create the `books` collection. We can do this using the `db.createCollection()` method:

    ```javascript
    db.createCollection("books")
    ```

We can then insert some data into the collection using the `db.books.insert()` method. We will insert a document for each book:

    ```javascript
    db.books.insert({
        "title": "Moby Dick",
        "author": "Herman Melville",
        "year": 1851
    })

    db.books.insert({
        "title": "The Catcher in the Rye",
        "author": "J.D. Salinger",
        "year": 1951
    })

    db.books.insert({
        "title": "To Kill a Mockingbird",
        "author": "Harper Lee",
        "year": 1960
    })
    ```

We can then create the `authors` collection and insert data into it using the same methods:

    ```javascript
    db.createCollection("authors")

    db.authors.insert({
        "name": "Herman Melville",
        "born": 1819,
        "died": 1891,
        "books": ["Moby Dick"]
    })

    db.authors.insert({
        "name": "J.D. Salinger",
        "born": 1919,
        "died": 2010,
        "books": ["The Catcher in the Rye"]
    })

    db.authors.insert({
        "name": "Harper Lee",
        "born": 1926,
        "died": 2016,
        "books": ["To Kill a Mockingbird"]
    })
    ```

We can then use the `db.collection.find()` method to query the data in the collections. For example, to find all books written by J.D. Salinger, we would use the following query:

    ```javascript
    db.books.find({"author": "J.D. Salinger"})
    ```

## Building a NoSQL Application

In this section, we will build a simple web application that displays information about books. We will use the MongoDB database we created in the previous section.

We will build the application using the Node.js platform. Node.js is a popular platform for building web applications. It is lightweight and has a large ecosystem of modules that can be used to add functionality to applications.

We will use the Express.js web application framework. Express.js is a popular choice for building web applications with Node.js. It is easy to use and has a large number of features.

We will use the Jade template engine to generate the HTML for our web pages. Jade is a popular template engine that is easy to use and generates clean HTML.

We will use the Mongoose.js module to interface with our MongoDB database. Mongoose.js is a popular module that makes it easy to work with MongoDB from Node.js.

### Installing the dependencies

First, we need to install the modules we will be using. We can do this using the `npm` package manager, which is included with Node.js. We will install the modules globally so that we can use them from the command line.

From the command line, we can install the modules we need using the following commands:

    npm install -g express
    npm install -g jade
    npm install -g mongoose

### Creating the application

We will now create the files for our application. First, we will create a file named `app.js` in the root directory of our application. This file will contain the code for our web application.

We will start by requiring the modules we installed and setting up the basic structure of our application:

    ```javascript
    var express = require("express");
    var jade = require("jade");
    var mongoose = require("mongoose");

    var app = express();

    app.set("view engine", "jade");
    app.set("views", __dirname + "/views");

    app.use(express.static(__dirname + "/public"));
    ```

We will then define our routes. We will create two routes: one for the home page and one for the book details page.

For the home page route, we will query the `books` collection and render a template that displays the results:

    ```javascript
    app.get("/", function(req, res) {
        db.books.find(function(err, books) {
            if (err) {
                // handle error
            } else {
                res.render("index", { books: books });
            }
        });
    });
    ```

For the book details page, we will query the `books` and `authors` collections and render a template that displays the results:

    ```javascript
    app.get("/book/:id", function(req, res) {
        db.books.findById(req.params.id, function(err, book) {
            if (err) {
                // handle error
            } else {
                db.authors.findById(book.author, function(err, author) {
                    if (err) {
                        // handle error
                    } else {
                        res.render("book", { book: book, author: author });
                    }
                });
            }
        });
    });
    ```

We will then define our templates. We will create two templates: one for the home page and one for the book details page.

For the home page template, we will iterate over the `books` array and display information about each book:

    ```jade
    extends layout

    block content
        h1= title

        ul
            each book in books
                li
                    a(href="/book/#{book._id}")= book.title
    ```

For the book details page template, we will display information about the book and the author:

    ```jade
    extends layout

    block content
        h1= book.title

        p
            | Written by
            a(href="/author/#{author._id}")= author.name

        p= book.year
    ```

We will then create a file named `layout.jade` in the `views` directory. This file will contain the layout template for our application:

    ```jade
    doctype html
    html
        head
            title= title
            link(rel='stylesheet', href='/stylesheets/style.css')
        body
            block content
    ```

We will then create a file named `style.css` in the `public/stylesheets` directory. This file will contain the CSS for our application:

    ```css
    body {
        font-family: sans-serif;
    }

    h1 {
        font-weight: normal;
    }
    ```

We will then create a file named `package.json` in the root directory of our application. This file will contain the dependencies for our application:

    ```javascript
    {
        "name": "book-app",
        "version": "0.0.1",
        "dependencies": {
            "express": "3.x",
            "jade": "1.x",
            "mongoose": "3.x"
        }
    }
    ```

We will then create a file named `Procfile` in the root directory of our application. This file will tell Heroku how to start our application:

    ```
    web: node app.js
    ```

### Connecting to the database

We will now modify our `app.js` file to connect to our MongoDB database. We will use the `mongoose.connect()` method to connect to the database. We will store the connection in a variable named `db` so that we can use it in our routes:

    ```javascript
    var db = mongoose.connect("mongodb://localhost/book-app");
    ```

We will then define our models. We will create two models: one for books and one for authors.

For the book model, we will define the fields that we want to store in the database:

    ```javascript
    var bookSchema = mongoose.Schema({
        title: String,
        author: mongoose.Schema.Types.ObjectId,
        year: Number
    });

    var Book = mongoose.model("Book", bookSchema);
    ```

For the author model, we will define the fields that we want to store in the database:

    ```javascript
    var authorSchema = mongoose.Schema({
        name: String,
        born: Number,
        died: Number,
        books: [mongoose.Schema.Types.ObjectId]
    });

    var Author = mongoose.model("Author", authorSchema);
    ```

We will then modify our routes to use our models.

For the home page route, we will query the `books` collection and render a template that displays the results:

    ```javascript
    app.get("/", function(req, res) {
        Book.find(function(err, books) {
            if (err) {
                // handle error
            } else {
                res.render("index", { books: books });
            }
        });
    });
    ```

For the book details page, we will query the `books` and `authors` collections and render a template that displays the results:

    ```javascript
    app.get("/book/:id", function(req, res) {
        Book.findById(req.params.id, function(err, book) {
            if (err) {
                // handle error
            } else {
                Author.findById(book.author, function(err, author) {
                    if (err) {
                        // handle error
                    } else {
                        res.render("book", { book: book, author: author });
                    }
                });
            }
        });
    });
    ```

## Deploying the Application

In this section, we will deploy our application to Heroku. Heroku is a popular platform as a service (PaaS) that makes it easy to deploy and scale web applications.

We will first need to create a Heroku account (https://signup.heroku.com/). Once your account has been created, you will need to install the Heroku Toolbelt (https://toolbelt.heroku.com/). The Heroku Toolbelt is a command line interface (CLI) that can be used to manage Heroku applications.

Once the Heroku Toolbelt has been installed, you can log in to your account using the `heroku login` command. You will be prompted for your email address and password.

We can then create our Heroku application using the `heroku create` command. This will create a new application and give it a unique name. We can optionally specify a name for our application using the `--app` flag:

    heroku create --app my-app-name

We can then deploy our application to Heroku using the `git push heroku master` command. This will push our code from the `master` branch of our Git repository to the `heroku` remote:

    git push heroku master

We can then open our application in a web browser using the `heroku open` command. This will open the home page of our application in a new tab:

    heroku open

## Conclusion

In this article, we have covered the basics of building NoSQL applications with MongoDB. We have covered how to install MongoDB, how to create a database, how to build a NoSQL application, and how to deploy the application to Heroku.

NoSQL databases are becoming increasingly popular for web applications. MongoDB is a popular choice for NoSQL applications due to its document-oriented data model, index-based search feature, and rich query language.

Node.js is a popular platform for building web applications. It is lightweight and has a large ecosystem of modules. Express.js is a popular web application framework for Node.js. Jade is a popular template engine that is easy to use and generates clean HTML. Mongoose.js is a popular module that makes it easy to work with MongoDB from Node.js.

Heroku is a popular platform as a service (PaaS) that makes it easy to deploy and scale web applications.