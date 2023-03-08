---
title: Kubernetes Extension APIs: Enhancing the Functionality of Your Cluster
description: 
published: true
date: 2023-02-17T18:17:21.143Z
tags: 
editor: markdown
dateCreated: 2023-01-31T02:23:22.396Z
---

- [Kubernetes 확장 API: 클러스터의 기능 향상***Korean** version of this document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-extension-apis-enhancing-the-functionality-of-your-cluster)
{.links-list}
- [Kubernetes 拡張 API: クラスターの機能を強化する***Japanese** version of this document is available*](/ja/Knowledge-base/Kubernetes/kubernetes-extension-apis-enhancing-the-functionality-of-your-cluster)
{.links-list}
- [Kubernetes 扩展 API：增强集群的功能***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-extension-apis-enhancing-the-functionality-of-your-cluster)
{.links-list}



# Kubernetes Extension APIs: Enhancing the Functionality of Your Cluster

Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications. It groups containers that make up an application into logical units for easy management and discovery. Kubernetes also provides mechanisms for storage orchestration, networking, and security.

Extending Kubernetes functionality is a popular topic, and there are many ways to do so. In this article, we'll focus on Kubernetes Extension APIs. We'll discuss what they are, how they work, and why you might want to use them. We'll also provide some sample code to get you started.

## What are Kubernetes Extension APIs?

Kubernetes Extension APIs are a set of APIs that allow you to extend the functionality of your Kubernetes cluster. They provide a way to add new functionality to Kubernetes without changing the core code.

Extension APIs are implemented as CustomResourceDefinitions (CRDs). CRDs are a way to add new resources to Kubernetes. A resource is an object that can be managed by Kubernetes, such as a pod or a service. CRDs allow you to define new resources that Kubernetes can manage.

## How do Kubernetes Extension APIs work?

Kubernetes Extension APIs are implemented as CustomResourceDefinitions (CRDs). CRDs are a way to add new resources to Kubernetes. A resource is an object that can be managed by Kubernetes, such as a pod or a service. CRDs allow you to define new resources that Kubernetes can manage.

Each CRD has a description of the resource, including the name, type, and properties. Kubernetes uses this information to create the new resource. You can then use the Kubernetes API to manage this new resource.

## Why use Kubernetes Extension APIs?

Kubernetes Extension APIs provide a way to add new functionality to Kubernetes without changing the core code. This can be useful if you want to add a newfeature, or if you want to experiment with new code without affecting the stability of your cluster.

Extension APIs also provide a way to share your code with the Kubernetes community. If you think your code would be useful to others, you can submit it to be included in Kubernetes.

## Sample Code

Here's a simple example of a CustomResourceDefinition:

```
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  name: mycrd.example.com
spec:
  scope: Cluster
  group: example.com
  version: v1
  names:
    plural: mycrds
    singular: mycrd
    kind: MyCrd
    shortNames:
    - crd
  validation:
    openAPIV3Schema:
      description: MyCrds are ..."
      type: object
      properties:
        spec:
          type: object
          properties:
            size:
              type: integer
              minimum: 1
              maximum: 100
          required:
          - size
  subresources:
    status: {}
```

This CRD defines a resource called "MyCrd". This resource has a property called "size", which is an integer between 1 and 100.

You can use the Kubernetes API to create, update, and delete MyCrds:

```
# Create a MyCrd
apiVersion: example.com/v1
kind: MyCrd
metadata:
  name: mycrd-1
spec:
  size: 10

# Update a MyCrd
apiVersion: example.com/v1
kind: MyCrd
metadata:
  name: mycrd-1
spec:
  size: 20

# Delete a MyCrd
apiVersion: example.com/v1
kind: MyCrd
metadata:
  name: mycrd-1
spec:
  size: 0
```

## Conclusion

Kubernetes Extension APIs provide a way to add new functionality to Kubernetes without changing the core code. They are implemented as CustomResourceDefinitions (CRDs), which are a way to add new resources to Kubernetes. Each CRD has a description of the resource, including the name, type, and properties. Kubernetes uses this information to create the new resource.

You can use Kubernetes Extension APIs to add new features to Kubernetes, or to experiment with new code without affecting the stability of your cluster. If you think your code would be useful to others, you can submit it to be included in Kubernetes.