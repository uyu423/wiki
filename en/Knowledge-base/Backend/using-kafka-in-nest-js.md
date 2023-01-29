---
title: Using Kafka in Nest.js
description: 
published: true
date: 2023-01-29T20:18:41.101Z
tags: 
editor: markdown
dateCreated: 2023-01-29T20:18:41.101Z
---

- [Nest.js에서 Kafka 사용***Korean** version of this document is available*](/ko/Knowledge-base/Backend/using-kafka-in-nest-js)
{.links-list}

# Using Kafka in Nest.js

Kafka is a distributed streaming platform that can be used to build real-time data pipelines and streaming applications. Nest.js is a Node.js framework for building scalable server-side applications. In this blog post, we'll show you how to use Kafka with Nest.js.

## Prerequisites

- Node.js and npm installed
- A Kafka cluster up and running

## Installing the dependencies

First, we need to install the dependencies. We'll be using the `kafka-node` and `nestjs-kafka` packages.

```
npm install kafka-node nestjs-kafka --save
```

## Configuring Kafka

Next, we need to configure Kafka. We'll create a file called `kafka.config.js` in the root of our project and add the following content:

```js
const Kafka = require('kafka-node');

const kafkaHost = 'localhost:9092'; // your Kafka host

const kafkaClient = new Kafka.Client(kafkaHost);
const kafkaConsumer = new Kafka.HighLevelConsumer(kafkaClient, [
  { topic: 'my-topic' } // your Kafka topic
], {
  groupId: 'my-consumer-group',
  autoCommit: true,
  fromOffset: false
});

module.exports = {
  kafkaClient,
  kafkaConsumer
};
```

In the code above, we're configuring a Kafka client and a Kafka consumer. We're also specifying the Kafka host and the Kafka topic that we want to consume.

## Creating a Nest.js module

Now that we have our dependencies installed and our Kafka cluster configured, we can create a Nest.js module. We'll create a file called `src/app.module.ts` and add the following content:

```ts
import { Module } from '@nestjs/common';
import { KafkaModule } from 'nestjs-kafka';
import { AppController } from './app.controller';

@Module({
  imports: [
    KafkaModule.forRoot({
      options: {
        kafkaHost: 'localhost:9092' // your Kafka host
      }
    })
  ],
  controllers: [AppController]
})
export class AppModule {}
```

In the code above, we're importing the `KafkaModule` from the `nestjs-kafka` package. We're also configuring the Kafka host in the `forRoot` method.

## Creating a Nest.js controller

Now that we have our Nest.js module created, we can create a controller. We'll create a file called `src/app.controller.ts` and add the following content:

```ts
import { Controller, Get } from '@nestjs/common';
import { Client, Consumer } from 'kafka-node';

@Controller()
export class AppController {
  constructor(private readonly kafkaClient: Client, private readonly kafkaConsumer: Consumer) {}

  @Get()
  root() {
    this.kafkaConsumer.on('message', message => {
      console.log(message);
    });

    return 'Hello World!';
  }
}
```

In the code above, we're injecting the Kafka client and the Kafka consumer that we created in the `kafka.config.js` file. We're also creating a `GET` endpoint that will consume messages from our Kafka topic.

## Running the application

Now that we have our Nest.js application created, we can run it. We'll use the `npm` script that we defined in the `package.json` file.

```
npm start
```

## Testing the application

To test our Nest.js application, we'll use the `kafka-console-producer.sh` script that's included in the Kafka distribution. We'll use the `--broker-list` option to specify our Kafka broker and the `--topic` option to specify our Kafka topic.

```
kafka-console-producer.sh --broker-list localhost:9092 --topic my-topic
```

Now, we can type messages into the console and they should be consumed by our Nest.js application.

## Conclusion

In this blog post, we've shown you how to use Kafka with Nest.js. We've installed the dependencies, created a Nest.js module, created a controller, and ran the application. We've also tested the application by sending messages to our Kafka topic.