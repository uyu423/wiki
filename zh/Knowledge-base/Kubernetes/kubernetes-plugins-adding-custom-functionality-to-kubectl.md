---
title: Kubernetes 插件：向 kubectl 添加自定义功能
description: 
published: true
date: 2023-02-06T06:17:30.675Z
tags: 
editor: markdown
dateCreated: 2023-02-06T06:17:25.037Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes Plugins: Adding Custom Functionality to kubectl***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-plugins-adding-custom-functionality-to-kubectl)
{.links-list}


# Kubernetes 插件：向 kubectl 添加自定义功能

Kubernetes 是一个开源编排平台，用于自动化容器化应用程序的部署、扩展和管理。 kubectl 是一个用于与 Kubernetes 集群交互的命令行工具。

虽然 kubectl 非常强大，但有时您可能希望添加自定义功能以使其对您的特定工作流程更加高效。这就是 Kubernetes 插件的用武之地。

Kubernetes 插件是一段扩展 kubectl 功能的代码。在本文中，我们将了解如何创建 Kubernetes 插件以及如何使用它向 kubectl 添加自定义功能。

## 创建一个 Kubernetes 插件

Kubernetes 插件是用 Go 编写的。插件代码必须编译成二进制文件并放在您的 PATH 中。二进制文件必须命名为 kubectl-{plugin-name}。

插件二进制文件必须实现以下接口：

```go
type KubernetesPlugin interface {
	Run([]string) error
}
```

执行插件时调用 Run() 方法，并向其传递一个包含插件参数的字符串数组。

让我们看一个打印问候语的示例插件：

```go
package main

import "fmt"

type GreetPlugin struct{}

func (p *GreetPlugin) Run(args []string) error {
	fmt.Println("Hello, world!")
	return nil
}

func main() {
	plugin := &GreetPlugin{}
	plugin.Run(nil)
}
```

要编译插件，我们可以使用 go build 命令：

```
$ go build -o kubectl-greet ./greet.go
```

插件构建完成后，我们可以将其添加到我们的 PATH 中并进行测试：

```
$ export PATH=$PATH:$(pwd)
$ kubectl greet
Hello, world!
```

## 向 kubectl 添加功能

现在我们已经创建了一个基本的 Kubernetes 插件，让我们看看如何使用它向 kubectl 添加自定义功能。

对于这个例子，我们将创建一个插件来打印给定命名空间中的 pod 列表。我们将从定义一个包含我们需要传递给插件的信息的结构开始：

```go
type PodListOptions struct {
	Namespace string
}
```

接下来，我们将创建一个函数来解析插件的参数并初始化 PodListOptions 结构：

```go
func parseArgs(args []string) (*PodListOptions, error) {
	if len(args) == 0 {
		return nil, fmt.Errorf("namespace is required")
	}
	options := &PodListOptions{
		Namespace: args[0],
	}
	return options, nil
}
```

现在我们可以更新插件的 Run() 方法来调用我们的 parseArgs() 函数，并使用生成的 PodListOptions 结构来打印给定命名空间中的 pod 列表：

```go
func (p *PodListPlugin) Run(args []string) error {
	options, err := parseArgs(args)
	if err != nil {
		return err
	}
	pods, err := p.listPods(options.Namespace)
	if err != nil {
		return err
	}
	for _, pod := range pods {
		fmt.Println(pod)
	}
	return nil
}
```

最后，我们需要实现 listPods() 方法来实际从 Kubernetes API 中获取 pod 列表：

```go
func (p *PodListPlugin) listPods(namespace string) ([]string, error) {
	// TODO: Implement me!
}
```

插件完成后，我们可以将它添加到我们的 PATH 中并进行测试：

```
$ export PATH=$PATH:$(pwd)
$ kubectl pod-list my-namespace
pod-1
pod-2
pod-3
```

如您所见，Kubernetes 插件提供了一种向 kubectl 添加自定义功能的好方法。只需几行代码，您就可以让 kubectl 完全按照您想要的方式工作。

## 参考

https://kubernetes.io/docs/reference/using-api/extending-api/
https://kubernetes.io/docs/tasks/extend-kubectl/kubectl-plugins/