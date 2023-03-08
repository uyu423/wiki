---
title: Debugging Kubernetes Applications: Understanding Events and Logs
description: 
published: true
date: 2023-02-17T18:16:15.975Z
tags: 
editor: markdown
dateCreated: 2023-01-31T00:43:18.510Z
---

- [Kubernetes 애플리케이션 디버깅: 이벤트 및 로그 이해***Korean** version of this document is available*](/ko/Knowledge-base/Kubernetes/debugging-kubernetes-applications-understanding-events-and-logs)
{.links-list}
- [Kubernetes アプリケーションのデバッグ: イベントとログについて***Japanese** version of this document is available*](/ja/Knowledge-base/Kubernetes/debugging-kubernetes-applications-understanding-events-and-logs)
{.links-list}
- [调试 Kubernetes 应用程序：了解事件和日志***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kubernetes/debugging-kubernetes-applications-understanding-events-and-logs)
{.links-list}


# Debugging Kubernetes Applications: Understanding Events and Logs

Kubernetes is a powerful orchestration tool, but it can be tricky to debug applications running on it. In this article, we'll take a look at two important tools for debugging Kubernetes applications: events and logs.

## Events

Events are a great way to get visibility into what's happening inside a Kubernetes cluster. To view events, use the `kubectl` command:

```
kubectl get events
```

This will return a list of all the events in the cluster, along with their timestamps, types, and so on.

Events can be filtered by label, so if you want to see only the events related to a particular pod, you can use the `--selector` flag:

```
kubectl get events --selector=app=nginx
```

It's also possible to see the events for a particular namespace:

```
kubectl get events --namespace=default
```

Finally, you can use the `--since` flag to only get events that have occurred since a certain time:

```
kubectl get events --since=2019-01-01T00:00:00Z
```

## Logs

In addition to events, logs are another important tool for debugging Kubernetes applications. To get the logs for a pod, use the `kubectl` command:

```
kubectl logs POD_NAME
```

Replace `POD_NAME` with the name of the pod you want to get the logs for.

It's also possible to get the logs for all the pods in a deployment:

```
kubectl logs DEPLOYMENT_NAME
```

Replace `DEPLOYMENT_NAME` with the name of the deployment you want to get the logs for.

Finally, you can use the `--since` flag to only get logs that have been generated since a certain time:

```
kubectl logs --since=2019-01-01T00:00:00Z
```

## Conclusion

In this article, we've looked at two important tools for debugging Kubernetes applications: events and logs. Events are a great way to get visibility into what's happening inside a Kubernetes cluster, and logs can be used to troubleshoot problems with your applications.