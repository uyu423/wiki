---
title: Rolling Updates and Rollbacks with Kubernetes Deployments
description: 
published: true
date: 2023-01-31T11:36:21.605Z
tags: 
editor: markdown
dateCreated: 2023-01-31T11:36:18.137Z
---

- [Kubernetes 배포를 통한 롤링 업데이트 및 롤백***Korean** version of this document is available*](/ko/Knowledge-base/Kubernetes/rolling-updates-and-rollbacks-with-kubernetes-deployments)
{.links-list}
- [Kubernetes デプロイメントでのローリング アップデートとロールバック***Japanese** version of this document is available*](/ja/Knowledge-base/Kubernetes/rolling-updates-and-rollbacks-with-kubernetes-deployments)
{.links-list}
- [使用 Kubernetes 部署进行滚动更新和回滚***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kubernetes/rolling-updates-and-rollbacks-with-kubernetes-deployments)
{.links-list}



# Rolling Updates and Rollbacks with Kubernetes Deployments

In a production environment, it is often necessary to update applications without downtime. Kubernetes provides a feature called `Rolling Updates` to help with this. This guide will explain what `Rolling Updates` are and how to use them.

## What are Rolling Updates?

Rolling updates are a method of updating software with minimal or no downtime. With this method, new versions of the software are gradually deployed to servers. This ensures that there is always a working version of the software available, even if some of the servers are being updated.

## How do Rolling Updates work?

Rolling updates are performed by updating individual pods in a deployment. Kubernetes will update the pods one at a time. This ensures that there is always a working version of the software available.

## How do I perform a Rolling Update?

To perform a rolling update, you need to update the deployment's `spec` with the new image. Kubernetes will then update the pods one at a time.

## What if there is a problem with the update?

If there is a problem with the update, you can rollback the deployment to the previous version. To do this, you need to update the deployment's `spec` with the previous image. Kubernetes will then update the pods one at a time.

## Conclusion

Rolling updates are a great way to update software with minimal or no downtime. Kubernetes makes it easy to perform rolling updates with its `Rolling Updates` feature.