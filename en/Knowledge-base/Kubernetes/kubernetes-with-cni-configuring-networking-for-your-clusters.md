---
title: Kubernetes with CNI: Configuring Networking for Your Clusters
description: 
published: true
date: 2023-02-05T14:17:28.678Z
tags: 
editor: markdown
dateCreated: 2023-02-05T14:17:26.767Z
---

- [Kubernetes con CNI: configuración de redes para sus clústeres***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-with-cni-configuring-networking-for-your-clusters)
{.links-list}
- [带有 CNI 的 Kubernetes：为您的集群配置网络***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-with-cni-configuring-networking-for-your-clusters)
{.links-list}
- [CNI를 사용한 Kubernetes: 클러스터에 대한 네트워킹 구성***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-with-cni-configuring-networking-for-your-clusters)
{.links-list}


# Kubernetes with CNI: Configuring Networking for Your Clusters

Kubernetes is a powerful container management system that enables developers to deploy and manage scalable applications in a cloud-native environment. In order to run Kubernetes clusters, developers need to configure networking for their applications. This can be done using the Container Networking Interface (CNI).

CNI is a library that provides APIs for simplifying the configuration of network interfaces for containers. It is designed to be used with container runtimes, such as Kubernetes, to provide a consistent network configuration experience for developers. CNI provides a portable and extensible network configuration solution that can be used with any container runtime.

In this article, we will show you how to configure networking for Kubernetes clusters using CNI. We will cover the following topics:

- What is CNI?
- How does CNI work?
- How to configure networking for Kubernetes using CNI?

## What is CNI?

CNI is a library that provides APIs for simplifying the configuration of network interfaces for containers. It is designed to be used with container runtimes, such as Kubernetes, to provide a consistent network configuration experience for developers. CNI provides a portable and extensible network configuration solution that can be used with any container runtime.

## How does CNI work?

CNI works by creating a network namespace for each container. A network namespace is a virtual environment that contains its own network configuration. This enables each container to have its own IP address and networking configuration. CNI then uses plugins to configure the network interfaces for each container.

There are two types of CNI plugins:

- **Network** plugins: These plugins configure the network interface for a container.
- **IPAM** plugins: These plugins allocate IP addresses for containers.

## How to configure networking for Kubernetes using CNI?

Kubernetes uses CNI to configure networking for containers. In order to use CNI with Kubernetes, you need to install a CNI plugin. There are many CNI plugins available, such as flannel, Weave Net, and Calico.

In this section, we will show you how to install and configure the flannel CNI plugin.

### Installing the flannel CNI plugin

The flannel CNI plugin is available from the CNI GitHub repository. To install the plugin, you need to download the binary and place it in the `$PATH`.

```
$ wget https://github.com/containernetworking/cni/releases/download/v0.6.0/cni-amd64-v0.6.0.tgz
$ tar -xvzf cni-amd64-v0.6.0.tgz -C /usr/local/bin/
```

### Configuring the flannel CNI plugin

Once the flannel CNI plugin is installed, you need to configure it. The flannel CNI plugin uses a configuration file to configure the network. The configuration file is in JSON format and contains the following fields:

- `name`: The name of the network.
- `type`: The type of the network. The flannel CNI plugin supports the `flannel` type.
- `delegate`: The delegate CNI plugin to use. The flannel CNI plugin uses the `bridge` delegate by default.
- `bridge`: The name of the bridge to use. The flannel CNI plugin creates a bridge with the name `cni0` by default.
- `isGateway`: Specifies whether the bridge is the gateway for the network. The flannel CNI plugin sets this to `true` by default.
- `ipMasq`: Specifies whether to enable IP masquerading. The flannel CNI plugin sets this to `true` by default.
- `mtu`: The MTU of the network. The flannel CNI plugin sets this to `1500` by default.
- `hairpinMode`: Specifies whether to enable hairpin mode. The flannel CNI plugin sets this to `true` by default.

Here is an example flannel CNI plugin configuration:

```json
{
    "name": "my-network",
    "type": "flannel",
    "delegate": {
        "bridge": "cni0"
    },
    "isGateway": true,
    "ipMasq": true,
    "mtu": 1500,
    "hairpinMode": true
}
```

Save the configuration file as `my-network.json` and place it in the `/etc/cni/net.d/` directory.

### Creating the flannel CNI network

Once the flannel CNI plugin is installed and configured, you can create the network using the `cni-add` command. The `cni-add` command takes the path to the configuration file as an argument.

```
$ sudo cni-add my-network.json
```

This will create a network with the name `my-network`. The network will be configured using the settings in the `my-network.json` file.

### Deleting the flannel CNI network

To delete the flannel CNI network, you can use the `cni-del` command. The `cni-del` command takes the path to the configuration file as an argument.

```
$ sudo cni-del my-network.json
```

This will delete the network with the name `my-network`.

## Conclusion

In this article, we showed you how to configure networking for Kubernetes clusters using CNI. We covered the following topics:

- What is CNI?
- How does CNI work?
- How to configure networking for Kubernetes using CNI?

If you have any questions about configuring networking for Kubernetes, please leave a comment below.