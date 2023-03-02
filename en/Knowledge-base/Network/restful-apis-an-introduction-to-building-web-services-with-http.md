---
title: RESTful APIs: An Introduction to Building Web Services with HTTP
description: 
published: true
date: 2023-03-02T15:32:16.123Z
tags: 
editor: markdown
dateCreated: 2023-03-02T15:32:16.123Z
---

- [RESTful API: HTTP로 웹 서비스 구축 소개***Korean** document is available*](/ko/Knowledge-base/Network/restful-apis-an-introduction-to-building-web-services-with-http)
{.links-list}
RESTful APIs: An Introduction to Building Web Services with HTTP

RESTful APIs are becoming increasingly popular among developers for developing web services. REST stands for Representational State Transfer, which is a standard for creating web services that are lightweight, scalable, and maintainable. The use of HTTP makes RESTful APIs a popular choice among developers, as it is widely used and understood. This article will provide an introduction to building RESTful APIs using HTTP.

## What is a RESTful API?

A RESTful API is an architectural style for building web services based on HTTP. It focuses on the resources exposed by the web service rather than the operations that can be performed on those resources. The resources are represented in a stateless manner, which means that each request from the client to the server contains all the information necessary to perform the request. This allows for scalability and simplifies the implementation of the API.

RESTful APIs are based on four basic principles:

1. **Client-Server Architecture:** The client and server are separate, allowing them to evolve independently.

2. **Stateless:** The client and server do not maintain any information about each other. Each request is self-contained.

3. **Cacheable:** Responses must be marked as cacheable or non-cacheable. This allows for more efficient use of resources.

4. **Uniform Interface:** The API must have a uniform interface, which means that resources should be identified using URIs, and standard HTTP methods should be used for operations on those resources.

## HTTP Methods

The HTTP protocol supports several methods, but RESTful APIs use a subset of them. The most commonly used methods are:

1. **GET:** Retrieves a resource from the server.

2. **POST:** Creates a new resource on the server.

3. **PUT:** Updates an existing resource on the server.

4. **DELETE:** Deletes a resource from the server.

5. **PATCH:** Partially updates an existing resource on the server.

## HTTP Status Codes

HTTP status codes indicate the success or failure of a request. The most commonly used status codes in RESTful APIs are:

1. **200 OK:** The request was successful.

2. **201 Created:** The resource was created successfully.

3. **204 No Content:** The request was successful, but there is no response body.

4. **400 Bad Request:** The request was malformed or invalid.

5. **401 Unauthorized:** The client is not authorized to perform the request.

6. **404 Not Found:** The requested resource was not found on the server.

7. **500 Internal Server Error:** The server encountered an error while processing the request.

## Building a Simple RESTful API

To illustrate how to build a RESTful API with HTTP, let's create a simple API for managing books. The API will have two endpoints: one for retrieving a list of books and another for retrieving a single book.

### Step 1: Create the Data Model

We'll start by creating a simple data model for the books. Create a file called `book.py` and add the following code:

```python
class Book:
    def __init__(self, id, title, author):
        self.id = id
        self.title = title
        self.author = author
```

This creates a basic `Book` class with three attributes: `id`, `title`, and `author`.

### Step 2: Create the API Endpoints

Next, we'll create two endpoints for our API: one for retrieving a list of books and another for retrieving a single book.

Create a file called `api.py` and add the following code:

```python
from flask import Flask, jsonify
from book import Book

app = Flask(__name__)

books = [
    Book(1, 'The Hitchhiker\'s Guide to the Galaxy', 'Douglas Adams'),
    Book(2, '1984', 'George Orwell'),
    Book(3, 'The Catcher in the Rye', 'J.D. Salinger')
]

@app.route('/books', methods=['GET'])
def get_books():
    return jsonify({'books': [book.__dict__ for book in books]})

@app.route('/books/<int:book_id>', methods=['GET'])
def get_book(book_id):
    book = next((book for book in books if book.id == book_id), None)
    if book:
        return jsonify(book.__dict__)
    else:
        return jsonify({'error': 'Book not found'}), 404

if __name__ == '__main__':
    app.run()
```

This code sets up a Flask application and defines two endpoints: `/books` and `/books/<int:book_id>`. The first endpoint returns a list of all the books, and the second endpoint returns a single book by its ID.

### Step 3: Test the API

To test the API, run the `api.py` file and open a browser to `http://localhost:5000/books` to retrieve all the books or `http://localhost:5000/books/<book_id>` to retrieve a single book.

## Conclusion

RESTful APIs are a popular choice for building web services, and HTTP is the foundation for building these APIs. By following the principles of REST and using the HTTP protocol, developers can create lightweight, scalable, and maintainable web services. By creating a simple RESTful API for managing books, we've illustrated how to build an API using HTTP.

## Further Reading

1. [RESTful Web Services](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm) by Roy Fielding
2. [HTTP/1.1 Specification](https://tools.ietf.org/html/rfc7231)
3. [Flask Documentation](https://flask.palletsprojects.com/)