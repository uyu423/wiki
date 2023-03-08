---
title: Kubernetes Resource Management: Setting Limits and Requests for Your Pods
description: 
published: true
date: 2023-02-05T20:17:26.054Z
tags: 
editor: markdown
dateCreated: 2023-02-05T20:17:20.634Z
---

- [Gestión de recursos de Kubernetes: configuración de límites y solicitudes para sus pods***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-resource-management-setting-limits-and-requests-for-your-pods)
{.links-list}
- [Kubernetes 资源管理：为您的 Pod 设置限制和请求***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-resource-management-setting-limits-and-requests-for-your-pods)
{.links-list}
- [Kubernetes 리소스 관리: Pod에 대한 제한 및 요청 설정***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-resource-management-setting-limits-and-requests-for-your-pods)
{.links-list}


# Kubernetes Resource Management: Setting Limits and Requests for Your Pods

In a production environment, you need to be able to control the resources that your applications use. This is especially important in a containerized environment like Kubernetes, where many applications can be running on the same cluster.

There are two main ways to do this in Kubernetes: setting limits and requests. Limits define the maximum amount of resources that a pod can use, while requests define the minimum amount of resources that a pod needs.

In this article, we'll take a look at how to set limits and requests for your pods. We'll also look at some best practices for using these settings.

## How to Set Limits and Requests

Limits and requests are set as annotations on a pod. You can set them when you create a pod, or you can set them later using the kubectl annotate command.

Here's an example of how to set limits and requests when creating a pod:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
  annotations:
    "limits.cpu": "1",
    "requests.cpu": "0.5"
spec:
  containers:
  - name: mycontainer
    image: myimage
```

In this example, we're setting a limit of 1 CPU and a request of 0.5 CPU.

You can also set these annotations using the kubectl annotate command:

```
kubectl annotate pod mypod "limits.cpu=1" "requests.cpu=0.5"
```

## Best Practices

There are a few best practices to keep in mind when setting limits and requests:

* Set both limits and requests for each resource. If you only set a limit, Kubernetes will not enforce it.
* Make sure that your requests are less than your limits. If they're not, your pod will not be scheduled.
* Try to set your requests and limits as close to each other as possible. This will help to ensure that your pod gets the resources it needs.
* Be aware of the default limits that are set by your cluster. If you don't set limits and requests, your pod will use these defaults.

## Conclusion

In this article, we've looked at how to set limits and requests for your pods. We've also looked at some best practices for using these settings. By following these best practices, you can ensure that your pods get the resources they need without using more resources than necessary.