---
title: Kubernetes 플러그인: kubectl에 사용자 지정 기능 추가
description: 
published: true
date: 2023-02-06T06:17:30.675Z
tags: 
editor: markdown
dateCreated: 2023-02-06T06:17:25.028Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes Plugins: Adding Custom Functionality to kubectl***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-plugins-adding-custom-functionality-to-kubectl)
{.links-list}


# 쿠버네티스 플러그인: kubectl에 커스텀 기능 추가하기

Kubernetes는 컨테이너화된 애플리케이션의 배포, 확장 및 관리를 자동화하기 위한 오픈 소스 오케스트레이션 플랫폼입니다. kubectl은 Kubernetes 클러스터와 상호 작용하기 위한 명령줄 도구입니다.

kubectl은 매우 강력하지만 특정 워크플로에 대해 훨씬 더 효율적으로 만들기 위해 사용자 지정 기능을 추가하려는 경우가 있습니다. 바로 여기에서 Kubernetes 플러그인이 등장합니다.

Kubernetes 플러그인은 kubectl의 기능을 확장하는 코드 조각입니다. 이 기사에서는 Kubernetes 플러그인을 생성하는 방법과 이를 사용하여 kubectl에 사용자 지정 기능을 추가하는 방법을 살펴보겠습니다.

## 쿠버네티스 플러그인 생성

Kubernetes 플러그인은 Go로 작성됩니다. 플러그인 코드는 바이너리로 컴파일하고 PATH에 배치해야 합니다. 바이너리 이름은 kubectl-{plugin-name}이어야 합니다.

플러그인 바이너리는 다음 인터페이스를 구현해야 합니다.

```go
type KubernetesPlugin interface {
	Run([]string) error
}
```

Run() 메서드는 플러그인이 실행될 때 호출되며 플러그인의 인수가 포함된 문자열 배열이 전달됩니다.

인사말을 인쇄하는 예제 플러그인을 살펴보겠습니다.

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

플러그인을 컴파일하기 위해 go build 명령을 사용할 수 있습니다.

```
$ go build -o kubectl-greet ./greet.go
```

플러그인이 빌드되면 PATH에 추가하고 테스트할 수 있습니다.

```
$ export PATH=$PATH:$(pwd)
$ kubectl greet
Hello, world!
```

## kubectl에 기능 추가하기

이제 기본 Kubernetes 플러그인을 만들었으므로 이를 사용하여 kubectl에 사용자 지정 기능을 추가하는 방법을 살펴보겠습니다.

이 예에서는 지정된 네임스페이스의 포드 목록을 인쇄하는 플러그인을 생성합니다. 플러그인에 전달해야 하는 정보가 포함된 구조체를 정의하는 것으로 시작하겠습니다.

```go
type PodListOptions struct {
	Namespace string
}
```

다음으로 플러그인의 인수를 구문 분석하고 PodListOptions 구조체를 초기화하는 함수를 만듭니다.

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

이제 플러그인의 Run() 메서드를 업데이트하여 parseArgs() 함수를 호출하고 결과 PodListOptions 구조체를 사용하여 지정된 네임스페이스의 포드 목록을 인쇄할 수 있습니다.

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

마지막으로 Kubernetes API에서 포드 목록을 실제로 가져오려면 listPods() 메서드를 구현해야 합니다.

```go
func (p *PodListPlugin) listPods(namespace string) ([]string, error) {
	// TODO: Implement me!
}
```

플러그인이 완료되면 PATH에 추가하고 테스트할 수 있습니다.

```
$ export PATH=$PATH:$(pwd)
$ kubectl pod-list my-namespace
pod-1
pod-2
pod-3
```

보시다시피 Kubernetes 플러그인은 kubectl에 사용자 정의 기능을 추가하는 훌륭한 방법을 제공합니다. 몇 줄의 코드만으로 kubectl이 원하는 대로 정확하게 작동하도록 만들 수 있습니다.

## 참조

https://kubernetes.io/docs/reference/using-api/extending-api/
https://kubernetes.io/docs/tasks/extend-kubectl/kubectl-plugins/