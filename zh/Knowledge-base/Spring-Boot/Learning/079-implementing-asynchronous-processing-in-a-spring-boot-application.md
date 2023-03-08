---
title: 079：在 Spring Boot 应用程序中实现异步处理
description: 
published: true
date: 2023-02-05T10:32:15.894Z
tags: 
editor: markdown
dateCreated: 2023-02-05T10:32:14.257Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [079: Implementing Asynchronous Processing in a Spring Boot Application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/079-implementing-asynchronous-processing-in-a-spring-boot-application)
{.links-list}


# 079：在 Spring Boot 应用程序中实现异步处理

异步处理是一种以并行或非阻塞方式处理任务的方式。在 Spring Boot 应用程序中，异步处理可用于通过将长时间运行的任务卸载到单独的线程来提高它们的性能。

在本文中，我们将了解如何在 Spring Boot 应用程序中实现异步处理。我们将从查看可在 Spring Boot 中使用的不同类型的异步处理开始。然后我们将看看如何配置 Spring Boot 以使用异步处理。最后，我们将看看在 Spring Boot 应用程序中使用异步处理的一些技巧。

## 异步处理的类型

Spring Boot 中可以使用两种类型的异步处理：

* 并行处理：这是一种异步处理，任务并行执行。并行处理可用于通过跨多个线程分配工作来提高长时间运行任务的性能。

* 非阻塞处理：这是一种异步处理，任务以非阻塞方式执行。非阻塞处理可用于通过避免等待长时间运行的任务完成来提高应用程序的响应能力。

## 配置异步处理

要在 Spring Boot 应用程序中使用异步处理，您需要将应用程序配置为使用任务执行器。任务执行器是负责以并行或非阻塞方式执行任务的组件。

Spring Boot 提供了许多不同的任务执行器，可用于不同类型的异步处理。例如SimpleAsyncTaskExecutor可以用于并行处理，CallableProcessingInterceptor可以用于非阻塞处理。

要将应用程序配置为使用任务执行器，您需要将以下属性添加到 application.properties 文件：

spring.task.executor.pool.size=10

此属性配置任务执行程序池的大小。任务执行器池用于以并行或非阻塞方式执行任务。

## 使用异步处理的技巧

在 Spring Boot 应用程序中使用异步处理时，需要注意以下几点：

* 避免使用同步方法：当使用异步处理时，避免使用同步方法。同步方法可以阻塞正在执行任务的线程，这会导致任务需要更长的时间才能完成。

* 使用任务执行器：当使用异步处理时，一定要使用任务执行器。任务执行器可以通过将工作分配到多个线程来帮助提高长时间运行任务的性能。

* 使用回调：当使用异步处理时，一定要使用回调。回调可以避免等待长时间运行的任务完成，从而有助于提高应用程序的响应能力。