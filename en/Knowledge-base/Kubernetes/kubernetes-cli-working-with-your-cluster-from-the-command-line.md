---
title: Kubernetes CLI: Working with Your Cluster from the Command Line
description: 
published: true
date: 2023-02-17T18:16:50.063Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:43:36.148Z
---

- [Kubernetes CLI: 명령줄에서 클러스터 작업***Korean** version of this document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-cli-working-with-your-cluster-from-the-command-line)
{.links-list}
- [Kubernetes CLI: コマンドラインからクラスターを操作する***Japanese** version of this document is available*](/ja/Knowledge-base/Kubernetes/kubernetes-cli-working-with-your-cluster-from-the-command-line)
{.links-list}
- [Kubernetes CLI：从命令行使用您的集群***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-cli-working-with-your-cluster-from-the-command-line)
{.links-list}

    

# Kubernetes CLI: Working with Your Cluster from the Command Line

The Kubernetes command-line interface (CLI), cfssl, is a tool that enables users to operate a Kubernetes cluster from the command line. This article provides an overview of how to install and set up the cfssl tool, and how to use it to manage a Kubernetes cluster.

## Installing the Cfssl Tool

The Cfssl tool can be installed on any Linux or macOS system. To install cfssl on Linux, use the following command:

```
$ curl -LO https://storage.googleapis.com/kubernetes-release/cfssl/cfssl_linux-amd64.tar.gz
$ tar -xzf cfssl_linux-amd64.tar.gz
$ mv cfssl_linux-amd64/bin/cfssl /usr/local/bin/
$ rm -rf cfssl_linux-amd64
```

To install cfssl on macOS, use the following command:

```
$ brew install cfssl
```

## Setting Up the Cfssl Tool

Once you have installed the cfssl tool, you need to set up your environment variables. The CFSSL_CA environment variable specifies the path to the CA certificate used by cfssl. The CFSSL_CERT environment variable specifies the path to the client certificate used by cfssl. The CFSSL_KEY environment variable specifies the path to the client key used by cfssl.

To set up the cfssl tool, use the following commands:

```
$ export CFSSL_CA=/path/to/ca.pem
$ export CFSSL_CERT=/path/to/client.pem
$ export CFSSL_KEY=/path/to/client-key.pem
```

## Creating a Kubernetes Cluster

Once you have installed and set up the cfssl tool, you can use it to create a Kubernetes cluster. To create a Kubernetes cluster, use the following command:

```
$ cfssl create-cluster -size=3 -server=https://kubernetes.default.svc.cluster.local:443 -ca=ca.pem -ca-key=ca-key.pem
```

This command creates a Kubernetes cluster with three nodes. The server flag specifies the URL of the Kubernetes API server. The ca flag specifies the path to the CA certificate used by cfssl. The ca-key flag specifies the path to the CA key used by cfssl.

## Deleting a Kubernetes Cluster

To delete a Kubernetes cluster, use the following command:

```
$ cfssl delete-cluster -name=my-cluster
```

This command deletes the Kubernetes cluster with the name my-cluster.

## Listing Kubernetes Clusters

To list the Kubernetes clusters created with cfssl, use the following command:

```
$ cfssl list-clusters
```

This command lists all of the Kubernetes clusters created with cfssl.

## Getting Cluster Information

To get information about a Kubernetes cluster, use the following command:

```
$ cfssl get-cluster -name=my-cluster
```

This command gets information about the Kubernetes cluster with the name my-cluster.

## Updating a Kubernetes Cluster

To update a Kubernetes cluster, use the following command:

```
$ cfssl update-cluster -name=my-cluster -size=5
```

This command updates the size of the Kubernetes cluster with the name my-cluster to five nodes.

## Adding Nodes to a Kubernetes Cluster

To add nodes to a Kubernetes cluster, use the following command:

```
$ cfssl add-node -name=my-cluster -size=3
```

This command adds three nodes to the Kubernetes cluster with the name my-cluster.

## Deleting Nodes from a Kubernetes Cluster

To delete nodes from a Kubernetes cluster, use the following command:

```
$ cfssl delete-node -name=my-cluster -size=3
```

This command deletes three nodes from the Kubernetes cluster with the name my-cluster.

## Scaling a Kubernetes Cluster

To scale a Kubernetes cluster, use the following command:

```
$ cfssl scale-cluster -name=my-cluster -size=5
```

This command scales the Kubernetes cluster with the name my-cluster to five nodes.

## Resizing a Kubernetes Cluster

To resize a Kubernetes cluster, use the following command:

```
$ cfssl resize-cluster -name=my-cluster -size=3
```

This command resizes the Kubernetes cluster with the name my-cluster to three nodes.

## Getting the Status of a Kubernetes Cluster

To get the status of a Kubernetes cluster, use the following command:

```
$ cfssl get-status -name=my-cluster
```

This command gets the status of the Kubernetes cluster with the name my-cluster.

## Getting Help

To get help for a particular command, use the following command:

```
$ cfssl help <command>
```

This command gets help for the cfssl command.

## External Links

- [Cfssl Documentation](https://pkg.go.dev/mod/github.com/cloudflare/cfssl?tab=doc)
- [Kubernetes Documentation](https://kubernetes.io/docs/home/)