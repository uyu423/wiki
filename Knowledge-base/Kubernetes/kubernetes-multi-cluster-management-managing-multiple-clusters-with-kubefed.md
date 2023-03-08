---
title: Kubernetes 다중 클러스터 관리: kubefed로 다중 클러스터 관리
description: 
published: true
date: 2023-02-14T04:32:31.626Z
tags: 
editor: markdown
dateCreated: 2023-02-14T04:32:29.978Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes Multi-Cluster Management: Managing Multiple Clusters with kubefed***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-multi-cluster-management-managing-multiple-clusters-with-kubefed)
{.links-list}



# 쿠버네티스 다중 클러스터 관리: kubefed로 다중 클러스터 관리하기

프로덕션 환경에서 여러 Kubernetes 클러스터를 갖는 것은 드문 일이 아닙니다. 이는 확장성, 고가용성 또는 서로 다른 프로젝트에서 작업하는 서로 다른 팀을 포함하여 다양한 이유 때문일 수 있습니다.

여러 Kubernetes 클러스터를 관리하는 것은 특히 클러스터를 동기화 상태로 유지하는 것과 관련하여 어려울 수 있습니다. 여러 Kubernetes 클러스터를 관리하기 위한 몇 가지 옵션이 있지만 이 기사에서는 kubefed에 중점을 둘 것입니다.

kubefed는 여러 Kubernetes 클러스터를 관리하는 데 사용할 수 있는 도구입니다. Kubernetes 프로젝트의 일부이며 Kubernetes 클러스터 연합을 쉽게 만들고 유지 관리할 수 있도록 설계되었습니다.

kubefed에는 다음과 같은 몇 가지 종속성이 있습니다.

- kubectl
- kube-apiserver
- kube-컨트롤러-매니저

kubefed에는 다음 요구 사항을 충족하는 Kubernetes 클러스터도 필요합니다.

- 쿠버네티스 버전 1.4 이상
- 클러스터에 RBAC가 활성화되어 있어야 합니다.

## kubefed 클러스터 생성

kubefed 클러스터를 만드는 것은 쉽습니다. 먼저 kubefed 구성을 저장하는 데 사용할 ConfigMap을 생성해야 합니다. 이 ConfigMap을 "kubefed-config"라고 합니다.

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: kubefed-config
  namespace: kube-system
data:
  kubefed.yaml: |
    apiVersion: federation/v1beta1
    kind: Federation
    metadata:
      name: federation
    spec:
      # Add clusters to the federation here.
      clusters:
      - clusterName: cluster1
        serverAddressByClientCIDRs:
        - clientCIDR: 0.0.0.0/0
          serverAddress: https://10.0.1.1:6443
      - clusterName: cluster2
        serverAddressByClientCIDRs:
        - clientCIDR: 0.0.0.0/0
          serverAddress: https://10.0.2.1:6443
    ```

이 ConfigMap은 연합에 추가하려는 두 개의 Kubernetes 클러스터를 정의합니다. "clusters" 목록의 "cluster1" 및 "cluster2" 항목은 추가하려는 클러스터의 이름입니다. "serverAddressByClientCIDRs" 항목은 각 클러스터에 대한 Kubernetes API 서버의 URL을 정의합니다.

다음으로 각 클러스터의 kubeconfig 파일을 저장하는 데 사용할 시크릿을 생성해야 합니다. 이 보안 비밀을 "kubefed-kubeconfig"라고 합니다.

```
apiVersion: v1
kind: Secret
metadata:
  name: kubefed-kubeconfig
  namespace: kube-system
data:
  kubeconfig-cluster1: |
    apiVersion: v1
    kind: Config
    clusters:
    - cluster:
        server: https://10.0.1.1:6443
        name: cluster1
      name: cluster1
    contexts:
    - context:
        cluster: cluster1
        user: admin
      name: cluster1
    current-context: cluster1
    preferences: {}
    users:
    - name: admin
      user:
        token: abcdefg
  kubeconfig-cluster2: |
    apiVersion: v1
    kind: Config
    clusters:
    - cluster:
        server: https://10.0.2.1:6443
        name: cluster2
      name: cluster2
    contexts:
    - context:
        cluster: cluster2
        user: admin
      name: cluster2
    current-context: cluster2
    preferences: {}
    users:
    - name: admin
      user:
        token: hijklmnop
    ```

이 시크릿에는 각 클러스터의 kubeconfig 파일이 포함되어 있습니다. cluster1의 kubeconfig 파일은 "kubeconfig-cluster1" 키에 저장되고 cluster2의 kubeconfig 파일은 "kubeconfig-cluster2" 키에 저장됩니다.

ConfigMap과 Secret이 있으면 이제 kubefed 클러스터를 만들 수 있습니다. kubectl 명령을 사용하여 kubefed 클러스터를 생성합니다.

```
kubectl create -f kubefed-configmap.yaml
kubectl create -f kubefed-secret.yaml
kubectl create -f kubefed-cluster.yaml
```

이렇게 하면 "kubefed"라는 새 Kubernetes 클러스터가 생성됩니다. 이 클러스터는 ConfigMap 및 Secret에서 정의한 다른 두 Kubernetes 클러스터를 관리하는 데 사용됩니다.

## kubefed에 클러스터 추가

이제 kubefed 클러스터가 있으므로 여기에 다른 Kubernetes 클러스터를 추가할 수 있습니다. kubefed 명령을 사용하여 클러스터를 추가합니다.

```
kubefed join cluster1 --host-cluster-context=cluster1 --cluster-context=cluster1
kubefed join cluster2 --host-cluster-context=cluster2 --cluster-context=cluster2
```

이렇게 하면 "cluster1" 및 "cluster2" Kubernetes 클러스터가 kubefed 클러스터에 추가됩니다. "--host-cluster-context" 및 "--cluster-context" 인수는 호스트 클러스터(kubefed) 및 추가되는 클러스터(cluster1 또는 cluster2)에 사용할 kubeconfig 컨텍스트를 지정합니다.

## kubefed 관리

이제 kubefed 클러스터를 가동하고 실행했으므로 이를 사용하여 다른 Kubernetes 클러스터를 관리할 수 있습니다.

kubefed 명령은 kubefed 및 관리 중인 Kubernetes 클러스터를 관리하는 데 사용할 수 있습니다.

kubefed가 관리하는 Kubernetes 클러스터를 나열하려면 "kubefed list" 명령을 사용하십시오.

```
kubefed list
```

그러면 kubefed가 현재 관리하고 있는 Kubernetes 클러스터가 나열됩니다.

특정 Kubernetes 클러스터에 대한 자세한 정보를 얻으려면 "kubefed describe" 명령을 사용하십시오.

```
kubefed describe cluster1
```

이렇게 하면 "cluster1" Kubernetes 클러스터에 대한 자세한 정보가 제공됩니다.

kubefed 명령을 사용하여 Kubernetes 클러스터를 확장할 수도 있습니다. 클러스터를 확장하려면 "kubefed scale" 명령을 사용합니다.

```
kubefed scale cluster1 --replicas=3
```

이렇게 하면 "cluster1" Kubernetes 클러스터가 3개의 복제본으로 확장됩니다.

## kubefed 클러스터 삭제

kubefed 클러스터 사용을 마치면 "kubefed delete" 명령을 사용하여 클러스터를 삭제할 수 있습니다.

```
kubefed delete cluster1
```

이렇게 하면 kubefed에서 "cluster1" Kubernetes 클러스터가 삭제됩니다.

## 결론

kubefed는 여러 Kubernetes 클러스터를 관리하는 데 유용한 도구입니다. 사용하기 쉽고 클러스터를 동기화 상태로 유지하는 데 도움이 될 수 있습니다.