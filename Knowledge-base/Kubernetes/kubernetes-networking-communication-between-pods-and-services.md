---
title: Kubernetes 네트워킹: Pod와 서비스 간의 통신
description: 
published: true
date: 2023-01-30T07:32:21.952Z
tags: 
editor: markdown
dateCreated: 2023-01-30T07:32:21.952Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kubernetes Networking: Communication Between Pods and Services***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-networking-communication-between-pods-and-services)
{.links-list}


Kubernetes 포드 네트워킹

Kubernetes 네트워킹은 포드와 서비스 간의 통신을 제공합니다. Pod는 자신이 있는 호스트에 관계없이 다른 Pod와 통신할 수 있습니다. 서비스는 팟(Pod) 위에 추상화를 제공하며 팟(Pod) 세트에서 실행 중인 애플리케이션을 다른 애플리케이션에 노출하는 데 사용할 수 있습니다.

이 게시물에서는 Kubernetes에서 포드와 서비스가 서로 통신하는 방법을 살펴보겠습니다. Kubernetes의 네트워킹에 대한 간략한 개요부터 시작한 다음 포드가 서로 통신하는 방법을 살펴보겠습니다. 마지막으로 포드 집합에서 실행 중인 애플리케이션을 다른 애플리케이션에 노출하는 데 서비스를 사용하는 방법을 살펴보겠습니다.

Kubernetes의 네트워킹

Kubernetes 네트워킹은 컨테이너 네트워크 인터페이스(CNI)를 기반으로 합니다. CNI는 컨테이너의 네트워킹을 구성하는 방법에 대한 사양입니다. Kubernetes는 kubenet 플러그인을 사용하여 CNI를 구현합니다.

Kubenet은 각 포드에 대한 네트워크 네임스페이스를 생성하고 포드의 네트워크 인터페이스가 포드 네트워크 네임스페이스의 구성원이 되도록 구성합니다. 이 네트워크 네임스페이스에는 다른 포드 및 서비스와 통신하는 데 사용되는 가상 이더넷 장치가 포함되어 있습니다.

각 포드에는 고유한 IP 주소도 있습니다. 기본적으로 Kubernetes는 Pod에 대한 노드 서브넷의 IP 주소를 사용합니다. 서로 다른 노드의 포드는 IP 주소를 사용하여 서로 통신할 수 있습니다.

Kubernetes에는 내장 DNS 서버도 있습니다. 이 DNS 서버는 서비스의 IP 주소를 확인하는 데 사용할 수 있습니다.

포드 네트워킹

포드는 IP 주소를 사용하여 서로 통신할 수 있습니다. Kubernetes는 노드의 네트워크를 사용하여 서로 다른 노드의 포드 간에 트래픽을 라우팅합니다.

포드는 서비스 검색을 사용하여 서비스와 통신할 수도 있습니다. 서비스 검색을 통해 포드는 서비스의 IP 주소를 찾을 수 있습니다. 기본적으로 Kubernetes는 서비스 검색에 DNS를 사용합니다. 이는 포드가 서비스의 DNS 이름을 사용하여 서비스와 통신할 수 있음을 의미합니다.

서비스 네트워킹

서비스는 팟(Pod) 세트 위에 있는 추상화입니다. 서비스는 팟(Pod) 세트로 트래픽을 라우팅하기 위한 규칙 세트를 정의합니다.

로드 밸런서를 사용하여 서비스를 다른 애플리케이션에 노출할 수 있습니다. 로드 밸런서는 클라이언트에서 트래픽을 가져와서 서비스에 의해 노출된 포드로 라우팅합니다.

Kubernetes 서비스는 Ingress를 사용하여 노출될 수도 있습니다. Ingress는 HTTP 트래픽을 서비스로 라우팅하기 위한 규칙 집합을 정의하는 Kubernetes 리소스입니다.

결론

이 게시물에서는 Kubernetes에서 네트워킹이 작동하는 방식을 살펴보았습니다. 포드는 IP 주소를 사용하여 서로 통신할 수 있으며 서비스를 사용하여 애플리케이션을 다른 애플리케이션에 노출할 수 있습니다.