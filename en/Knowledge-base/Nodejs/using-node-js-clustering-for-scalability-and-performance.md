---
title: Using Node.js Clustering for Scalability and Performance
description: 
published: true
date: 2023-03-01T20:32:38.527Z
tags: 
editor: markdown
dateCreated: 2023-03-01T20:32:31.330Z
---

- [확장성과 성능을 위해 Node.js 클러스터링 사용***Korean** document is available*](/ko/Knowledge-base/Nodejs/using-node-js-clustering-for-scalability-and-performance)
{.links-list}


# Using Node.js Clustering for Scalability and Performance

Node.js is a JavaScript runtime environment that enables developers to create scalable and high-performance applications. Node.js applications are event-driven and use a non-blocking I/O model, making them lightweight and efficient.

Node.js clustering is a process of running multiple instances of a Node.js application on a single server. Clustering is a way to increase the scalability and performance of a Node.js application. When multiple instances of a Node.js application are running on a single server, each instance can handle a different request. This way, the server can handle more requests and process them faster.

There are two ways to achieve clustering in Node.js:

- Use the built-in cluster module
- Use a third-party module like pm2

## Using the Built-in Cluster Module

Node.js comes with a built-in module called `cluster` that can be used for clustering. The `cluster` module allows developers to create child processes that share the same server port.

To use the `cluster` module, developers need to first require it in their application:

```javascript
const cluster = require('cluster');
```

After requiring the `cluster` module, developers can create a child process by using the `fork()` method:

```javascript
if (cluster.isMaster) {
  // This code will be executed by the master process
  cluster.fork();
} else {
  // This code will be executed by the child process
}
```

The `isMaster` property is a Boolean value that indicates whether the process is a master process or a child process. The master process is the process that initializes the clustering, and the child process is the process that shares the server port with the master process.

The `fork()` method creates a child process and returns a `worker` object. The `worker` object contains information about the child process, including the `worker.id` and `worker.process.pid` properties.

The `worker.id` property is a numeric value that is unique to each child process. The `worker.process.pid` property is the process ID of the child process.

After creating a child process, the master process can send messages to the child process using the `worker.send()` method:

```javascript
worker.send('Message from the master process');
```

The child process can receive messages from the master process using the `worker.on('message')` event:

```javascript
worker.on('message', (message) => {
  console.log(`Message from the master process: ${message}`);
});
```

The `worker.on('message')` event is triggered when the child process receives a message from the master process. The `message` argument is the message that was sent from the master process.

The master process can also send messages to all of the child processes using the `cluster.workers` property:

```javascript
for (const id in cluster.workers) {
  cluster.workers[id].send('Message from the master process');
}
```

The `cluster.workers` property is an object that contains all of the child processes. The `id` property is the unique ID of the child process, and the `cluster.workers[id]` property is the child process object.

The master process can also receive messages from all of the child processes using the `cluster.on('message')` event:

```javascript
cluster.on('message', (worker, message) => {
  console.log(`Message from worker ${worker.id}: ${message}`);
});
```

The `cluster.on('message')` event is triggered when the master process receives a message from a child process. The `worker` argument is the child process that sent the message, and the `message` argument is the message that was sent.

The master process can also terminate a child process using the `worker.kill()` method:

```javascript
worker.kill();
```

The `worker.kill()` method sends a `SIGTERM` signal to the child process, which terminates the child process.

The master process can also disconnect a child process using the `worker.disconnect()` method:

```javascript
worker.disconnect();
```

The `worker.disconnect()` method disconnects the child process from the master process. The child process will still be running, but it will no longer be able to communicate with the master process.

## Using PM2

PM2 is a third-party module that can be used for clustering. PM2 is a production process manager for Node.js applications. It enables developers to create and manage multiple processes and process groups.

To use PM2, developers need to first install it using NPM:

```javascript
npm install pm2 -g
```

After installing PM2, developers can start a Node.js application using the `pm2 start` command:

```javascript
pm2 start app.js
```

The `app.js` file is the entry point for the Node.js application.

PM2 will automatically start multiple instances of the Node.js application and load balance the requests between the instances.

PM2 also enables developers to monitor the state of their applications. Developers can view the current requests, memory usage, and CPU usage of their applications using the `pm2 monit` command:

```javascript
pm2 monit
```

PM2 also enables developers to view the log output of their applications. Developers can view the combined log output of all the instances of their applications using the `pm2 logs` command:

```javascript
pm2 logs
```

Developers can also view the log output of a specific instance of their application using the `--instance` option:

```javascript
pm2 logs --instance 0
```

The `--instance` option specifies the index of the instance. The index of the first instance is `0`.

Developers can also view the log output of all the instances of their application in real-time using the `--lines` option:

```javascript
pm2 logs --lines 1000
```

The `--lines` option specifies the number of lines of log output to display.

PM2 also enables developers to restart their applications. Developers can restart all the instances of their application using the `pm2 restart` command:

```javascript
pm2 restart app.js
```

Developers can also restart a specific instance of their application using the `--instance` option:

```javascript
pm2 restart app.js --instance 0
```

Developers can also stop their applications. Developers can stop all the instances of their application using the `pm2 stop` command:

```javascript
pm2 stop app.js
```

Developers can also stop a specific instance of their application using the `--instance` option:

```javascript
pm2 stop app.js --instance 0
```

## Conclusion

Node.js clustering is a process of running multiple instances of a Node.js application on a single server. Clustering is a way to increase the scalability and performance of a Node.js application.

There are two ways to achieve clustering in Node.js:

- Use the built-in cluster module
- Use a third-party module like pm2