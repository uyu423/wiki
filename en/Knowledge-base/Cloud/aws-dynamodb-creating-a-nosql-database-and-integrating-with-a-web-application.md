---
title: AWS DynamoDB: Creating a NoSQL Database and Integrating with a Web Application
description: 
published: true
date: 2023-02-19T01:07:41.710Z
tags: 
editor: markdown
dateCreated: 2023-02-19T01:07:34.632Z
---

- [AWS DynamoDB: NoSQL 데이터베이스 생성 및 웹 애플리케이션과 통합***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-dynamodb-creating-a-nosql-database-and-integrating-with-a-web-application)
{.links-list}


# DynamoDB NoSQL Database

## Introduction 

DynamoDB is a fast, flexible, and scalable NoSQL database service provided by Amazon. It can be used as a key-value store or document database, and has many features that make it a great fit for a wide range of applications.

In this article, we'll look at how to create a DynamoDB table and integrate it with a web application. We'll also look at some of the key features of DynamoDB and how they can be used to build scalable and resilient applications.

## Creating a DynamoDB Table

Creating a DynamoDB table is a simple process. First, login to the AWS Management Console and select DynamoDB from the list of services.

![dynamodb-create-table-1](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-create-table-1.png)

On the next page, click the "Create table" button.

![dynamodb-create-table-2](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-create-table-2.png)

Enter a name for your table, choose a primary key, and select the "Provisioned" throughput mode. Then, click the "Create" button.

![dynamodb-create-table-3](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-create-table-3.png)

On the next page, you'll be able to configure the provisioned throughput for your table. DynamoDB will automatically scale the throughput up or down based on traffic, but you can also manually adjust the throughput if needed.

![dynamodb-create-table-4](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-create-table-4.png)

Once you've configured the provisioned throughput, click the "Create" button to create the table.

## Inserting Data into a DynamoDB Table

Now that our table has been created, let's insert some data into it. DynamoDB provides a simple API for working with data in a table. We can use the `putItem` method to insert a new item into the table.

```javascript
var AWS = require('aws-sdk');

AWS.config.update({
  region: "us-west-2",
  endpoint: "http://localhost:8000"
});

var docClient = new AWS.DynamoDB.DocumentClient();

var table = "Movies";

var year = 2015;
var title = "The Big New Movie";

var params = {
    TableName:table,
    Item:{
        "year": year,
        "title": title,
        "info":{
            "plot": "Nothing happens at all.",
            "rating": 0
        }
    }
};

console.log("Adding a new item...");
docClient.put(params, function(err, data) {
    if (err) {
        console.error("Unable to add item. Error JSON:", JSON.stringify(err, null, 2));
    } else {
        console.log("Added item:", JSON.stringify(data, null, 2));
    }
});
```

This code will insert a new item into the table with the primary key `year` and the sort key `title`. The `info` attribute contains a map of information about the movie.

## Retrieving Data from a DynamoDB Table

We can use the `getItem` method to retrieve an item from a DynamoDB table. The following code will retrieve the item we just inserted.

```javascript
var params = {
    TableName:table,
    Key:{
        "year": year,
        "title": title
    }
};

docClient.get(params, function(err, data) {
    if (err) {
        console.error("Unable to read item. Error JSON:", JSON.stringify(err, null, 2));
    } else {
        console.log("GetItem succeeded:", JSON.stringify(data, null, 2));
    }
});
```

## Updating Data in a DynamoDB Table

We can use the `updateItem` method to update an existing item in a DynamoDB table. The following code will add some additional information to the `info` map for the item we inserted earlier.

```javascript
var params = {
    TableName:table,
    Key:{
        "year": year,
        "title": title
    },
    UpdateExpression: "set info.rating = :r, info.plot=:p, info.actors=:a",
    ExpressionAttributeValues:{
        ":r":5.5,
        ":p":"Everything happens all at once.",
        ":a":["Larry", "Moe", "Curly"]
    },
    ReturnValues:"UPDATED_NEW"
};

console.log("Updating the item...");
docClient.update(params, function(err, data) {
    if (err) {
        console.error("Unable to update item. Error JSON:", JSON.stringify(err, null, 2));
    } else {
        console.log("UpdateItem succeeded:", JSON.stringify(data, null, 2));
    }
});
```

## Deleting Data from a DynamoDB Table

We can use the `deleteItem` method to delete an existing item from a DynamoDB table. The following code will delete the item we inserted earlier.

```javascript
var params = {
    TableName:table,
    Key:{
        "year": year,
        "title": title
    }
};

console.log("Attempting a conditional delete...");
docClient.delete(params, function(err, data) {
    if (err) {
        console.error("Unable to delete item. Error JSON:", JSON.stringify(err, null, 2));
    } else {
        console.log("DeleteItem succeeded:", JSON.stringify(data, null, 2));
    }
});
```

## DynamoDB Streams

DynamoDB Streams is a feature that allows you to track changes to items in a DynamoDB table in near-real-time. Streams can be used to build event-driven applications that respond to changes in data.

To enable DynamoDB Streams for a table, select the "Enable DynamoDB Streams" checkbox when creating the table.

![dynamodb-create-table-5](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-create-table-5.png)

Once DynamoDB Streams is enabled for a table, you can view the stream by clicking on the "Overview" tab for the table and then clicking on the "Streams" tab.

![dynamodb-streams-1](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-streams-1.png)

DynamoDB Streams consists of a stream of records, where each record represents a change to an item in the table. You can learn more about DynamoDB Streams in the [DynamoDB Streams Developer Guide](http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Streams.html).

## DynamoDB Global Tables

DynamoDB Global Tables is a feature that allows you to replicate a DynamoDB table across multiple AWS regions. This can be used to build applications that are resilient to region-specific failures or that can offer low-latency access to data for users in different regions.

To create a global table, select the "Enable DynamoDB Global Tables" checkbox when creating the table.

![dynamodb-create-table-6](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-create-table-6.png)

On the next page, you'll be able to select the AWS regions where you want to replicate the table.

![dynamodb-global-tables-1](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-global-tables-1.png)

Once the table has been created, you can view the global table by clicking on the "Overview" tab for the table and then clicking on the "Global Tables" tab.

![dynamodb-global-tables-2](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-global-tables-2.png)

DynamoDB Global Tables replicates data across regions automatically, and you can read and write data to the table in any region. You can learn more about DynamoDB Global Tables in the [DynamoDB Global Tables Developer Guide](http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GlobalTables.html).

## Integrating DynamoDB with a Web Application

Now that we've seen how to create and manipulate DynamoDB tables, let's look at how we can integrate DynamoDB with a web application. We'll use the [AWS SDK for JavaScript](https://aws.amazon.com/sdk-for-javascript/) to interact with DynamoDB from a Node.js web application.

First, we'll install the SDK using [npm](https://www.npmjs.com/), the Node.js package manager.

```
npm install aws-sdk
```

Next, we'll create a file named `dynamodb.js` that contains the following code. This code will configure the SDK and export an object that contains methods for working with DynamoDB.

```javascript
var AWS = require('aws-sdk');

AWS.config.update({
  region: "us-west-2",
  endpoint: "http://localhost:8000"
});

var docClient = new AWS.DynamoDB.DocumentClient();

module.exports = {
  getMovies: function(year, title, callback) {
    var params = {
      TableName: "Movies",
      Key:{
        "year": year,
        "title": title
      }
    };

    docClient.get(params, function(err, data) {
      if (err) {
        console.error("Unable to read item. Error JSON:", JSON.stringify(err, null, 2));
      } else {
        callback(data);
      }
    });
  },
  addMovie: function(year, title, info, callback) {
    var params = {
      TableName: "Movies",
      Item:{
        "year": year,
        "title": title,
        "info": info
      }
    };

    docClient.put(params, function(err, data) {
      if (err) {
        console.error("Unable to add item. Error JSON:", JSON.stringify(err, null, 2));
      } else {
        callback();
      }
    });
  },
  updateMovie: function(year, title, info, callback) {
    var params = {
      TableName: "Movies",
      Key:{
        "year": year,
        "title": title
      },
      UpdateExpression: "set info.rating = :r, info.plot=:p, info.actors=:a",
      ExpressionAttributeValues:{
        ":r": info.rating,
        ":p": info.plot,
        ":a": info.actors
      },
      ReturnValues:"UPDATED_NEW"
    };

    docClient.update(params, function(err, data) {
      if (err) {
        console.error("Unable to update item. Error JSON:", JSON.stringify(err, null, 2));
      } else {
        callback();
      }
    });
  },
  deleteMovie: function(year, title, callback) {
    var params = {
      TableName: "Movies",
      Key:{
        "year": year,
        "title": title
      }
    };

    docClient.delete(params, function(err, data) {
      if (err) {
        console.error("Unable to delete item. Error JSON:", JSON.stringify(err, null, 2));
      } else {
        callback();
      }
    });
  }
}
```

This code configures the SDK to connect to a local DynamoDB instance. It then exports an object that contains methods for working with DynamoDB. These methods can be used to get, add, update, and delete items in a DynamoDB table.

Finally, we'll create a file named `server.js` that contains the following code. This code uses the [Express](https://expressjs.com/) web framework to create a simple web server. It also uses the DynamoDB methods we defined in the `dynamodb.js` file to interact with DynamoDB.

```javascript
var express = require('express');
var app = express();
var bodyParser = require('body-parser');
var dynamodb = require('./dynamodb');

app.use(bodyParser.json());

app.get('/movies/:year/:title', function(req, res) {
  var year = req.params.year;
  var title = req.params.title;

  dynamodb.getMovies(year, title, function(data) {
    res.json(data);
  });
});

app.post('/movies', function(req, res) {
  var year = req.body.year;
  var title = req.body.title;
  var info = req.body.info;

  dynamodb.addMovie(year, title, info, function() {
    res.sendStatus(201);
  });
});

app.put('/movies/:year/:title', function(req, res) {
  var year = req.params.year;
  var title = req.params.title;
  var info = req.body.info;

  dynamodb.updateMovie(year, title, info, function() {
    res.sendStatus(200);
  });
});

app.delete('/movies/:year/:title', function(req, res) {
  var year = req.params.year;
  var title = req.params.title;

  dynamodb.deleteMovie(year, title, function() {
    res.sendStatus(200);
  });
});

app.listen(3000, function() {
  console.log('Movie API listening on port 3000!');
});
```

This code defines routes for getting, adding, updating, and deleting movies. Each route uses the DynamoDB methods we defined in the `dynamodb.js` file to interact with DynamoDB.

## Conclusion

In this article, we've looked at how to create a DynamoDB table and integrate it with a web application. We've also seen how to use some of the key features of DynamoDB, including DynamoDB Streams and DynamoDB Global Tables.

If you're interested in learni more about DynamoDB, be sure to check out the [DynamoDB Developer Guide](http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/).