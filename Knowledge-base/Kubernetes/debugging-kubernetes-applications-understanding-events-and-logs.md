---
title: Kubernetes 애플리케이션 디버깅: 이벤트 및 로그 이해
description: 
published: true
date: 2023-02-17T18:16:18.581Z
tags: 
editor: markdown
dateCreated: 2023-01-31T00:43:18.512Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Debugging Kubernetes Applications: Understanding Events and Logs***English** version of this document is available*](/en/Knowledge-base/Kubernetes/debugging-kubernetes-applications-understanding-events-and-logs)
{.links-list}


# Kubernetes 애플리케이션 디버깅: 이벤트 및 로그 이해

Kubernetes는 강력한 오케스트레이션 도구이지만 여기에서 실행 중인 애플리케이션을 디버깅하기 까다로울 수 있습니다. 이 기사에서는 Kubernetes 애플리케이션 디버깅을 위한 두 가지 중요한 도구인 이벤트와 로그를 살펴보겠습니다.

## 이벤트

이벤트는 Kubernetes 클러스터 내부에서 일어나는 일에 대한 가시성을 확보할 수 있는 좋은 방법입니다. 이벤트를 보려면 `kubectl` 명령을 사용하십시오.

```
kubectl get events
```

그러면 타임스탬프, 유형 등과 함께 클러스터의 모든 이벤트 목록이 반환됩니다.

이벤트는 레이블로 필터링할 수 있으므로 특정 포드와 관련된 이벤트만 보려면 `--selector` 플래그를 사용할 수 있습니다.

```
kubectl get events --selector=app=nginx
```

특정 네임스페이스에 대한 이벤트를 볼 수도 있습니다.

```
kubectl get events --namespace=default
```

마지막으로 `--since` 플래그를 사용하여 특정 시간 이후에 발생한 이벤트만 가져올 수 있습니다.

```
kubectl get events --since=2019-01-01T00:00:00Z
```

## 로그

이벤트 외에도 로그는 Kubernetes 애플리케이션 디버깅을 위한 또 다른 중요한 도구입니다. 팟(Pod)에 대한 로그를 가져오려면 `kubectl` 명령을 사용하십시오.

```
kubectl logs POD_NAME
```

`POD_NAME`을 로그를 가져오려는 팟(Pod)의 이름으로 바꿉니다.

배포의 모든 포드에 대한 로그를 가져올 수도 있습니다.

```
kubectl logs DEPLOYMENT_NAME
```

`DEPLOYMENT_NAME`을 로그를 가져오려는 배포의 이름으로 바꿉니다.

마지막으로 `--since` 플래그를 사용하여 특정 시간 이후에 생성된 로그만 가져올 수 있습니다.

```
kubectl logs --since=2019-01-01T00:00:00Z
```

## 결론

이 기사에서는 Kubernetes 애플리케이션 디버깅을 위한 두 가지 중요한 도구인 이벤트와 로그를 살펴보았습니다. 이벤트는 Kubernetes 클러스터 내부에서 일어나는 일에 대한 가시성을 얻을 수 있는 좋은 방법이며 로그는 애플리케이션 문제를 해결하는 데 사용할 수 있습니다.