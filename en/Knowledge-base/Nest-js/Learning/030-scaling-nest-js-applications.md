---
title: 030: Scaling Nest.js applications
description: 
published: true
date: 2023-02-15T09:32:23.702Z
tags: 
editor: markdown
dateCreated: 2023-02-15T09:32:21.976Z
---

- [030: Escalado de aplicaciones Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/030-scaling-nest-js-applications)
{.links-list}
- [030：扩展 Nest.js 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/030-scaling-nest-js-applications)
{.links-list}
- [030: Nest.js 애플리케이션 확장***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/030-scaling-nest-js-applications)
{.links-list}


# Scaling Nest.js Applications

As your application grows, you'll eventually need to start thinking about how to scale it. In this article, we'll take a look at some of the options available to you when scaling a Nest.js application.

## Scaling horizontally

One way to scale an application is to add more servers, or nodes, to the application. This is known as horizontal scaling.

Adding more nodes to an application has a few benefits. First, it allows the application to handle more traffic. Second, it can improve performance, since each node can handle requests independently.

There are a few things to keep in mind when scaling horizontally. First, you'll need to make sure that each node has a unique ID. This is so that the load balancer can send traffic to the correct node.

Second, you'll need to make sure that the nodes are stateless. This means that each node can handle any request, regardless of the state of the other nodes.

Third, you'll need to use a load balancer. A load balancer is a piece of software that sits in front of the application and routes traffic to the different nodes.

There are a few different options available for load balancers, but we'll use nginx in this example.

Fourth, you'll need to make sure that the nodes can communicate with each other. This is so that they can share information, such as session data.

Finally, you'll need to make sure that the nodes can be added and removed dynamically. This is so that the application can be scaled up or down as needed.

## Scaling vertically

Another way to scale an application is to add more resources to a single node. This is known as vertical scaling.

Adding more resources to a node has a few benefits. First, it allows the node to handle more traffic. Second, it can improve performance, since the node has more resources to work with.

There are a few things to keep in mind when scaling vertically. First, you'll need to make sure that the node can be added and removed dynamically. This is so that the application can be scaled up or down as needed.

Second, you'll need to make sure that the node can be upgraded without affecting the other nodes. This is so that you can add more resources to the node without affecting the performance of the other nodes.

Third, you'll need to make sure that the node can be downgraded without affecting the other nodes. This is so that you can remove resources from the node without affecting the performance of the other nodes.

Fourth, you'll need to make sure that the node can be migrated without affecting the other nodes. This is so that you can move the node to a different server without affecting the performance of the other nodes.

Finally, you'll need to make sure that the node can be replicated without affecting the other nodes. This is so that you can create a copy of the node on another server without affecting the performance of the other nodes.

## Conclusion

Scaling an application is an important part of growing a business. There are a few different options available to you when scaling a Nest.js application. You can scale horizontally by adding more nodes to the application, or you can scale vertically by adding more resources to a single node.