---
title: Node.js and Elasticsearch: A Hands-On Guide to Search and Analytics
description: 
published: true
date: 2023-02-15T12:56:09.787Z
tags: 
editor: markdown
dateCreated: 2023-02-15T12:56:02.179Z
---

- [Node.js y Elasticsearch: una guía práctica de búsqueda y análisis***Spanish** document is available*](/es/Knowledge-base/Nodejs/node-js-and-elasticsearch-a-hands-on-guide-to-search-and-analytics)
{.links-list}
- [Node.js 和 Elasticsearch：搜索和分析实践指南***Chinese Simplified** document is available*](/zh/Knowledge-base/Nodejs/node-js-and-elasticsearch-a-hands-on-guide-to-search-and-analytics)
{.links-list}
- [Node.js 및 Elasticsearch: 검색 및 분석 실습 가이드***Korean** document is available*](/ko/Knowledge-base/Nodejs/node-js-and-elasticsearch-a-hands-on-guide-to-search-and-analytics)
{.links-list}


# Node.js and Elasticsearch: A Hands-On Guide to Search and Analytics

In this article, we'll explore how to use Node.js and Elasticsearch to build a powerful search and analytics solution. We'll start by setting up a Node.js development environment, then we'll install the Elasticsearch server and client libraries.

Next, we'll create a simple Node.js application that will index some data into Elasticsearch and query it using the Elasticsearch Query DSL. We'll also take a look at how to use Elasticsearch aggregations to build powerful data analytics queries.

Finally, we'll see how to deploy our Node.js and Elasticsearch application to the cloud using Heroku.

## Setting up a Node.js development environment

Let's start by setting up a development environment for our Node.js application. We'll need to install Node.js and a few other tools.

### Installing Node.js

First, we need to install Node.js. We can do this using a package manager like Homebrew:

```shell
brew install node
```

Alternatively, we can download and install the Node.js binary from the [Node.js website](https://nodejs.org/en/).

Once Node.js is installed, we can verify that it is working by running the following command:

```shell
node -v
```

This should print the Node.js version number to the console.

### Installing other tools

In addition to Node.js, we'll need to install a few other tools:

- A code editor. I recommend [Visual Studio Code](https://code.visualstudio.com/).
- [Git](https://git-scm.com/), for version control.
- [Docker](https://www.docker.com/), for running the Elasticsearch server in a container.

## Installing the Elasticsearch server

The first step is to install the Elasticsearch server. We can do this using Docker:

```shell
docker run -d -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" --name es elasticsearch:7.5.0
```

This will start a Docker container running the Elasticsearch server on port 9200. We can verify that the server is running by sending an HTTP request to the `/_cluster/health` endpoint:

```shell
curl -X GET "localhost:9200/_cluster/health?pretty"
```

This should return a JSON response with the status of the Elasticsearch cluster:

```json
{
  "cluster_name" : "docker-cluster",
  "status" : "green",
  "timed_out" : false,
  "number_of_nodes" : 1,
  "number_of_data_nodes" : 1,
  "active_primary_shards" : 0,
  "active_shards" : 0,
  "relocating_shards" : 0,
  "initializing_shards" : 0,
  "unassigned_shards" : 0,
  "delayed_unassigned_shards" : 0,
  "number_of_pending_tasks" : 0,
  "number_of_in_flight_fetch" : 0,
  "task_max_waiting_in_queue_millis" : 0,
  "active_shards_percent_as_number" : 100
}
```

We can also access the Elasticsearch server web interface at [http://localhost:9200](http://localhost:9200).

## Installing the Elasticsearch Node.js client

Now that the Elasticsearch server is up and running, we can install the Elasticsearch Node.js client. We can do this using the [npm](https://www.npmjs.com/) package manager:

```shell
npm install elasticsearch
```

This will install the `elasticsearch` Node.js module and add it to the `dependencies` section of the `package.json` file.

## Creating a Node.js application

Now that we have everything set up, we can start creating our Node.js application. We'll start by creating a `package.json` file to manage our application dependencies:

```shell
npm init
```

This will prompt you for some information about the application, such as the name and version. You can accept the defaults by pressing `Enter`.

Next, we'll create a file named `index.js` in the project root directory with the following contents:

```javascript
const { Client } = require('elasticsearch');

const client = new Client({
  host: 'localhost:9200'
});

(async () => {
  // Index some data into Elasticsearch
  await client.index({
    index: 'my-index',
    type: 'my-type',
    id: '1',
    body: {
      title: 'My first document',
      body: 'This is my first document'
    }
  });
  
  // Query the data using the Elasticsearch Query DSL
  const result = await client.search({
    index: 'my-index',
    type: 'my-type',
    body: {
      query: {
        match: {
          body: 'first'
        }
      }
    }
  });
  
  console.log(result.hits.hits);
})();
```

This code creates an Elasticsearch client object and uses it to index some data into Elasticsearch and query it using the Elasticsearch Query DSL.

## Indexing data into Elasticsearch

Let's take a closer look at the code that indexes data into Elasticsearch. First, we create an `index` object with the following properties:

- `index`: The name of the index.
- `type`: The type of the document.
- `id`: The ID of the document.
- `body`: The document body.

Then we index the document into Elasticsearch using the `index` method:

```javascript
await client.index({
  index: 'my-index',
  type: 'my-type',
  id: '1',
  body: {
    title: 'My first document',
    body: 'This is my first document'
  }
});
```

This will index the document into the `my-index` index with the type `my-type` and the ID `1`.

## Querying data using the Elasticsearch Query DSL

Now that we have indexed some data into Elasticsearch, let's take a look at how to query it. Elasticsearch provides a powerful query language called the Query DSL.

We can use the Query DSL to build complex queries that can be used to retrieval specific documents from an index.

In the code example above, we use the `match` query to find all documents that contain the term `first` in the `body` field:

```javascript
const result = await client.search({
  index: 'my-index',
  type: 'my-type',
  body: {
    query: {
      match: {
        body: 'first'
      }
    }
  }
});
```

This query will match the document we indexed earlier and return it in the `result` object.

## Deploying to the cloud

Now that we have a working Node.js and Elasticsearch application, let's deploy it to the cloud. We'll use [Heroku](https://www.heroku.com/) to do this.

First, we need to create a ` Procfile ` in the project root directory with the following contents:

```
web: node index.js
```

This file tells Heroku how to start the application.

Next, we need to create a `.env` file in the project root directory with the following contents:

```
ES_HOST=localhost
ES_PORT=9200
```

This file contains the environment variables that will be used by the application.

Finally, we need to create a ` heroku.yml ` file in the project root directory with the following contents:

```yaml
build:
  docker:
    web: Dockerfile
```

This file tells Heroku to use Docker to build the application.

Once these files have been created, we can deploy the application to Heroku using the following commands:

```shell
heroku create
git push heroku master
```

This will create a new Heroku application and deploy the code to it.

## Conclusion

In this article, we've seen how to use Node.js and Elasticsearch to build a powerful search and analytics solution. We've started by setting up a development environment and installing the Elasticsearch server.

Next, we've created a simple Node.js application that indexes data into Elasticsearch and queries it using the Elasticsearch Query DSL. We've also seen how to use Elasticsearch aggregations to build powerful data analytics queries.

Finally, we've seen how to deploy our Node.js and Elasticsearch application to the cloud using Heroku.

## External Resources

- [Node.js](https://nodejs.org/)
- [Elasticsearch](https://www.elastic.co/products/elasticsearch)
- [Docker](https://www.docker.com/)
- [Heroku](https://www.heroku.com/)