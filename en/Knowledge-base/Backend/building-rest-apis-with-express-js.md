---
title: Building REST APIs with Express.js
description: 
published: true
date: 2023-02-06T13:55:55.766Z
tags: 
editor: markdown
dateCreated: 2023-02-06T13:55:50.127Z
---

- [Creación de API REST con Express.js***Spanish** document is available*](/es/Knowledge-base/Backend/building-rest-apis-with-express-js)
{.links-list}
- [使用 Express.js 构建 REST API***Chinese Simplified** document is available*](/zh/Knowledge-base/Backend/building-rest-apis-with-express-js)
{.links-list}
- [Express.js로 REST API 구축***Korean** document is available*](/ko/Knowledge-base/Backend/building-rest-apis-with-express-js)
{.links-list}


# Building REST APIs with Express.js

If you're looking to build a REST API with Node.js, you'll likely want to use the popular Express.js framework. In this article, we'll show you how to build a basic REST API with Express.js.

## What is a REST API?

Before we get started, let's first briefly go over what a REST API is. REST (Representational State Transfer) is an architectural style for building web services. A REST API defines a set of operations that can be performed on resources, which are typically identified by URLs.

For example, if you have a blog, you might have a `/posts` resource that represents all of the blog posts, and each post would have its own URL. To create a new post, you would `POST` to the `/posts` resource. To view a specific post, you would `GET` the post's URL. To update a post, you would `PUT` to the post's URL, and to delete a post, you would `DELETE` the post's URL.

These are just a few of the most common operations, but there are many more that can be performed on resources.

## Setting up Express.js

Now that we know what a REST API is, let's get started setting up Express.js. The first thing you'll need to do is install the Express.js framework. You can do this using the Node Package Manager (NPM).

```
npm install express
```

Once Express.js is installed, you can create a new `app.js` file and require the Express.js module.

```javascript
const express = require('express');
const app = express();
```

Next, we'll need to set up a few routes. Routes are defined by the HTTP method and the URL pattern. For our example, we'll create a route for `GET`ting all posts and a route for `POST`ing a new post.

```javascript
app.get('/posts', (req, res) => {
  // Get all posts
});

app.post('/posts', (req, res) => {
  // Create a new post
});
```

We can also define routes for `PUT`ting and `DELETE`ing posts by their id.

```javascript
app.put('/posts/:id', (req, res) => {
  // Update a post
});

app.delete('/posts/:id', (req, res) => {
  // Delete a post
});
```

In the `PUT` and `DELETE` routes, we're using a URL parameter, `:id`, which represents the id of the post we want to update or delete. We can access this id in the route handler function using the `req.params` object.

```javascript
app.put('/posts/:id', (req, res) => {
  const id = req.params.id;
  // Update a post
});

app.delete('/posts/:id', (req, res) => {
  const id = req.params.id;
  // Delete a post
});
```

Now that we have our routes defined, we need to start the Express.js server. We can do this by calling the `app.listen` method and passing in the port number. We'll also add a `console.log` statement so we know when the server is running.

```javascript
app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

## Testing the API

Now that our server is up and running, let's test out our API. We can use a tool like Postman to make HTTP requests to our API.

First, let's `GET` all posts. We should see an empty array as a response, since we haven't added any posts yet.

![get all posts](https://i.imgur.com/VmYbU7D.png)

Next, let's `POST` a new post. We'll need to set the `Content-Type` header to `application/json` and pass in a JSON body with the `title` and `body` of the post.

![post a new post](https://i.imgur.com/WBY4KdI.png)

If we `GET` all posts again, we should see our new post in the response.

![get all posts with new post](https://i.imgur.com/YB7qAFs.png)

Finally, let's `PUT` an update to our post and `DELETE` it. We'll need to set the `Content-Type` header to `application/json` again and pass in the `id` of the post in the URL. For the update, we'll just change the `title` of the post.

![put update to post](https://i.imgur.com/YB7qAFs.png)

If we `GET` the post again, we should see the updated `title`.

![get post with updated title](https://i.imgur.com/VmYbU7D.png)

Now, let's `DELETE` the post.

![delete post](https://i.imgur.com/VmYbU7D.png)

If we `GET` all posts again, we should see that the post has been deleted.

![get all posts with post deleted](https://i.imgur.com/VmYbU7D.png)

And that's it! You've now successfully built a basic REST API with Express.js.

## External Resources

- [REST API Tutorial](https://www.restapitutorial.com/)
- [Express.js](https://expressjs.com/)
- [Node.js](https://nodejs.org/)