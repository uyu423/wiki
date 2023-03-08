---
title: 使用 ElastiCache 和 ElasticBeanstalk 扩展应用程序
description: 
published: true
date: 2023-02-17T18:14:25.187Z
tags: 
editor: markdown
dateCreated: 2023-01-30T21:23:16.332Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Scaling Applications with ElastiCache and ElasticBeanstalk***English** version of this document is available*](/en/Knowledge-base/Backend/scaling-applications-with-elasticache-and-elasticbeanstalk)
{.links-list}
 

## 使用 ElastiCache 和 ElasticBeanstalk 扩展应用程序

在本文中，我们将介绍两种可帮助您扩展应用程序的 Amazon Web Services (AWS) 产品：ElastiCache 和 Elastic Beanstalk。我们将讨论这些产品如何工作以及如何使用它们来扩展您的应用程序。

ElastiCache 是一种 Web 服务，可以轻松地在云中部署、操作和扩展内存缓存。 ElastiCache 支持两种开源缓存引擎：Memcached 和 Redis。

Elastic Beanstalk 是一种 Web 服务，可让您轻松地在 AWS 云中部署和管理 Web 应用程序。 Elastic Beanstalk 提供了一个用于部署和运行 Web 应用程序的平台。它自动处理容量配置、负载平衡、扩展和应用程序运行状况监控的细节。

如果您将 ElastiCache 与 Elastic Beanstalk 结合使用，则可以利用 ElastiCache 的垂直和水平扩展能力。垂直扩展意味着增加应用程序可用的内存量和/或 CPU 数量。水平扩展意味着向缓存集群添加更多节点。

ElastiCache 可以通过向缓存集群添加节点来垂直扩展。要水平扩展，您可以向 ElastiCache 集群添加更多节点。您还可以使用分片来水平扩展。分片是一种跨多个节点分布数据的技术。

Elastic Beanstalk 可以通过向您的环境添加更多 Web 服务器来水平扩展。您还可以通过增加可用于 Web 服务器的内存量和/或 CPU 数量来垂直扩展。

以下是使用 ElastiCache 和 Elastic Beanstalk 扩展应用程序的一些技巧：

- 使用 ElastiCache 缓存经常访问的数据。缓存可以通过减少访问数据库的次数来提高应用程序的性能。

- 使用 Elastic Beanstalk 部署和管理您的 Web 应用程序。 Elastic Beanstalk 提供了一个用于部署和运行 Web 应用程序的平台。它自动处理容量配置、负载平衡、扩展和应用程序运行状况监控的细节。

- 将 ElastiCache 与 Elastic Beanstalk 结合使用，以利用 ElastiCache 的垂直和水平扩展能力。垂直扩展意味着增加应用程序可用的内存量和/或 CPU 数量。水平扩展意味着向缓存集群添加更多节点。

- 使用分片水平扩展 ElastiCache。分片是一种跨多个节点分布数据的技术。

- 使用 Elastic Beanstalk 通过向您的环境添加更多 Web 服务器来横向扩展。您还可以通过增加可用于 Web 服务器的内存量和/或 CPU 数量来垂直扩展。