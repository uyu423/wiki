---
title: A Guide to MongoDB Realm: A Serverless Platform for Building Modern Applications
description: 
published: true
date: 2023-03-07T21:33:03.915Z
tags: 
editor: markdown
dateCreated: 2023-03-07T21:33:02.419Z
---

- [MongoDB Realm 가이드: 최신 애플리케이션 구축을 위한 서버리스 플랫폼***Korean** document is available*](/ko/Knowledge-base/NoSQL/a-guide-to-mongodb-realm-a-serverless-platform-for-building-modern-applications)
{.links-list}

MongoDB Realm: A Serverless Platform for Building Modern Applications

MongoDB is a popular NoSQL database that has revolutionized the software industry since its launch in 2009. It has gained immense popularity due to its scalability, flexibility, powerful querying language, and high performance. Developers have been using MongoDB to build a wide range of applications, from simple blogging platforms to complex e-commerce systems. However, managing a MongoDB cluster and setting up a back-end for your application can be time-consuming and complicated. That's where MongoDB Realm comes in. MongoDB Realm is a powerful, serverless platform that allows you to build modern applications with ease. In this article, we'll take a closer look at MongoDB Realm and how it can simplify your development process.

What is MongoDB Realm?

MongoDB Realm is an innovative serverless platform that makes it easy to build modern applications. It is designed to simplify the development process by removing the need for back-end infrastructure and allowing you to focus on building your application. MongoDB Realm is built on top of MongoDB and provides a wide range of features such as data synchronization, real-time event handling, and user authentication.

One of the key features of MongoDB Realm is its serverless architecture. With serverless computing, you don't have to worry about managing servers, installing software, or scaling up and down. MongoDB Realm takes care of all of this for you, allowing you to focus on writing code and building your application.

Another important feature of MongoDB Realm is its data synchronization capabilities. MongoDB Realm allows you to synchronize data between devices and the cloud in real-time, making it easy to build applications that work offline and online. This feature is particularly useful for mobile applications, where network connectivity can be unreliable.

How does MongoDB Realm work?

MongoDB Realm is built on top of MongoDB, which means that it uses MongoDB's query language (MongoDB Query Language or MQL) to interact with data. MongoDB Realm provides a serverless platform for building your application, which means that you don't have to worry about managing servers or scaling infrastructure. MongoDB Realm provides a set of APIs that you can use to interact with data, handle events, and authenticate users.

One of the key components of MongoDB Realm is its data access layer. MongoDB Realm provides a powerful data access layer that allows you to interact with data stored in MongoDB. The data access layer provides a set of APIs that you can use to perform CRUD (Create, Read, Update, Delete) operations on data, and also supports complex queries using MQL.

Another important component of MongoDB Realm is its event handling capabilities. MongoDB Realm allows you to handle real-time events, such as data changes, user authentication, and user registration. You can use MongoDB Realm to trigger serverless functions in response to events, making it easy to build reactive applications.

MongoDB Realm also provides user authentication and authorization capabilities. MongoDB Realm allows you to authenticate users using a wide range of authentication providers, including email/password, Google, Facebook, and Apple. MongoDB Realm also supports role-based access control, allowing you to control access to your application's resources based on user roles.

How to use MongoDB Realm?

Using MongoDB Realm is easy. All you need to do is create a MongoDB Realm account and follow a few simple steps to set up your application. MongoDB Realm provides a wide range of integration options that you can use to connect your application to MongoDB Realm, including SDKs for iOS, Android, and web applications.

To get started with MongoDB Realm, follow these steps:

1. Create a MongoDB Realm account: To get started with MongoDB Realm, you'll need to create a MongoDB Realm account. You can create an account by visiting the MongoDB Realm website and signing up for a free account.

2. Create a new application: Once you've created your MongoDB Realm account, you can create a new application by navigating to the MongoDB Realm dashboard and clicking the "New Application" button. You'll need to provide a name for your application and choose a region.

3. Set up data synchronization: If you're building a mobile application, you'll need to set up data synchronization between devices and the cloud. MongoDB Realm provides a wide range of synchronization options that you can use to sync data, including automatic conflict resolution.

4. Set up user authentication: MongoDB Realm provides a wide range of authentication providers that you can use to authenticate users, including email/password, Google, Facebook, and Apple. You'll need to set up user authentication to control access to your application's resources.

5. Build your application: Once you've set up your MongoDB Realm application, you can start building your application. MongoDB Realm provides a wide range of APIs that you can use to interact with data, handle events, and authenticate users.

Example: Building a simple chat application with MongoDB Realm

Let's take a look at how you can use MongoDB Realm to build a simple chat application. For this example, we'll be using the MongoDB Realm web SDK and the React framework.

First, we'll create a new MongoDB Realm application and set up data synchronization. We'll use MongoDB Atlas as our database.

Next, we'll create a new collection in MongoDB Atlas to store our chat messages. We'll use the following schema:

```javascript
{
  "_id": ObjectId(),
  "message": String,
  "sender": String,
  "timestamp": Date
}
```

Next, we'll create a serverless function in MongoDB Realm to handle new chat messages. We'll use the following code:

```javascript
exports = async function (payload) {
  const { message, sender } = payload;
  const chatCollection = context.services.get("mongodb-atlas").db("chat").collection("messages");

  const result = await chatCollection.insertOne({
    message,
    sender,
    timestamp: new Date()
  });

  return result.insertedId;
};
```

This function will insert a new chat message into the MongoDB Atlas database whenever a new message is sent.

Next, we'll create a React component to display the chat messages. We'll use the following code:

```javascript
import React, { useState, useEffect } from "react";
import { Stitch, RemoteMongoClient } from "mongodb-stitch-browser-sdk";

const Chat = () => {
  const [messages, setMessages] = useState([]);

  useEffect(() => {
    const fetchMessages = async () => {
      const mongoClient = Stitch.defaultAppClient.getServiceClient(
        RemoteMongoClient.factory,
        "mongodb-atlas"
      );

      const chatCollection = mongoClient.db("chat").collection("messages");
      const cursor = chatCollection.find({}, { sort: { timestamp: -1 } });

      const newMessages = await cursor.toArray();
      setMessages(newMessages.reverse());
    };

    fetchMessages();
  }, []);

  const handleSubmit = async (event) => {
    event.preventDefault();

    const message = event.target.elements.message.value;
    const sender = "John Doe";

    const result = await Stitch.defaultAppClient.callFunction("newMessage", {
      message,
      sender
    });

    event.target.elements.message.value = "";
  };

  return (
    <div>
      <ul>
        {messages.map((message) => (
          <li key={message._id.toString()}>
            {message.sender}: {message.message}
          </li>
        ))}
      </ul>
      <form onSubmit={handleSubmit}>
        <input type="text" name="message" />
        <button>Send</button>
      </form>
    </div>
  );
};

export default Chat;
```

This component will display the chat messages and allow the user to send new messages. The component uses the MongoDB Stitch SDK to fetch the chat messages and send new messages.

Conclusion

In this article, we've explored MongoDB Realm, a powerful serverless platform for building modern applications. MongoDB Realm provides a wide range of features, including data synchronization, real-time event handling, and user authentication. MongoDB Realm makes it easy to build reactive applications that work offline and online, and provides a simple and intuitive API for interacting with data. If you're looking for a powerful and easy-to-use platform for building modern applications, MongoDB Realm is definitely worth checking out.

External resources:

- MongoDB Realm documentation: https://docs.mongodb.com/realm/
- MongoDB Atlas documentation: https://docs.atlas.mongodb.com/
- MongoDB Stitch SDK documentation: https://docs.mongodb.com/stitch/
- React documentation: https://reactjs.org/
- MongoDB Realm and React tutorial: https://www.mongodb.com/developer/how-to/build-a-chat-app-with-realm-and-react/