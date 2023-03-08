---
title: Kubernetes Custom Resource Definitions: Extending the Kubernetes API
description: 
published: true
date: 2023-02-01T08:24:15.554Z
tags: 
editor: markdown
dateCreated: 2023-02-01T08:24:12.119Z
---

- [Kubernetes 사용자 지정 리소스 정의: Kubernetes API 확장***Korean** version of this document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-custom-resource-definitions-extending-the-kubernetes-api)
{.links-list}
- [Kubernetes 自定义资源定义：扩展 Kubernetes API***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-custom-resource-definitions-extending-the-kubernetes-api)
{.links-list}



# Kubernetes Custom Resource Definitions: Extending the Kubernetes API

Kubernetes Custom Resource Definitions (CRDs) provide a way to extend the Kubernetes API with new resources that represent user-defined objects. CRDs allow Kubernetes administrators and developers to create and use new resources without having to modify the Kubernetes API server or write any code.

In this article, we'll take a look at how CRDs work and how you can use them to extend the Kubernetes API. We'll also explore some of the use cases for CRDs and look at some example CRDs that have been developed by the community.

## What are Kubernetes Custom Resource Definitions?

A Custom Resource Definition (CRD) is a way to define a new Kubernetes resource. CRDs are used to extend the Kubernetes API with new resources that represent user-defined objects. CRDs allow Kubernetes administrators and developers to create and use new resources without having to modify the Kubernetes API server or write any code.

CRDs are similar to the built-in Kubernetes resources, such as Pods and Services. Like built-in resources, CRDs have a name, a schema, and a set of operations (such as create, read, update, and delete). CRDs can also be used in conjunction with the built-in resources to create new, composite resources.

## How do Kubernetes Custom Resource Definitions work?

CRDs are stored in the Kubernetes API server and are used by the Kubernetes API server to validate and serve user requests. CRDs are defined using the OpenAPI v3 specification.

The OpenAPI v3 specification is a standard for describing RESTful APIs. It defines the structure of the API, the operations that can be performed, the input and output formats, and the authentication methods.

The OpenAPI v3 specification is used by the Kubernetes API server to validate user requests. When a user sends a request to the Kubernetes API server, the Kubernetes API server uses the OpenAPI v3 specification to validate the request. If the request is valid, the Kubernetes API server forwards the request to the appropriate CRD.

The Kubernetes API server uses the OpenAPI v3 specification to validate user requests. If the request is valid, the Kubernetes API server forwards the request to the appropriate CRD.

## What are the benefits of using Kubernetes Custom Resource Definitions?

CRDs have a number of benefits over traditional API development approaches:

- CRDs allow you to define new resources without having to modify the Kubernetes API server or write any code.
- CRDs are stored in the Kubernetes API server and are used by the Kubernetes API server to validate and serve user requests.
- CRDs are defined using the OpenAPI v3 specification, which is a standard for describing RESTful APIs.
- CRDs can be used in conjunction with the built-in resources to create new, composite resources.

## What are some use cases for Kubernetes Custom Resource Definitions?

CRDs can be used to extend the Kubernetes API with new resources that represent user-defined objects. CRDs allow Kubernetes administrators and developers to create and use new resources without having to modify the Kubernetes API server or write any code.

CRDs can be used to create new resources that represent:

- Cluster objects, such as Namespaces, Nodes, and Pods.
- Application objects, such as Deployments, Services, and Ingresses.
- Custom objects, such as customer records, order records, and product records.

## How do I create a Kubernetes Custom Resource Definition?

Creating a CRD is a two-step process:

1. Define the CRD using the OpenAPI v3 specification.
2. Register the CRD with the Kubernetes API server.

The OpenAPI v3 specification is a standard for describing RESTful APIs. It defines the structure of the API, the operations that can be performed, the input and output formats, and the authentication methods.

The OpenAPI v3 specification is used by the Kubernetes API server to validate user requests. When a user sends a request to the Kubernetes API server, the Kubernetes API server uses the OpenAPI v3 specification to validate the request. If the request is valid, the Kubernetes API server forwards the request to the appropriate CRD.

Registering the CRD with the Kubernetes API server is a two-step process:

1. Create a file named crd.yaml with the following contents:

```yaml
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  name: {crd-name}
spec:
  group: {crd-group}
  version: {crd-version}
  names:
    kind: {crd-kind}
    plural: {crd-plural}
  scope: {crd-scope}
```

2. Register the CRD with the Kubernetes API server:

```
kubectl create -f crd.yaml
```

## How do I use a Kubernetes Custom Resource Definition?

Once you have created a CRD, you can use it to create new resources. Creating a resource is a two-step process:

1. Define the resource using the OpenAPI v3 specification.
2. Create the resource using the kubectl create command.

The OpenAPI v3 specification is a standard for describing RESTful APIs. It defines the structure of the API, the operations that can be performed, the input and output formats, and the authentication methods.

The OpenAPI v3 specification is used by the Kubernetes API server to validate user requests. When a user sends a request to the Kubernetes API server, the Kubernetes API server uses the OpenAPI v3 specification to validate the request. If the request is valid, the Kubernetes API server forwards the request to the appropriate CRD.

Creating a resource is a two-step process:

1. Define the resource using the OpenAPI v3 specification.
2. Create the resource using the kubectl create command.

```
kubectl create -f {resource-definition.yaml}
```

## What are some example Kubernetes Custom Resource Definitions?

The following are some example CRDs that have been developed by the community:

- [Kubernetes Namespace](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/namespaces.md)
- [Kubernetes Node](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/nodes.md)
- [Kubernetes Pod](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/pods.md)
- [Kubernetes Service](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/services.md)
- [Kubernetes Deployment](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/deployments.md)
- [Kubernetes Ingress](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/ingresses.md)
- [Kubernetes Job](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/jobs.md)
- [Kubernetes CronJob](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/cronjobs.md)

## Conclusion

In this article, we've taken a look at how CRDs work and how you can use them to extend the Kubernetes API. We've also explored some of the use cases for CRDs and looked at some example CRDs that have been developed by the community.