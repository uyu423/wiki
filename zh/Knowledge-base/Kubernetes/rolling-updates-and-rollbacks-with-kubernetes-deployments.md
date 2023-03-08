---
title: 使用 Kubernetes 部署进行滚动更新和回滚
description: 
published: true
date: 2023-01-31T11:36:19.674Z
tags: 
editor: markdown
dateCreated: 2023-01-31T11:36:18.139Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Rolling Updates and Rollbacks with Kubernetes Deployments***English** version of this document is available*](/en/Knowledge-base/Kubernetes/rolling-updates-and-rollbacks-with-kubernetes-deployments)
{.links-list}



# 使用 Kubernetes 部署进行滚动更新和回滚

在生产环境中，经常需要在不停机的情况下更新应用程序。 Kubernetes 提供了一个称为“滚动更新”的功能来帮助解决这个问题。本指南将解释什么是“滚动更新”以及如何使用它们。

## 什么是滚动更新？

滚动更新是一种在停机时间最少或没有停机的情况下更新软件的方法。通过这种方式，新版本的软件逐渐部署到服务器上。这确保始终有可用的软件工作版本，即使某些服务器正在更新。

## 滚动更新如何工作？

滚动更新是通过更新部署中的各个 pod 来执行的。 Kubernetes 将一次更新一个 pod。这确保始终有可用的软件工作版本。

## 如何执行滚动更新？

要执行滚动更新，您需要使用新图像更新部署的“规范”。然后 Kubernetes 将一次更新一个 pod。

## 更新出现问题怎么办？

如果更新有问题，可以将部署回滚到之前的版本。为此，您需要使用之前的图像更新部署的“规范”。然后 Kubernetes 将一次更新一个 pod。

## 结论

滚动更新是一种在停机时间最少或不停机的情况下更新软件的好方法。 Kubernetes 通过其“滚动更新”功能可以轻松执行滚动更新。